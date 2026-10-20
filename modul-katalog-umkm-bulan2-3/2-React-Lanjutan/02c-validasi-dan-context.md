# 2.2c Slice 6 — Form yang Layak (Validasi & Context Toast)

> **Bacaan wajib sebelum sesi:** Modul React Programmer Pit — **Bab 2.1** (Event Handling & Forms) & **Bab 3.1** (Context API).  
> **Prasyarat:** Menyelesaikan `02a` (Validasi Form) dan `02b` (Context Toast).

---

## Tujuan Slice Ini

1. Form tambah produk dan edit produk sekarang **memvalidasi input sebelum dikirim ke API** (bukan hanya mengandalkan `required` HTML bawaan).
2. Input yang bermasalah ditandai secara visual dengan border merah, atribut `aria-invalid`, dan pesan kesalahan teks di bawahnya.
3. Aplikasi memiliki sistem **notifikasi mengambang (toast)** yang muncul saat produk berhasil ditambah, diubah, atau dihapus, memanfaatkan React Context.

---

## Kenapa Ini Penting untuk Produk?

Di dunia nyata, pengguna sering salah memasukkan input (misalnya mengetik harga `0` atau huruf di kolom stok). Validasi di sisi frontend (*client-side validation*) memberikan respons seketika tanpa perlu membebani server atau jaringan.

Sementara itu, notifikasi toast memberikan kepastian tindakan (*action feedback*) kepada pengguna: *"Apakah tombol yang barusan saya klik berhasil menyimpan barang?"* — tanpa perlu popup `alert()` browser yang mengganggu kenyamanan.

---

## Langkah demi Langkah Implementasi

### 1. Hubungkan Validasi ke `ProductForm.tsx`

Buka file `src/components/ProductForm.tsx`.
Impor fungsi `validate` dan tipe `FormErrors` dari `../utils/validate`:

```tsx
import { useState } from 'react'
import type { FormEvent } from 'react'
import type { Category } from '../types/category'
import type { CreateProductInput } from '../types/product'
import { validate } from '../utils/validate'
import type { FormErrors } from '../utils/validate'
import Button from './ui/Button'
import Input from './ui/Input'
import { useToast } from '../hooks/useToast'

interface ProductFormProps {
  categories: Category[]
  onSubmit: (input: CreateProductInput) => Promise<void>
}

// ...
export default function ProductForm({ categories, onSubmit }: ProductFormProps) {
  const { showToast } = useToast()
  const [values, setValues] = useState({
    name: '',
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
        price: Number(values.price),
        stock: Number(values.stock),
        merchant_name: values.merchant_name.trim(),
        category_id: Number(values.category_id),
        status: 'published',
      })

      // 3. Tampilkan toast sukses!
      showToast('Produk berhasil ditambahkan!')

      // Reset form
      setValues({
        name: '',
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

        <Input
          id="merchant_name"
          label="Nama UMKM"
          value={values.merchant_name}
          error={fieldErrors.merchant_name}
          onChange={(e) => setValues({ ...values, merchant_name: e.target.value })}
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

### 2. Terapkan Validasi pada `ProductEditForm.tsx`

Terapkan pola yang persis sama pada komponen modal edit `src/components/ProductEditForm.tsx`:
- Tambahkan `state fieldErrors`
- Jalankan `validate(values)` di `handleSubmit`
- Teruskan `error={fieldErrors.fieldName}` ke tiap `<Input>`
- Panggil `showToast('Perubahan produk disimpan!')` saat penyimpanan sukses

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

---

## Verifikasi & Pengujian Hasil

Lakukan pengujian skenario berikut di browser:

1. **Uji Validasi Form Kosong:**
   - Buka halaman produk.
   - Langsung klik tombol **Tambah Produk** tanpa mengisi input apa pun.
   - Pastikan border input berubah menjadi merah dan muncul teks error di bawah masing-masing kolom ("Nama produk wajib diisi", "Harga wajib diisi angka", dst).
   - Buka tab **Network** di DevTools — pastikan **TIDAK ADA** request HTTP POST yang dikirim ke server.
2. **Uji Validasi Angka:**
   - Isi harga dengan `-5000` atau `0`.
   - Submit form — pastikan muncul pesan error spesifik: *"Harga harus lebih dari 0"*.
3. **Uji Notifikasi Toast:**
   - Isi form dengan data valid, lalu submit.
   - Kotak hitam mengambang di bawah layar muncul: *"Produk berhasil ditambahkan!"*.
   - Amati toast tersebut: setelah 3 detik, toast harus menghilang secara mulus.
4. **Uji Toast Edit dan Hapus:**
   - Lakukan edit produk dan hapus salah satu produk — pastikan toast yang sesuai muncul untuk setiap tindakan.

---

## Kesalahan Umum yang Sering Muncul

| Gejala | Penyebab | Solusi |
|---|---|---|
| Error "useToast harus dipakai di dalam ToastProvider" | Komponen memanggil `useToast` tetapi `<ToastProvider>` belum dipasang di `main.tsx` | Pastikan `<ToastProvider>` membungkus `<App />` di `src/main.tsx` |
| Form tetap terkirim padahal ada input yang salah | Lupa baris `if (Object.keys(errors).length > 0) return` | Pastikan ada penghentian eksekusi (*early return*) setelah validasi |
| Input error tidak berwarna merah | Prop `error` tidak diteruskan ke `<Input error={fieldErrors.xxx}>` | Periksa koneksi prop `error` pada setiap elemen `<Input>` |

---

**Lanjut ke:** `02d-latihan-dan-pemantapan-slice6.md` (Latihan Pemantapan Slice 6)
