# 2.2b Context API & Notifikasi Global (Toast)

> **Bacaan wajib sebelum sesi:** Modul React Programmer Pit — **Bab 3.1** (useContext & Context API).  
> **Prasyarat:** Menguasai React component tree, props, dan `useState`.

---

## Kenapa Unit Ini Ada?

Bayangkan skenario ini di aplikasi kita:
- Saat pengguna berhasil **menambah produk** di `ProductForm`, kita ingin menampilkan notifikasi: *"Produk berhasil ditambahkan"*.
- Saat pengguna berhasil **mengedit produk** di `ProductEditForm`, kita ingin pesan: *"Perubahan produk disimpan"*.
- Saat pengguna **menghapus produk** dari `ProductCard` di dalam `ProductList`, kita ingin pesan: *"Produk berhasil dihapus"*.

Tampilan notifikasi mengambang (*toast*) ini posisinya berada di **tengah bawah layar aplikasi** (level global). 

Tanpa Context API, bagaimana caranya `ProductCard` (yang letaknya terkubur jauh di dalam `App` → `ProductsPage` → `ProductList` → `ProductCard`) bisa memicu notifikasi di level atas?
Kita harus mengoper fungsi `showToast` sebagai prop melewati 4 lapis komponen! Ini disebut masalah **Prop Drilling**:

```text
❌ MASALAH PROP DRILLING:
App (punya state toast)
 └── ProductsPage (tidak peduli toast, tapi terpaksa nerima prop)
      └── ProductList (tidak peduli toast, tapi terpaksa nerima prop)
           └── ProductCard (baru di sini showToast dipanggil)
```

**React Context API** memecahkan masalah ini dengan menyediakan saluran langsung (*teleport*) dari penyedia data (*Provider*) ke komponen mana pun yang membutuhkannya (*Consumer*), tanpa perantara prop drilling!

---

## 1. Arsitektur 3 File untuk Context yang Bersih & Cepat

Banyak tutorial menggabungkan definisi context, provider, dan hook dalam satu file raksasa. Namun di lingkungan proyek profesional (termasuk Vite + TypeScript), penggabungan tersebut sering memicu peringatan *Fast Refresh* (HMR gagal berjalan mulus jika komponen JSX dicampur dengan fungsi biasa).

Kita akan menerapkan **Arsitektur 3 File**:
1. `src/context/ToastContext.ts` — Definisi tipe dan context (murni TS, tanpa JSX)
2. `src/context/ToastProvider.tsx` — Komponen penyedia state dan render tampilan toast (JSX)
3. `src/hooks/useToast.ts` — Custom hook untuk komponen pemanggil membaca context

---

### Langkah 1: Buat Definisi Context (`src/context/ToastContext.ts`)

```ts
import { createContext } from 'react'

export interface ToastContextValue {
  showToast: (message: string) => void
}

export const ToastContext = createContext<ToastContextValue | null>(null)
```

Perhatikan: nilai awal context kita set `null`. Ini sengaja, agar kita bisa mendeteksi jika ada komponen yang memanggil hook di luar Provider.

---

### Langkah 2: Buat Komponen Provider (`src/context/ToastProvider.tsx`)

```tsx
import { useCallback, useState } from 'react'
import type { ReactNode } from 'react'
import { ToastContext } from './ToastContext'

interface Toast {
  id: number
  message: string
}

let nextId = 1

export function ToastProvider({ children }: { children: ReactNode }) {
  const [toasts, setToasts] = useState<Toast[]>([])

  const showToast = useCallback((message: string) => {
    const id = nextId++
    setToasts((current) => [...current, { id, message }])

    // Hilangkan toast secara otomatis setelah 3 detik (3000ms)
    setTimeout(() => {
      setToasts((current) => current.filter((toast) => toast.id !== id))
    }, 3000)
  }, [])

  return (
    <ToastContext.Provider value={{ showToast }}>
      {children}
      {/* Wadah Tampilan Notifikasi Mengambang */}
      <div className="fixed bottom-4 left-1/2 z-50 grid -translate-x-1/2 gap-2">
        {toasts.map((toast) => (
          <div
            key={toast.id}
            role="status"
            className="rounded-md bg-slate-900 px-4 py-2 text-sm text-white shadow-lg transition-all animate-bounce"
          >
            {toast.message}
          </div>
        ))}
      </div>
    </ToastContext.Provider>
  )
}
```

### Mengapa Menggunakan `useCallback`?
`showToast` dibungkus dengan `useCallback` agar referensi fungsinya tidak berubah di setiap re-render `ToastProvider`, sehingga komponen anak yang menggunakannya tidak ikut re-render tanpa perlu.

---

### Langkah 3: Buat Hook Konsumen (`src/hooks/useToast.ts`)

```ts
import { useContext } from 'react'
import { ToastContext } from '../context/ToastContext'
import type { ToastContextValue } from '../context/ToastContext'

export function useToast(): ToastContextValue {
  const context = useContext(ToastContext)
  if (context === null) {
    throw new Error('useToast harus dipakai di dalam <ToastProvider>')
  }
  return context
}
```

### Kenapa Ada Guard Clause `if (context === null)`?
Jika seorang developer lupa membungkus aplikasi dengan `<ToastProvider>` dan memanggil `useToast()`, kode ini akan langsung melempar error yang jelas dan ramah pemula, alih-alih menyebabkan error misterius `"Cannot read properties of null (reading 'showToast')"`.

---

## 2. Memasang Provider di Puncak Aplikasi (`main.tsx`)

Buka `src/main.tsx`. Bungkus komponen `<App />` dengan `<ToastProvider>`:

```tsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import { BrowserRouter } from 'react-router-dom'
import App from './App.tsx'
import { ToastProvider } from './context/ToastProvider.tsx'
import './index.css'

createRoot(document.getElementById('root')!).render(
  <StrictMode>
    <BrowserRouter>
      <ToastProvider>
        <App />
      </ToastProvider>
    </BrowserRouter>
  </StrictMode>,
)
```

Sekarang, komponen apa pun di dalam `<App />` bebas memanggil `useToast()`!

---

## 3. Cara Memanggil Notifikasi dari Mana Saja

Contoh pemakaian di komponen:
```tsx
import { useToast } from '../hooks/useToast'

function TombolContoh() {
  const { showToast } = useToast()

  return (
    <button onClick={() => showToast('Halo dari komponen terdalam!')}>
      Tes Notifikasi
    </button>
  )
}
```

---

## Latihan Mandiri (30 Menit)

1. **Uji Error Boundary:**
   Coba panggil `useToast()` di komponen sementara di luar `<ToastProvider>`. Amati pesan error di console browser yang memberitahu bahwa Provider belum dipasang.
2. **Eksperimen Durasi:**
   Ubah durasi timeout di `ToastProvider` dari 3000ms menjadi 1500ms. Perhatikan perubahan kecepatan hilangnya notifikasi di layar.

---

## Cek Pemahaman

1. Mengapa `ToastContext` diinisialisasi dengan nilai `null` di `createContext<ToastContextValue | null>(null)`?
2. Mengapa pemisahan 3 file (`Context`, `Provider`, `Hook`) lebih disukai daripada menaruh semuanya di satu file `Toast.tsx`?
3. Sebutkan satu contoh kasus penggunaan Context API selain sistem notifikasi (toast)!

---

**Lanjut ke:** `02c-validasi-dan-context.md` (Slice 6 — Implementasi Validasi Form & Notifikasi Toast)
