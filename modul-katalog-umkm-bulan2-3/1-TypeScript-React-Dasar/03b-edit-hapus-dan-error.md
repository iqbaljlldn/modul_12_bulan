# 3.0b Slice 3 — Edit & Hapus Produk (PATCH, DELETE, Custom Error)

> **Sesi ini bisa dipecah 2 sesi** kalau squad terasa kewalahan: sesi 1 = edit, sesi 2 = hapus + error handling.

## Tujuan slice ini

Produk yang sudah ada bisa **diedit** (harga dan stok) dan **dihapus**.

> **Prasyarat:** kamu sudah menyelesaikan `03a` (HTTP methods & API patterns). Fungsi `updateProduct`, `deleteProduct`, dan class `ApiError` sudah ditulis.

## Bacaan wajib (modul React bootcamp)

- **Bab 2.2** — Conditional Rendering & Lists (pendalaman: advanced key, rendering patterns)
- **Bab 2.5** — State Management Lanjutan (bagian lifting state — preview untuk sesi 03c)

## Kenapa ini penting untuk produk

CRUD (Create, Read, Update, Delete) baru lengkap di slice ini. Kita juga mulai menangani error dengan lebih rapi — bekal penting sebelum masuk ke backend asli di Bulan 3.

## Konsep yang dipakai

- **HTTP PATCH** (ubah sebagian data) dan **DELETE**
- **`Partial<T>`** (utility type) — field yang boleh sebagian saja diisi
- **Custom Error class** (`ApiError`) untuk membedakan error API dari error lain
- **State lokal per komponen** (`isEditing`) untuk mode edit inline

## Langkah demi langkah

### 1. Bikin class error khusus

Buat `src/errors/ApiError.ts`:

```ts
// Error khusus untuk kegagalan panggilan API, supaya mudah dibedakan
// dari error lain (misal bug di kode sendiri) saat di-catch.
export class ApiError extends Error {
  status: number

  constructor(status: number, message: string) {
    super(message)
    this.name = 'ApiError'
    this.status = status
  }
}
```

**Kenapa perlu class error sendiri?** Sampai sekarang kita cuma pakai `Error` biasa. Dengan `ApiError`, kode yang menangkap error bisa membedakan "ini gagal karena API" (punya `status`) dari error lain (misal bug logika kita sendiri) — nanti ini juga dasar untuk `class` di NestJS, Bulan 3.

### 2. Perbarui `fetchJson` untuk melempar `ApiError`

Ubah `src/api/http.ts`:

```ts
import { API_URL } from '../config'
import { ApiError } from '../errors/ApiError'

export async function fetchJson<T>(path: string, init?: RequestInit): Promise<T> {
  const response = await fetch(`${API_URL}${path}`, init)

  if (!response.ok) {
    throw new ApiError(response.status, `Permintaan gagal dengan kode ${response.status}`)
  }

  // DELETE lewat json-server tidak mengirim body sama sekali.
  if (response.status === 204) {
    return undefined as T
  }

  return (await response.json()) as T
}
```

Baris `response.status === 204` menangani kasus khusus: request `DELETE` yang sukses biasanya tidak membalas data apa pun (status "204 No Content"), jadi kita jangan coba `.json()` pada respons kosong.

### 3. Tambahkan `updateProduct` dan `deleteProduct`

Di `src/api/products.ts`, tambahkan:

```ts
export type UpdateProductInput = Partial<CreateProductInput>

export function updateProduct(id: number, input: UpdateProductInput): Promise<Product> {
  return fetchJson<Product>(`/products/${id}`, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(input),
  })
}

export function deleteProduct(id: number): Promise<void> {
  return fetchJson<void>(`/products/${id}`, { method: 'DELETE' })
}
```

`Partial<CreateProductInput>` artinya semua field jadi **opsional** — cocok untuk PATCH, karena kita hanya mengirim field yang berubah (di slice ini: harga dan stok saja), bukan seluruh data produk.

### 4. Bikin form edit kecil

Buat `src/components/ProductEditForm.tsx`. Slice ini sengaja **hanya membuka dua field** (harga & stok) — dua yang paling sering berubah untuk UMKM sehari-hari:

```tsx
import { useState } from 'react'
import type { ChangeEvent, FormEvent } from 'react'
import type { Product } from '../types/product'
import type { UpdateProductInput } from '../api/products'

interface ProductEditFormProps {
  product: Product
  onSubmit: (input: UpdateProductInput) => Promise<void>
  onCancel: () => void
}

function ProductEditForm({ product, onSubmit, onCancel }: ProductEditFormProps) {
  const [price, setPrice] = useState(String(product.price))
  const [stock, setStock] = useState(String(product.stock))
  const [isSubmitting, setIsSubmitting] = useState(false)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)

  async function handleSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault()
    setIsSubmitting(true)
    setErrorMessage(null)

    try {
      await onSubmit({ price: Number(price), stock: Number(stock) })
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : 'Terjadi kesalahan')
    } finally {
      setIsSubmitting(false)
    }
  }

  return (
    <form className="product-edit-form" onSubmit={handleSubmit}>
      <label>
        Harga (Rp)
        <input
          type="number"
          min="0"
          value={price}
          onChange={(event: ChangeEvent<HTMLInputElement>) => setPrice(event.target.value)}
        />
      </label>
      <label>
        Stok
        <input
          type="number"
          min="0"
          value={stock}
          onChange={(event: ChangeEvent<HTMLInputElement>) => setStock(event.target.value)}
        />
      </label>

      {errorMessage !== null && <p role="alert">Gagal menyimpan: {errorMessage}</p>}

      <div className="product-edit-form__actions">
        <button type="submit" disabled={isSubmitting}>
          {isSubmitting ? 'Menyimpan...' : 'Simpan'}
        </button>
        <button type="button" onClick={onCancel}>
          Batal
        </button>
      </div>
    </form>
  )
}

export default ProductEditForm
```

### 5. Tambahkan mode edit & tombol hapus di `ProductCard`

Ubah `src/components/ProductCard.tsx` supaya punya **state lokal** `isEditing`, dan menampilkan `ProductEditForm` menggantikan tampilan biasa saat mode edit aktif:

```tsx
import { useState } from 'react'
import type { Product } from '../types/product'
import type { UpdateProductInput } from '../api/products'
import { formatRupiah } from '../utils/format'
import ProductEditForm from './ProductEditForm'

interface ProductCardProps {
  product: Product
  onSave: (id: number, input: UpdateProductInput) => Promise<void>
  onDelete: (id: number) => void
}

function ProductCard({ product, onSave, onDelete }: ProductCardProps) {
  const [isEditing, setIsEditing] = useState(false)
  const isOutOfStock = product.stock === 0

  function handleDeleteClick() {
    const confirmed = window.confirm(`Hapus "${product.name}"?`)
    if (confirmed) {
      onDelete(product.id)
    }
  }

  if (isEditing) {
    return (
      <article className="product-card">
        <h3>{product.name}</h3>
        <ProductEditForm
          product={product}
          onCancel={() => setIsEditing(false)}
          onSubmit={async (input) => {
            await onSave(product.id, input)
            setIsEditing(false)
          }}
        />
      </article>
    )
  }

  return (
    <article className="product-card">
      <h3>{product.name}</h3>
      {product.status === 'draft' && <span className="badge">Draft</span>}
      <p>{product.description}</p>
      <p>
        <strong>{formatRupiah(product.price)}</strong>
      </p>
      <p>{isOutOfStock ? 'Stok habis' : `Stok: ${product.stock}`}</p>
      <p>
        <small>{product.merchant_name}</small>
      </p>
      <div className="product-actions">
        <button type="button" onClick={() => setIsEditing(true)}>
          Edit
        </button>
        <button type="button" onClick={handleDeleteClick}>
          Hapus
        </button>
      </div>
    </article>
  )
}

export default ProductCard
```

**`window.confirm()`** dipakai sebagai cara paling sederhana untuk mencegah hapus tidak sengaja. Ini bukan pola final (tampilannya bawaan browser, agak kasar), tapi cukup untuk sekarang — nanti bisa diganti modal custom kalau ada waktu (lihat `LATIHAN-TAMBAHAN.md`).

### 6. Teruskan `onSave`/`onDelete` lewat `ProductList`

Ubah `src/components/ProductList.tsx` supaya meneruskan kedua prop baru:

```tsx
import type { Product } from '../types/product'
import type { UpdateProductInput } from '../api/products'
import ProductCard from './ProductCard'

interface ProductListProps {
  products: Product[]
  onSave: (id: number, input: UpdateProductInput) => Promise<void>
  onDelete: (id: number) => void
}

function ProductList({ products, onSave, onDelete }: ProductListProps) {
  if (products.length === 0) {
    return <p>Belum ada produk.</p>
  }

  return (
    <div className="product-list">
      {products.map((product) => (
        <ProductCard key={product.id} product={product} onSave={onSave} onDelete={onDelete} />
      ))}
    </div>
  )
}

export default ProductList
```

### 7. Tambahkan handler di `ProductsPage`

```tsx
import { createProduct, deleteProduct, getProducts, updateProduct } from '../api/products'
import type { CreateProductInput, Product } from '../types/product'
import type { UpdateProductInput } from '../api/products'

// ...tambahkan dua fungsi ini:

async function handleSave(id: number, input: UpdateProductInput) {
  const updated = await updateProduct(id, input)
  setProducts((current) => current.map((product) => (product.id === id ? updated : product)))
}

async function handleDelete(id: number) {
  await deleteProduct(id)
  setProducts((current) => current.filter((product) => product.id !== id))
}

// ...lalu di JSX:

<ProductList products={products} onSave={handleSave} onDelete={handleDelete} />
```

Perhatikan pola `setProducts((current) => current.map(...))` untuk update, dan `.filter(...)` untuk hapus — dua-duanya mengubah state **tanpa fetch ulang** dari server, sama seperti pola tambah produk di slice sebelumnya.

### 8. Cek hasilnya

- Klik "Edit" di salah satu produk → form kecil muncul menggantikan tampilan kartu.
- Ubah harga/stok, klik "Simpan" → kartu kembali ke tampilan biasa dengan data baru.
- Klik "Hapus" → muncul konfirmasi browser → kalau OK, produk hilang dari daftar.
- Cek lagi `localhost:3001/products` untuk memastikan perubahan benar-benar tersimpan.

## Latihan

1. Coba matikan API sebentar (matikan `json-server`), lalu klik "Simpan" saat edit. Apa yang tampil? Bandingkan dengan sebelum ada `ApiError`.
2. `ProductEditForm` cuma membuka harga & stok. Tambahkan field `status` juga (dropdown seperti di `ProductForm`).
3. Ganti `window.confirm()` untuk hapus dengan pesan yang lebih spesifik (misal menyebut harga produk juga).

## Cek pemahaman

- Kenapa `ProductEditForm` menerima `product` (data lengkap) tapi `onSubmit`-nya hanya mengirim `{ price, stock }`, bukan seluruh objek produk?
- Apa yang membedakan `ApiError` dari `Error` biasa? Di baris mana perbedaan itu benar-benar dipakai?

## Kesalahan umum

| Gejala | Sebab | Solusi |
|---|---|---|
| Klik Edit, tapi form yang muncul di SEMUA kartu, bukan cuma satu | State `isEditing` diletakkan di luar `ProductCard` (misal di `ProductsPage`) | State edit harus lokal, di dalam tiap `ProductCard` |
| Hapus produk tapi tetap muncul sampai refresh manual | Lupa `setProducts` dengan `.filter()` setelah `deleteProduct` sukses | Cek `handleDelete` di `ProductsPage` |
| Error `is not assignable to type 'never'` di `UpdateProductInput` | Salah import — `UpdateProductInput` ada di `api/products.ts`, bukan `types/product.ts` | Perbaiki path import |

---

Lanjut ke: **05-routing-dan-detail.md** (Slice 4)
