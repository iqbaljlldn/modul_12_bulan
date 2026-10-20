# 2.0e Slice 2 — Tambah Produk (Form & POST)

## Tujuan slice ini

Menambahkan form supaya user bisa **menambah produk baru**, tersimpan ke API palsu (`json-server`).

> **Prasyarat:** kamu sudah menyelesaikan `02d` (event handling & form). Kalau pola controlled component dan `handleChange` belum klik, baca lagi dulu.

## Bacaan wajib (modul React bootcamp)

- **Bab 2.1** — Event Handling & Forms (review controlled component dan form handling)

## Kenapa ini penting untuk produk

Ini pertama kalinya kita **mengirim** data, bukan cuma menampilkan. UMKM di produk asli nanti akan sering menambah produk — pola form ini akan kita pakai berkali-kali (nanti dengan validasi lebih lengkap di Bulan 3).

## Konsep yang dipakai

- **Form terkontrol** (*controlled form*) di React: `useState` + `onChange`
- **HTTP POST**
- **`Omit<T, K>`** (utility type) untuk mendeskripsikan data yang dikirim (tanpa `id`, karena `id` dibuat server)
- **Event bertipe**: `ChangeEvent`, `FormEvent`

## Langkah demi langkah

### 1. Tambahkan tipe untuk data yang dikirim

Di `src/types/product.ts`, tambahkan:

```ts
// Data yang diisi user saat menambah produk. id dan created_at dibuat di luar form.
export type CreateProductInput = Omit<Product, 'id' | 'created_at'>
```

`Omit<Product, 'id' | 'created_at'>` artinya: "sama seperti `Product`, tapi tanpa field `id` dan `created_at`". Ini lebih aman daripada menulis ulang semua field manual — kalau `Product` berubah, `CreateProductInput` otomatis ikut menyesuaikan.

### 2. Tambahkan fungsi `createProduct`

Di `src/api/products.ts`, tambahkan:

```ts
export function createProduct(input: CreateProductInput): Promise<Product> {
  return fetchJson<Product>('/products', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    // created_at diisi di sini untuk sementara. Di Bulan 3, server yang mengisinya.
    body: JSON.stringify({ ...input, created_at: new Date().toISOString() }),
  })
}
```

Perhatikan komentarnya: mengisi `created_at` di sisi frontend itu **sementara** dan bukan cara yang benar untuk backend asli — nanti di Bulan 3, server (NestJS) yang akan mengisi ini sendiri. Kita catat supaya tidak lupa membersihkannya nanti.

### 3. Bikin komponen form

Buat `src/components/ProductForm.tsx`. Ini bagian paling banyak kodenya di slice ini — baca pelan-pelan:

```tsx
import { useState } from 'react'
import type { ChangeEvent, FormEvent } from 'react'
import type { CreateProductInput, ProductStatus } from '../types/product'

// Semua nilai form berupa string, karena <input> selalu menghasilkan string.
interface FormValues {
  name: string
  description: string
  price: string
  stock: string
  status: ProductStatus
  merchant_name: string
}

const emptyValues: FormValues = {
  name: '',
  description: '',
  price: '',
  stock: '',
  status: 'active',
  merchant_name: '',
}

function toInput(values: FormValues): CreateProductInput {
  return {
    name: values.name.trim(),
    description: values.description.trim(),
    price: Number(values.price),
    stock: Number(values.stock),
    status: values.status,
    // TODO Slice 5: kategori dipilih user. Sementara diisi 1 (Kuliner).
    category_id: 1,
    merchant_name: values.merchant_name.trim(),
  }
}

interface ProductFormProps {
  onSubmit: (input: CreateProductInput) => Promise<void>
}

function ProductForm({ onSubmit }: ProductFormProps) {
  const [values, setValues] = useState<FormValues>(emptyValues)
  const [isSubmitting, setIsSubmitting] = useState(false)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)

  function handleChange(
    event: ChangeEvent<HTMLInputElement | HTMLTextAreaElement | HTMLSelectElement>,
  ) {
    const { name, value } = event.target
    setValues((current) => ({ ...current, [name]: value }))
  }

  async function handleSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault()
    setIsSubmitting(true)
    setErrorMessage(null)

    try {
      await onSubmit(toInput(values))
      setValues(emptyValues)
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : 'Terjadi kesalahan')
    } finally {
      setIsSubmitting(false)
    }
  }

  return (
    <form className="product-form" onSubmit={handleSubmit}>
      <h2>Tambah produk</h2>

      <label>
        Nama produk
        <input name="name" value={values.name} onChange={handleChange} required />
      </label>

      <label>
        Deskripsi
        <textarea name="description" value={values.description} onChange={handleChange} />
      </label>

      <label>
        Harga (Rp)
        <input
          name="price"
          type="number"
          min="0"
          value={values.price}
          onChange={handleChange}
          required
        />
      </label>

      <label>
        Stok
        <input
          name="stock"
          type="number"
          min="0"
          value={values.stock}
          onChange={handleChange}
          required
        />
      </label>

      <label>
        Status
        <select name="status" value={values.status} onChange={handleChange}>
          <option value="active">Aktif</option>
          <option value="draft">Draft</option>
        </select>
      </label>

      <label>
        Nama UMKM
        <input
          name="merchant_name"
          value={values.merchant_name}
          onChange={handleChange}
          required
        />
      </label>

      {errorMessage !== null && <p role="alert">Gagal menyimpan: {errorMessage}</p>}

      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? 'Menyimpan...' : 'Simpan produk'}
      </button>
    </form>
  )
}

export default ProductForm
```

**Poin-poin penting:**

- **Satu `handleChange` untuk semua input** — trik `[name]: value` (dari atribut `name` di tiap `<input>`) supaya tidak perlu menulis fungsi `onChange` terpisah untuk setiap field.
- **Nilai form selalu string**, walau nanti dikonversi ke `number` di `toInput()`. Ini karena elemen HTML `<input>` selalu mengembalikan string, walau `type="number"`.
- **`event.preventDefault()`** wajib — supaya browser tidak reload halaman (kebiasaan lama HTML form).
- **`disabled={isSubmitting}`** mencegah user klik dua kali saat masih menyimpan.
- Ada `// TODO` yang jujur menyebut keterbatasan sementara (kategori masih hardcode `1`). Ini kebiasaan baik: catat utang kecil di kode, bukan disembunyikan.

### 4. Sambungkan ke `ProductsPage`

Di `src/pages/ProductsPage.tsx`, tambahkan handler dan render form:

```tsx
import { createProduct, getProducts } from '../api/products'
import ProductForm from '../components/ProductForm'
import type { CreateProductInput, Product } from '../types/product'

// ...di dalam ProductsPage, tambahkan sebelum `if (isLoading)`:

async function handleCreate(input: CreateProductInput) {
  const created = await createProduct(input)
  setProducts((current) => [...current, created])
}

// ...lalu di JSX, sebelum <ProductList>:

<ProductForm onSubmit={handleCreate} />
```

Perhatikan `setProducts((current) => [...current, created])` — ini menambahkan produk baru ke state **tanpa fetch ulang** semua data dari server. Lebih cepat dan langsung terasa responsif.

### 5. Cek hasilnya

- Isi form, klik "Simpan produk" → produk baru harus muncul di daftar **tanpa reload halaman**.
- Cek `localhost:3001/products` di tab baru — produk baru harus ada di sana juga (artinya benar-benar tersimpan di `db.json`).
- Coba submit form dengan field kosong (yang `required`) — browser harus mencegah submit.

## Latihan

1. Tambahkan field `sku` (opsional) ke form.
2. Coba isi harga dengan angka negatif. Apakah aplikasi mencegahnya? Kalau tidak, ini bahan diskusi untuk Bulan 3 (validasi form yang lebih lengkap) — untuk sekarang cukup dicatat sebagai temuan.
3. Setelah submit sukses, form otomatis kosong lagi (`setValues(emptyValues)`). Coba hapus baris itu dan lihat bedanya dari sisi pengalaman pengguna.

## Cek pemahaman

- Kenapa nilai di `useState<FormValues>` semuanya `string`, padahal `price` dan `stock` di tipe `Product` adalah `number`?
- Fungsi `toInput()` dipisah dari `handleSubmit()`. Menurutmu apa untungnya dipisah begitu?

## Kesalahan umum

| Gejala | Sebab | Solusi |
|---|---|---|
| Ketik di satu input, semua input berubah | `name` di `<input>` tidak diisi atau salah | Pastikan tiap input punya `name` yang sesuai key di `FormValues` |
| Produk baru punya `price: NaN` | Lupa `Number(values.price)` di `toInput`, atau input kosong | Cek `toInput()`, pastikan konversi tipe benar |
| Klik "Simpan" dua kali bikin dua data terkirim | Tombol tidak di-disable saat `isSubmitting` | Pastikan `disabled={isSubmitting}` terpasang |

## Kaitkan ke rujukan

Form terkontrol (*controlled input*) dan `useState` ada di modul React bootcamp bagian **State Management & Hooks**.

---

Lanjut ke: **04-edit-hapus-dan-error.md** (Slice 3)
