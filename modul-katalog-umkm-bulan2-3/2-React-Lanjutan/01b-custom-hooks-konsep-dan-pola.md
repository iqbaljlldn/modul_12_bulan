# 2.1b Custom Hooks: Konsep, Aturan, dan Ekstraksi Logika

> **Bacaan wajib sebelum sesi:** Modul React Programmer Pit — **Bab 3.2** (Custom Hooks).  
> **Prasyarat:** Memahami `useState` dan `useEffect` dari Bulan 2 (Slice 1 & 2).

---

## Kenapa Unit Ini Ada?

Di akhir Bulan 2, coba buka kembali file `ProductsPage.tsx`. File tersebut mulai terasa sangat panjang dan padat:
- Menyimpan state `products`, `isLoading`, `errorMessage`
- Menjalankan `useEffect` untuk fetching data saat mount
- Mengatur logika `handleCreate`, `handleSave`, `handleDelete`
- Sekaligus merender form, daftar produk, dan modal edit

Semua tercampur dalam satu komponen tampilan. Jika nanti halaman lain (misalnya halaman dasbor admin atau halaman statistik) membutuhkan data produk yang sama, kita terpaksa menyalin-tempel (*copy-paste*) logika `useState` dan `useEffect` tersebut.

Solusi React untuk masalah ini adalah **Custom Hook**: mengekstrak logika stateful ke fungsi terpisah yang bersih dan reusable.

---

## 1. Apa Itu Custom Hook?

Custom Hook hanyalah **fungsi JavaScript/TypeScript biasa**, dengan dua aturan khusus:
1. **Namanya WAJIB diawali kata `use`** (misalnya `useProducts`, `useCategories`, `useToast`). Ini konvensi yang dikenali oleh linter React untuk memvalidasi aturan hooks.
2. **Boleh memanggil Hook React lain di dalamnya** (seperti `useState`, `useEffect`, `useCallback`, dll).

> **PENTING:** Custom Hook **tidak mengembalikan JSX**. Custom Hook mengembalikan **data atau fungsi** (state, fungsi pengubah, status loading, dsb) yang dibutuhkan oleh komponen tampilan.

```text
┌────────────────────────────────────────┐
│          Komponen Tampilan             │
│        (fokus pada render UI)          │
└───────────────────▲────────────────────┘
                    │ memanggil useCategories()
┌───────────────────┴────────────────────┐
│              Custom Hook               │
│ (mengelola state, useEffect, API call) │
└────────────────────────────────────────┘
```

---

## 2. Aturan Penting Hooks (Rules of Hooks)

React mengandalkan urutan pemanggilan hooks untuk mencocokkan state antar re-render. Karena itu:

1. **Hanya panggil Hooks di tingkat teratas (*Top Level*):**
   - ❌ JANGAN memanggil hook di dalam perulangan (`for`, `while`)
   - ❌ JANGAN memanggil hook di dalam percabangan kondisi (`if`, `switch`)
   - ❌ JANGAN memanggil hook di dalam nested function atau event handler
2. **Hanya panggil Hooks dari fungsi React:**
   - ✅ Dari komponen fungsional React
   - ✅ Dari Custom Hook lain
   - ❌ Bukan dari fungsi utilitas biasa yang tidak berawalan `use`

---

## 3. Implementasi Pertama: `useCategories`

Sebelum mengutak-atik produk, kita buat custom hook yang lebih sederhana dulu untuk mengambil data kategori dari API.

### Langkah A: Buat Tipe Kategori
Buat `src/types/category.ts`:
```ts
export interface Category {
  id: number
  name: string
}
```

### Langkah B: Buat Fungsi API Kategori
Buat `src/api/categories.ts`:
```ts
import type { Category } from '../types/category'
import { fetchJson } from './http'

export function getCategories(): Promise<Category[]> {
  return fetchJson<Category[]>('/categories')
}
```

### Langkah C: Buat Hook `src/hooks/useCategories.ts`
```ts
import { useEffect, useState } from 'react'
import { getCategories } from '../api/categories'
import type { Category } from '../types/category'

export function useCategories(): Category[] {
  const [categories, setCategories] = useState<Category[]>([])

  useEffect(() => {
    let ignore = false

    getCategories()
      .then((data) => {
        if (!ignore) {
          setCategories(data)
        }
      })
      .catch(() => {
        // Kategori gagal dimuat bukan alasan mematikan seluruh halaman;
        // form cukup tampil tanpa pilihan kategori dan tetap bisa dipakai.
      })

    return () => {
      ignore = true
    }
  }, [])

  return categories
}
```

### Membedah Pola di Atas:
1. **Pola Flag `ignore`:**
   Di dalam cleanup function `return () => { ignore = true }`, kita mencegah *race condition* jika komponen unmount sebelum respon API selesai diterima.
2. **Graceful Degradation (Penanganan Error Halus):**
   Blok `.catch()` tidak melempar error fatal ke layar. Jika endpoint `/categories` bermasalah, aplikasi tetap bisa berjalan dengan fallback array kosong.
3. **Nilai Kembalian Sederhana:**
   Hook ini cukup mengembalikan `Category[]`. Komponen pemanggil tidak perlu tahu detail `useState` atau `useEffect` di dalamnya.

---

## 4. Cara Komponen Menggunakan Hook Ini

Di komponen mana pun yang butuh data kategori:

```tsx
function KategoriSelector() {
  const categories = useCategories() // ✨ Satu baris, bersih sekali!

  return (
    <select>
      <option value="">Pilih Kategori</option>
      {categories.map((cat) => (
        <option key={cat.id} value={cat.id}>
          {cat.name}
        </option>
      ))}
    </select>
  )
}
```

Bandingkan jika setiap komponen harus menulis `useState`, `useEffect`, `catch`, dan cleanup sendiri!

---

## Latihan Mandiri (30 Menit)

1. **Uji Isolasi Hook:**
   Buat komponen pengujian kecil yang memanggil `useCategories()`. Periksa tab **Network** di browser DevTools untuk memastikan request `GET /categories` terpanggil sekali saat komponen dimuat.
2. **Eksperimen Error:**
   Ubah sementara endpoint di `src/api/categories.ts` menjadi path yang salah (`/categories-salah`). Perhatikan bahwa console mencatat kegagalan, tetapi aplikasi tidak crash (layar putih). Kembalikan path yang benar setelah memahami dampaknya.

---

## Cek Pemahaman

1. Apa perbedaan utama antara fungsi utilitas biasa (misalnya `formatRupiah`) dengan custom hook (misalnya `useCategories`)?
2. Mengapa React melarang pemanggilan hook di dalam blok `if (isLoggedIn) { useState(...) }`?
3. Apa fungsi variabel boolean `ignore` di dalam `useEffect`?

---

**Lanjut ke:** `01c-kategori-styling-custom-hook.md` (Slice 5 — Implementasi Penuh Kategori, Tailwind & useProducts)
