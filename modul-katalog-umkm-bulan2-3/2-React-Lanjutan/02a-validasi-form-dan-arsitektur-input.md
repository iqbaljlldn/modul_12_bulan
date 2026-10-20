# 2.2a Validasi Form & Arsitektur Input Terkendali

> **Bacaan wajib sebelum sesi:** Modul React Programmer Pit — **Bab 2.1** (Event Handling & Forms — review form validation) & **Bab 4.1** (TypeScript pada React).  
> **Prasyarat:** Menguasai controlled components dan form handling dari Bulan 2 (Slice 2).

---

## Kenapa Unit Ini Ada?

Sepanjang Bulan 2, validasi form kita hanya mengandalkan atribut bawaan HTML seperti `required`:
```tsx
<input type="text" required />
<input type="number" required min="1" />
```

Meskipun sederhana, validasi bawaan browser memiliki kelemahan mendasar di aplikasi web modern:
1. **Aturan bisnis tidak bisa ditangani:** Browser tidak bisa mengecek nama yang isinya hanya spasi kosong (`"   "`), atau aturan komposit seperti "stok tidak boleh negatif jika status published".
2. **Tampilan error kaku & tidak konsisten:** Balon pesan error (*tooltip*) bawaan browser berbeda-beda di tiap browser (Chrome vs Firefox vs Safari di HP) dan tidak bisa disesuaikan dengan tema aplikasi kita.
3. **Aksesibilitas terbatas:** Pengguna pembaca layar (*screen reader*) seringkali kesulitan mengetahui field mana yang salah jika tidak menggunakan standar atribut ARIA yang benar.

Di unit ini, kita membangun arsitektur validasi form yang bersih, terpisah dari UI, dan didukung penuh oleh TypeScript.

---

## 1. Memisahkan Logika Validasi: Fungsi Murni (*Pure Function*)

Prinsip penting arsitektur software: **jangan campur aduk logika bisnis di dalam JSX tampilan**.

Kita buat file khusus untuk validasi di `src/utils/validate.ts`. Karena ini adalah fungsi murni (*pure function*), kita bisa mengujinya dengan sangat mudah tanpa memerlukan render React.

Buat file `src/utils/validate.ts`:

```ts
export interface FormErrors {
  name?: string
  price?: string
  stock?: string
  merchant_name?: string
}

interface RawValues {
  name: string
  price: string
  stock: string
  merchant_name: string
}

export function validate(values: RawValues): FormErrors {
  const errors: FormErrors = {}

  // 1. Validasi Nama Produk
  if (values.name.trim().length === 0) {
    errors.name = 'Nama produk wajib diisi'
  } else if (values.name.trim().length < 3) {
    errors.name = 'Nama produk minimal 3 karakter'
  }

  // 2. Validasi Harga
  const price = Number(values.price)
  if (values.price.trim().length === 0 || Number.isNaN(price)) {
    errors.price = 'Harga wajib diisi angka'
  } else if (price <= 0) {
    errors.price = 'Harga harus lebih dari 0'
  }

  // 3. Validasi Stok
  const stock = Number(values.stock)
  if (values.stock.trim().length === 0 || Number.isNaN(stock)) {
    errors.stock = 'Stok wajib diisi angka'
  } else if (stock < 0) {
    errors.stock = 'Stok tidak boleh negatif'
  }

  // 4. Validasi Nama UMKM
  if (values.merchant_name.trim().length === 0) {
    errors.merchant_name = 'Nama UMKM wajib diisi'
  }

  return errors
}
```

### Mengapa Tipe `FormErrors` Menggunakan Tanda Tanya (`?`)?
Setiap field bernilai opsional karena jika sebuah field valid (tidak ada kesalahan), kita **tidak menyertakan kuncinya** di objek `errors`.
- Field bermasalah: `{ name: 'Nama produk wajib diisi' }`
- Semua field valid: `{}` (objek kosong)

Untuk mengecek apakah ada error, kita cukup memeriksa jumlah kuncinya:
```ts
const hasErrors = Object.keys(errors).length > 0
```

---

## 2. Mendukung Aksesibilitas di Komponen `Input.tsx`

Buka kembali komponen atomik kita `src/components/ui/Input.tsx`. Kita tambahkan penanganan visual dan semantik ketika prop `error` diberikan:

```tsx
import type { InputHTMLAttributes, ReactNode } from 'react'

interface InputProps extends InputHTMLAttributes<HTMLInputElement> {
  label: ReactNode
  error?: string
}

function Input({ label, id, error, ...props }: InputProps) {
  const isInvalid = error !== undefined

  return (
    <label className="grid gap-1 text-sm font-medium text-slate-700" htmlFor={id}>
      {label}
      <input
        id={id}
        aria-invalid={isInvalid}
        className={`rounded-md border px-3 py-1.5 text-sm text-slate-900 transition focus:ring-1 focus:outline-none ${
          isInvalid
            ? 'border-red-400 focus:border-red-500 focus:ring-red-500'
            : 'border-slate-300 focus:border-emerald-500 focus:ring-emerald-500'
        }`}
        {...props}
      />
      {isInvalid && <span className="text-xs text-red-600">{error}</span>}
    </label>
  )
}

export default Input
```

Perhatikan dua hal penting:
1. **`aria-invalid={isInvalid}`:** Memberi tahu teknologi bantu (seperti screen reader) bahwa input ini dalam kondisi tidak valid.
2. **Pesan error bersyarat:** Teks error merah hanya dirender jika `error !== undefined`.

---

## 3. Siklus Validasi pada Form Submit

Di dalam form, kita simpan state kesalahan:
```tsx
const [fieldErrors, setFieldErrors] = useState<FormErrors>({})
```

Alur saat pengguna menekan tombol Simpan (*submit*):
1. Pengguna klik **Submit**.
2. Jalankan `const errors = validate(values)`.
3. Simpan `setFieldErrors(errors)`.
4. Jika `Object.keys(errors).length > 0`, **HENTIKAN EKSEKUSI (`return`)**. Jangan kirim request ke API!
5. Jika tidak ada error, kosongkan `fieldErrors` dan lanjutkan panggil fungsi API.

Dengan pola ini, server kita terhindar dari request data sampah, dan pengguna mendapatkan umpan balik visual instan di kolom yang keliru.

---

## Latihan Mandiri (30 Menit)

1. **Uji Fungsi `validate` di Console:**
   Coba panggil fungsi `validate` dengan berbagai kombinasi input:
   - `{ name: '   ', price: 'abc', stock: '-5', merchant_name: '' }`
   - Pastikan objek error yang dihasilkan memuat pesan spesifik untuk keempat field.
2. **Tambahkan Aturan Validasi Baru:**
   Tambahkan aturan bahwa nama UMKM tidak boleh kurang dari 3 karakter.

---

## Cek Pemahaman

1. Mengapa kita menggunakan `values.name.trim().length === 0` daripada sekadar `values.name === ''`?
2. Mengapa `Number.isNaN(price)` perlu diperiksa setelah pemanggilan `Number(values.price)`?
3. Apa keunggulan menulis aturan validasi di `src/utils/validate.ts` dibandingkan menulis `if/else` langsung di dalam komponen `ProductForm.tsx`?

---

**Lanjut ke:** `02b-context-api-dan-global-state.md` (Context API & Global Toast Notification)
