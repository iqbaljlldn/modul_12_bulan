# 2.1c Slice 5 — Kategori, Styling Standar Tribe, Custom Hook useProducts

> **Bacaan wajib sebelum sesi:** Modul React Programmer Pit — **Bab 1.4** (Styling), **Bab 3.2** (Custom Hooks), **Bab 4.2** (Advanced Styling).  
> **Prasyarat:** Telah menyelesaikan `01a` (Tailwind & Komponen UI) dan `01b` (Konsep Custom Hook & `useCategories`).

---

## Tujuan Slice Ini

Tiga capaian produk nyata sekaligus yang saling berkaitan:
1. Produk sekarang memiliki **kategori asli** dari relasi API (menggantikan nilai hardcode `category_id: 1` di Bulan 2).
2. Tampilan aplikasi dirombak menggunakan **Tailwind CSS** dengan komponen reusable (`Button`, `Input`, `Badge`).
3. Seluruh logika CRUD produk dipindahkan ke **custom hook `useProducts`**, sehingga `ProductsPage` menjadi sangat ringkas dan berfokus pada penyusunan tata letak.

---

## Kenapa Ini Penting untuk Produk?

Kategori adalah **data relasi pertama** yang kita gunakan secara nyata di aplikasi (`products.category_id` merujuk pada `categories.id`) — ini menjadi modal penting sebelum kita mempelajari relasi tabel *Foreign Key* di database PostgreSQL asli pada Bulan 4.

Standar styling Tailwind disepakati sekali di awal Bulan 3 agar saat nanti peserta dipecah menjadi beberapa squad di fase berikutnya, antarmuka produk tetap konsisten dan tidak saling tabrak gaya.

---

## Langkah demi Langkah Implementasi

### 1. Migrasi Styling ke Tailwind CSS
Pastikan langkah dari bab `01a` sudah diterapkan:
- Paket `@tailwindcss/vite` terpasang di `vite.config.ts`.
- File `src/index.css` berisi `@import "tailwindcss";`.
- Komponen dasar `src/components/ui/Button.tsx` dan `src/components/ui/Input.tsx` sudah siap dipakai.

### 2. Buat Custom Hook `src/hooks/useProducts.ts`
Sekarang kita pindahkan state dan operasi data dari `ProductsPage.tsx` ke dalam hook tersendiri.

Buat file `src/hooks/useProducts.ts`:

```ts
import { useEffect, useState } from 'react'
import { createProduct, deleteProduct, getProducts, updateProduct } from '../api/products'
import type { UpdateProductInput } from '../api/products'
import type { CreateProductInput, Product } from '../types/product'

interface UseProductsResult {
  products: Product[]
  isLoading: boolean
  errorMessage: string | null
  create: (input: CreateProductInput) => Promise<void>
  save: (id: number, input: UpdateProductInput) => Promise<void>
  remove: (id: number) => Promise<void>
}

export function useProducts(): UseProductsResult {
  const [products, setProducts] = useState<Product[]>([])
  const [isLoading, setIsLoading] = useState(true)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)

  useEffect(() => {
    let ignore = false
    setIsLoading(true)

    getProducts()
      .then((data) => {
        if (!ignore) {
          setProducts(data)
          setErrorMessage(null)
        }
      })
      .catch((error) => {
        if (!ignore) {
          setErrorMessage(error instanceof Error ? error.message : 'Terjadi kesalahan')
        }
      })
      .finally(() => {
        if (!ignore) {
          setIsLoading(false)
        }
      })

    return () => {
      ignore = true
    }
  }, [])

  async function create(input: CreateProductInput) {
    const created = await createProduct(input)
    setProducts((current) => [...current, created])
  }

  async function save(id: number, input: UpdateProductInput) {
    const updated = await updateProduct(id, input)
    setProducts((current) => current.map((p) => (p.id === id ? updated : p)))
  }

  async function remove(id: number) {
    await deleteProduct(id)
    setProducts((current) => current.filter((p) => p.id !== id))
  }

  return { products, isLoading, errorMessage, create, save, remove }
}
```

> **Catatan Evolusi:** Di Slice 5 ini, `create`, `save`, dan `remove` masih memperbarui state lokal secara langsung (*optimistic/local update*). Nanti di Slice 7, saat fitur sorting & pagination aktif, hook ini akan kita kembangkan menggunakan pola `reloadToken` untuk refetching otomatis.

---

### 3. Tambahkan Pilihan Kategori di Form Produk

Buka `src/components/ProductForm.tsx`.
Ganti input hardcode dengan elemen `<select>` kategori yang menerima data dari prop `categories: Category[]`:

```tsx
<label className="grid gap-1 text-sm font-medium text-slate-700" htmlFor="category_id">
  Kategori
  <select
    id="category_id"
    value={values.category_id}
    onChange={(e) => setValues((prev) => ({ ...prev, category_id: Number(e.target.value) }))}
    className="rounded-md border border-slate-300 px-3 py-1.5 text-sm text-slate-900 focus:border-emerald-500 focus:ring-1 focus:ring-emerald-500 focus:outline-none"
  >
    {categories.map((cat) => (
      <option key={cat.id} value={cat.id}>
        {cat.name}
      </option>
    ))}
  </select>
</label>
```

Terapkan hal yang sama pada `src/components/ProductEditForm.tsx`.

---

### 4. Tampilkan Badge Kategori di Kartu Produk

Buka `src/components/ProductCard.tsx`.
Terima prop `categories: Category[]`. Cari nama kategori yang sesuai dengan `product.category_id`:

```tsx
const categoryName = categories.find((cat) => cat.id === product.category_id)?.name ?? 'Tanpa Kategori'
```

Tampilkan sebagai badge di dalam kartu:
```tsx
<div className="flex items-center gap-2">
  <span className="rounded bg-slate-100 px-2 py-0.5 text-xs font-medium text-slate-600">
    {categoryName}
  </span>
  <span className="rounded bg-emerald-50 px-2 py-0.5 text-xs font-medium text-emerald-700">
    {product.status}
  </span>
</div>
```

---

### 5. Refaktor `src/pages/ProductsPage.tsx` Menjadi Sangat Rapi

Lihat betapa bersihnya `ProductsPage.tsx` sekarang setelah logika dipisah:

```tsx
import ProductForm from '../components/ProductForm'
import ProductList from '../components/ProductList'
import { useCategories } from '../hooks/useCategories'
import { useProducts } from '../hooks/useProducts'

function ProductsPage() {
  const { products, isLoading, errorMessage, create, save, remove } = useProducts()
  const categories = useCategories()

  return (
    <section className="mx-auto max-w-5xl p-6">
      <h1 className="mb-6 text-2xl font-bold text-slate-900">Katalog Produk UMKM</h1>

      <ProductForm categories={categories} onSubmit={create} />

      {isLoading ? (
        <p className="text-slate-500">Memuat produk...</p>
      ) : errorMessage !== null ? (
        <p role="alert" className="text-red-600">
          Gagal memuat produk: {errorMessage}
        </p>
      ) : (
        <ProductList
          products={products}
          categories={categories}
          onSave={save}
          onDelete={remove}
        />
      )}
    </section>
  )
}

export default ProductsPage
```

---

## Verifikasi & Pengujian Hasil

1. Jalankan `npm run dev` dan buka browser di `http://localhost:5173`.
2. Pastikan tampilan berubah total menjadi modern dan bersih berkat Tailwind CSS.
3. Form Tambah Produk menampilkan pilihan kategori dinamis dari server (`db.json`).
4. Buat produk baru dengan memilih salah satu kategori — pastikan produk muncul di list dengan badge nama kategori yang tepat.
5. Edit dan Hapus produk — pastikan semua fitur CRUD dari Bulan 2 tetap berfungsi 100% normal tanpa regresi.

---

## Kesalahan Umum yang Sering Muncul

| Gejala | Penyebab | Solusi |
|---|---|---|
| Tampilan polos tanpa style Tailwind | Lupa `@import "tailwindcss";` di `index.css` atau plugin belum terdaftar di `vite.config.ts` | Periksa konfigurasi Vite dan import CSS |
| Badge kategori tertulis "Tanpa Kategori" | Data `categories` masih kosong saat render awal atau tipe `id` tidak cocok (string vs number) | Pastikan perbandingan menggunakan tipe angka: `cat.id === Number(product.category_id)` |
| Hook error: "Rendered fewer hooks than expected" | Memanggil hook di dalam blok `if` atau `try/catch` | Pindahkan semua panggilan hook ke baris-baris paling atas komponen |

---

**Lanjut ke:** `01d-latihan-dan-pemantapan-slice5.md` (Latihan Pemantapan Slice 5)
