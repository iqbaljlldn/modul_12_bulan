# 2.1a Styling Standar Tribe: Tailwind CSS & Component Composition

> **Bacaan wajib sebelum sesi:** Modul React Programmer Pit — **Bab 1.4** (Styling dalam React) & **Bab 4.2** (Advanced Styling & UI Libraries).  
> **Prasyarat:** Menyelesaikan Bulan 2 (Mini Katalog UMKM v1 dengan CSS kustom di `index.css`).

---

## Kenapa Unit Ini Ada?

Di Bulan 2, kita menulis CSS manual di satu file besar `src/index.css` (`.product-card`, `.product-form`, `.btn`, dst). Cara ini bagus untuk memahami dasar CSS, tapi saat aplikasi membesar dan dikerjakan banyak squad, cara ini punya kelemahan besar:
1. **Nama class saling tabrak** (*class naming collision*).
2. **File CSS makin membengkak** dan sulit dirapikan karena takut merusak tampilan halaman lain.
3. **Inkonsistensi desain:** warna tombol, ukuran padding, dan radius border beda-beda di tiap komponen karena tiap peserta menebak nilainya sendiri.

Di Bulan 3, tribe mengambil **keputusan standar styling**. Modul ini memakai **Tailwind CSS v4** sebagai standar. Kita juga akan menerapkan pola **Component Composition**: membangun komponen UI atomik yang reusable (`Button`, `Input`, `Badge`) dengan tipe TypeScript yang aman.

---

## 1. Menyiapkan Tailwind CSS v4 di Vite

Di project kita, Tailwind v4 terintegrasi langsung lewat plugin Vite `@tailwindcss/vite`:

### Instalasi paket (sudah disiapkan di starter v2)
```bash
npm install tailwindcss @tailwindcss/vite
```

### Konfigurasi `vite.config.ts`
```ts
import tailwindcss from '@tailwindcss/vite'
import react from '@vitejs/plugin-react'
import { defineConfig } from 'vite'

export default defineConfig({
  plugins: [react(), tailwindcss()],
})
```

### Reset `src/index.css`
Ganti seluruh isi file `src/index.css` yang ratusan baris dari Bulan 2 menjadi satu baris saja:

```css
@import "tailwindcss";
```

> **Apa yang terjadi?** Tailwind v4 secara otomatis meng-scan semua file `.tsx` dan menghasilkan CSS utility yang benar-benar dipakai saja. Semua CSS lama kita buang, dan kita beralih ke utility classes.

---

## 2. Pola Component Composition: Membangun UI Reusable

Daripada mengetik class Tailwind panjang berulang kali di tiap halaman:
```tsx
// ❌ Jangan lakukan ini di mana-mana:
<button className="rounded-md bg-emerald-600 px-3 py-1.5 text-sm font-medium text-white hover:bg-emerald-700 disabled:opacity-50">
  Simpan
</button>
```

Kita satukan di komponen reusable atomik dengan varian yang konsisten.

### Membuat `src/components/ui/Button.tsx`

```tsx
import type { ButtonHTMLAttributes } from 'react'

type ButtonVariant = 'primary' | 'secondary' | 'danger'

interface ButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: ButtonVariant
}

const variantClasses: Record<ButtonVariant, string> = {
  primary: 'bg-emerald-600 text-white hover:bg-emerald-700',
  secondary: 'bg-slate-100 text-slate-700 hover:bg-slate-200',
  danger: 'bg-red-50 text-red-600 hover:bg-red-100',
}

function Button({ variant = 'primary', className = '', ...props }: ButtonProps) {
  return (
    <button
      className={`rounded-md px-3 py-1.5 text-sm font-medium transition disabled:cursor-not-allowed disabled:opacity-50 ${variantClasses[variant]} ${className}`}
      {...props}
    />
  )
}

export default Button
```

### Membedah Pola TypeScript di Atas:
1. **`extends ButtonHTMLAttributes<HTMLButtonElement>`:**
   Memberikan semua atribut standar tombol HTML (`type`, `onClick`, `disabled`, `aria-label`, dll) tanpa kita harus mendefinisikannya satu per satu secara manual.
2. **`variant?: ButtonVariant`:**
   Membatasi pilihan tema tombol hanya pada `'primary' | 'secondary' | 'danger'`. TypeScript akan langsung memberi garis merah jika ada yang menulis `<Button variant="hijau">`.
3. **`Record<ButtonVariant, string>`:**
   Menjamin bahwa setiap varian yang ada di tipe `ButtonVariant` **wajib** punya mapping kelas Tailwind-nya di objek `variantClasses`.
4. **`{ variant = 'primary', className = '', ...props }`:**
   Destructuring dengan default value. Operator `...props` (rest/spread) meneruskan semua atribut yang tidak diekstrak langsung ke elemen `<button>` asli.

---

## 3. Komponen `Input.tsx` Terstandar

Buat `src/components/ui/Input.tsx`:

```tsx
import type { InputHTMLAttributes, ReactNode } from 'react'

interface InputProps extends InputHTMLAttributes<HTMLInputElement> {
  label: ReactNode
  error?: string
}

function Input({ label, id, error, ...props }: InputProps) {
  return (
    <label className="grid gap-1 text-sm font-medium text-slate-700" htmlFor={id}>
      {label}
      <input
        id={id}
        aria-invalid={error !== undefined}
        className={`rounded-md border px-3 py-1.5 text-sm text-slate-900 focus:ring-1 focus:outline-none ${
          error !== undefined
            ? 'border-red-400 focus:border-red-500 focus:ring-red-500'
            : 'border-slate-300 focus:border-emerald-500 focus:ring-emerald-500'
        }`}
        {...props}
      />
      {error !== undefined && <span className="text-xs text-red-600">{error}</span>}
    </label>
  )
}

export default Input
```

Perhatikan:
- `<label>` membungkus seluruh kontrol atau dihubungkan lewat `htmlFor={id}`.
- Prop `error` disiapkan untuk validasi form yang akan kita gunakan secara luas di Slice 6.

---

## Latihan Mandiri (30 Menit)

1. **Uji coba di sandbox:** Buat komponen uji coba yang menampilkan ketiga varian `Button` (`primary`, `secondary`, `danger`) serta kondisi `disabled={true}`. Pastikan cursor berubah menjadi `not-allowed` dan opacity berkurang saat disabled.
2. **Buat komponen `Badge.tsx`:**
   Buat file `src/components/ui/Badge.tsx` dengan varian:
   - `default`: latar abu-abu (`bg-slate-100 text-slate-700`)
   - `success`: latar hijau muda (`bg-emerald-50 text-emerald-700 border border-emerald-200`)
   - `warning`: latar kuning/oranye (`bg-amber-50 text-amber-700 border border-amber-200`)

---

## Cek Pemahaman

1. Apa keuntungan `extends ButtonHTMLAttributes<HTMLButtonElement>` dibanding menulis sendiri prop `onClick` dan `disabled`?
2. Mengapa kita menggabungkan `className` bawaan dengan `className` tambahan dari prop (`${variantClasses[variant]} ${className}`)?
3. Jika tribe memutuskan menggunakan CSS Module alih-alih Tailwind, apa saja yang perlu diubah dari komponen `Button` di atas?

---

**Lanjut ke:** `01b-custom-hooks-konsep-dan-pola.md` (Konsep & Pola Custom Hook)
