# 2.2c Slice 6 — Form yang Layak (Validasi & Context Toast)

> **Bacaan wajib sebelum sesi:** Modul React Programmer Pit — **Bab 2.1** (Event Handling & Forms) & **Bab 3.1** (Context API).  
> **Prasyarat:** Menyelesaikan `02a` (Validasi Form) dan `02b` (Context Toast).

---

## Tujuan Slice Ini

1. Form tambah produk dan form edit inline sekarang **memvalidasi input sebelum dikirim ke API** (bukan hanya mengandalkan `required` HTML bawaan).
2. Input yang bermasalah ditandai secara visual dengan border merah, atribut `aria-invalid`, dan pesan kesalahan teks di bawahnya.
3. Aplikasi memiliki sistem **notifikasi mengambang (toast)** yang muncul saat produk berhasil ditambah, diubah, atau dihapus, memanfaatkan React Context.

---

## Kenapa Ini Penting untuk Produk?

Di dunia nyata, pengguna sering salah memasukkan input (misalnya mengetik harga `0` atau huruf di kolom stok). Validasi di sisi frontend (*client-side validation*) memberikan respons seketika tanpa perlu membebani server atau jaringan.

Sementara itu, notifikasi toast memberikan kepastian tindakan (*action feedback*) kepada pengguna: *"Apakah tombol yang barusan saya klik berhasil menyimpan barang?"* — tanpa perlu popup `alert()` browser yang mengganggu kenyamanan.

---

## Langkah demi Langkah Implementasi (Blok 1)

### 1. Hubungkan Validasi & Toast ke `ProductForm.tsx`

Buka file `src/components/ProductForm.tsx`.
Impor fungsi `validate` dan tipe `FormErrors` dari `../utils/validate`, tetap pertahankan field `description` (sesuai kontrak `CreateProductInput` dari Bulan 2) serta dropdown `<select>` kategori dari Slice 5, dan perhatikan status produk memakai `'active'` sesuai `ProductStatus`:

```tsx
import { useState } from 'react'
import type { FormEvent } from 'react'
import { useToast } from '../hooks/useToast'
import type { Category } from '../types/category'
import type { CreateProductInput } from '../types/product'
import { validate } from '../utils/validate'
import type { FormErrors } from '../utils/validate'
import Button from './ui/Button'
import Input from './ui/Input'

interface ProductFormProps {
  categories: Category[]
  onSubmit: (input: CreateProductInput) => Promise<void>
}

export default function ProductForm({ categories, onSubmit }: ProductFormProps) {
  const { showToast } = useToast()
  const [values, setValues] = useState({
    name: '',
    description: '',
    price: '',
    stock: '',
    merchant_name: '',
    category_id: categories[0]?.id ?? 1,
  })
  const [fieldErrors, setFieldErrors] = useState<FormErrors>({})
  const [isSubmitting, setIsSubmitting] = useState(false)
  const [serverError, setServerError] = useState<string | null>(null)

  async function handleSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault()

    // 1. Jalankan fungsi validasi murni
    const errors = validate(values)
    setFieldErrors(errors)

    // 2. Jika ada field yang salah, hentikan submit!
    if (Object.keys(errors).length > 0) {
      return
    }

    setIsSubmitting(true)
    setServerError(null)

    try {
      await onSubmit({
        name: values.name.trim(),
        description: values.description.trim(),
        price: Number(values.price),
        stock: Number(values.stock),
        merchant_name: values.merchant_name.trim(),
        category_id: Number(values.category_id),
        status: 'active',
      })

      // 3. Tampilkan toast sukses!
      showToast('Produk berhasil ditambahkan!')

      // Reset form
      setValues({
        name: '',
        description: '',
        price: '',
        stock: '',
        merchant_name: '',
        category_id: categories[0]?.id ?? 1,
      })
      setFieldErrors({})
    } catch (err) {
      setServerError(err instanceof Error ? err.message : 'Gagal menyimpan produk')
    } finally {
      setIsSubmitting(false)
    }
  }

  return (
    <form onSubmit={handleSubmit} className="mb-8 rounded-lg border border-slate-200 bg-white p-5 shadow-sm">
      <h2 className="mb-4 text-lg font-semibold text-slate-800">Tambah Produk Baru</h2>

      {serverError && (
        <div role="alert" className="mb-4 rounded bg-red-50 p-3 text-sm text-red-700">
          {serverError}
        </div>
      )}

      <div className="grid gap-4 sm:grid-cols-2">
        <Input
          id="name"
          label="Nama Produk"
          value={values.name}
          error={fieldErrors.name}
          onChange={(e) => setValues({ ...values, name: e.target.value })}
        />

        <Input
          id="merchant_name"
          label="Nama UMKM"
          value={values.merchant_name}
          error={fieldErrors.merchant_name}
          onChange={(e) => setValues({ ...values, merchant_name: e.target.value })}
        />

        <Input
          id="price"
          label="Harga (Rp)"
          type="number"
          value={values.price}
          error={fieldErrors.price}
          onChange={(e) => setValues({ ...values, price: e.target.value })}
        />

        <Input
          id="stock"
          label="Stok"
          type="number"
          value={values.stock}
          error={fieldErrors.stock}
          onChange={(e) => setValues({ ...values, stock: e.target.value })}
        />

        <label className="grid gap-1 text-sm font-medium text-slate-700" htmlFor="category_id">
          Kategori
          <select
            id="category_id"
            value={values.category_id}
            onChange={(e) => setValues({ ...values, category_id: Number(e.target.value) })}
            className="rounded-md border border-slate-300 px-3 py-1.5 text-sm text-slate-900 focus:border-emerald-500 focus:ring-1 focus:ring-emerald-500 focus:outline-none"
          >
            {categories.map((cat) => (
              <option key={cat.id} value={cat.id}>
                {cat.name}
              </option>
            ))}
          </select>
        </label>

        <Input
          id="description"
          label="Deskripsi Singkat (Opsional)"
          value={values.description}
          onChange={(e) => setValues({ ...values, description: e.target.value })}
        />
      </div>

      <div className="mt-4 flex justify-end">
        <Button type="submit" disabled={isSubmitting}>
          {isSubmitting ? 'Menyimpan...' : 'Tambah Produk'}
        </Button>
      </div>
    </form>
  )
}
```

> **Perhatikan:** Atribut bawaan HTML `required` sekarang sudah dilepas dari `<Input>` karena seluruh kendali pesan validasi dikelola secara seragam oleh `src/utils/validate.ts`.

---

### 2. Terapkan Validasi pada Form Edit Inline (`ProductEditForm.tsx`)

Terapkan pola yang sama pada komponen form edit inline `src/components/ProductEditForm.tsx` (yang mengedit harga & stok dari Bulan 2):
- Tambahkan state `fieldErrors` dengan tipe `Pick<FormErrors, 'price' | 'stock'>`
- Jalankan `validateEdit({ price, stock })` di awal `handleSubmit` — hentikan eksekusi jika ada error
- Ganti `<input>` biasa dengan `<Input error={fieldErrors.price} ... />` dan `<Input error={fieldErrors.stock} ... />`
- Panggil `showToast('Perubahan produk disimpan!')` setelah `onSave(...)` sukses

---

### 3. Tambahkan Toast saat Hapus Produk di `ProductsPage.tsx`

Buka `src/pages/ProductsPage.tsx`. Tambahkan pemicu notifikasi saat produk berhasil dihapus:

```tsx
const { showToast } = useToast()

async function handleDeleteProduct(id: number) {
  if (confirm('Yakin ingin menghapus produk ini?')) {
    await remove(id)
    showToast('Produk berhasil dihapus!')
  }
}
```

Pastikan `onDelete={handleDeleteProduct}` diteruskan ke `<ProductList />`.

---

## Verifikasi & Pengujian Hasil (Blok 2 — Pairing)

Lakukan pengujian skenario berikut di browser:

1. **Uji Validasi Form Kosong:**
   - Buka halaman produk.
   - Langsung klik tombol **Tambah Produk** tanpa mengisi input apa pun.
   - Pastikan border input berubah menjadi merah dan muncul teks error di bawah masing-masing kolom ("Nama produk wajib diisi", "Harga wajib diisi angka", dst).
   - Buka tab **Network** di DevTools — pastikan **TIDAK ADA** request HTTP `POST` yang dikirim ke server.
2. **Uji Validasi Angka:**
   - Isi harga dengan `-5000` atau `0`.
   - Submit form — pastikan muncul pesan error spesifik: *"Harga harus lebih dari 0"*.
3. **Uji Notifikasi Toast:**
   - Isi form dengan data valid, lalu submit.
   - Kotak notifikasi mengambang di bawah layar muncul: *"Produk berhasil ditambahkan!"*.
   - Amati toast tersebut: setelah 3 detik, toast harus menghilang secara mulus.
4. **Uji Toast Edit dan Hapus:**
   - Lakukan edit harga/stok secara inline dan hapus salah satu produk contoh — pastikan toast yang sesuai muncul untuk setiap tindakan.

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan individual di kelas dan simpan hasilnya di repositori proyekmu pada:  
`tugas/tugas_02c.md`

1. Tuliskan identitas diri (Nama, Squad, Tanggal).
2. Dokumentasikan hasil verifikasi tab Network saat mencoba submit form kosong vs data valid (lampirkan screenshot/catatan status HTTP).
3. Jelaskan secara singkat mengapa atribut `required` bawaan browser perlu dilepas setelah kita memakai `validate()` kustom.

---

## Kesalahan Umum yang Sering Muncul

| Gejala | Penyebab | Solusi |
|---|---|---|
| Error "useToast harus dipakai di dalam ToastProvider" | Komponen memanggil `useToast` tetapi `<ToastProvider>` belum dipasang di `main.tsx` | Pastikan `<ToastProvider>` membungkus `<App />` di `src/main.tsx` |
| Form tetap terkirim padahal ada input yang salah | Lupa baris `if (Object.keys(errors).length > 0) return` | Pastikan ada penghentian eksekusi (*early return*) setelah validasi |
| Input error tidak berwarna merah | Prop `error` tidak diteruskan ke `<Input error={fieldErrors.xxx}>` | Periksa koneksi prop `error` pada setiap elemen `<Input>` |

---

**Lanjut ke:** `02d-latihan-dan-pemantapan-slice6.md` (Latihan Pemantapan Slice 6)
