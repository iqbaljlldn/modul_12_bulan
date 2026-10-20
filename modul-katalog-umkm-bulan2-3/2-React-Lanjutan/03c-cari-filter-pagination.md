# 2.3c Slice 7 — Cari, Filter, Urutkan, Pagination

> **Bacaan wajib sebelum sesi:** Modul React Programmer Pit — **Bab 2.3** (useEffect & Cleanup), **Bab 3.3** (Performance), **Bab 3.5** (React Router Advanced — Search Params).  
> **Prasyarat:** Menyelesaikan `03a` (Debounce) dan `03b` (URL Search Params).

---

## Tujuan Slice Ini

Katalog UMKM sekarang memiliki fitur penjelajahan produk yang lengkap:
1. **Pencarian teks (*search*)** berdasarkan nama produk dengan *debounce* 400ms.
2. **Filter kategori** secara dinamis dari API.
3. **Pengurutan (*sorting*)** berdasarkan harga (termurah/termahal) atau tanggal dibuat (terbaru).
4. **Paginasi (*pagination*)** dengan tombol Sebelumnya/Berikutnya dan indikator total halaman.
5. **Seluruh kondisi filter tersimpan di URL**, sehingga bisa di-refresh, dibagikan link-nya, dan mendukung navigasi back/forward browser.

---

## Kenapa Ini Penting untuk Produk?

Di marketplace nyata, katalog produk tidak pernah dimuat sekaligus ke browser. Skalabilitas bergantung pada kemampuan aplikasi meminta potongan data yang relevan dari server (*server-side filtering & pagination*).

Dengan menaruh state di URL, pengguna UMKM bisa mengirimkan link khusus ke pelanggannya (contoh: *"Ini katalog produk kategori Kerajinan kami: `https://katalog.id/?category=3`"*).

---

## Langkah demi Langkah Implementasi

### 1. Definisikan Tipe & Nilai Standar Filter

Buat file `src/types/productFilters.ts`:

```ts
export interface ProductFilters {
  q: string
  categoryId: string
  sort: 'price' | 'created_at'
  order: 'asc' | 'desc'
  page: number
}

export const defaultFilters: ProductFilters = {
  q: '',
  categoryId: '',
  sort: 'created_at',
  order: 'desc',
  page: 1,
}

export const PAGE_SIZE = 6
```

---

### 2. Tambahkan Fungsi `fetchPage` di `src/api/http.ts`

Buka `src/api/http.ts`. Tambahkan fungsi yang membaca data sekaligus header `X-Total-Count`:

```ts
export interface Page<T> {
  data: T[]
  total: number
}

export async function fetchPage<T>(path: string, init?: RequestInit): Promise<Page<T>> {
  const response = await fetch(`${API_URL}${path}`, init)

  if (!response.ok) {
    throw new ApiError(response.status, `Permintaan gagal dengan kode ${response.status}`)
  }

  const data = (await response.json()) as T[]
  const totalHeader = response.headers.get('X-Total-Count')
  const total = totalHeader !== null ? Number(totalHeader) : data.length

  return { data, total }
}
```

---

### 3. Perbarui `src/api/products.ts` untuk Mengirim Query Params

Buka `src/api/products.ts`. Ubah `getProducts` agar menerima filter dan menyusun query string:

```ts
import type { ProductFilters } from '../types/productFilters'
import { PAGE_SIZE } from '../types/productFilters'
import { fetchPage } from './http'
import type { Page } from './http'

export function getProducts(filters: ProductFilters): Promise<Page<Product>> {
  const params = new URLSearchParams()

  if (filters.q.trim().length > 0) {
    params.set('q', filters.q.trim())
  }
  if (filters.categoryId.length > 0) {
    params.set('category_id', filters.categoryId)
  }
  params.set('_sort', filters.sort)
  params.set('_order', filters.order)
  params.set('_page', String(filters.page))
  params.set('_limit', String(PAGE_SIZE))

  return fetchPage<Product>(`/products?${params.toString()}`)
}
```

---

### 4. Perbarui Hook `src/hooks/useProducts.ts`

Buka `src/hooks/useProducts.ts`. Hook ini sekarang menerima `filters: ProductFilters` dan menggunakan `reloadToken` untuk refetching otomatis saat terjadi mutasi data:

```ts
import { useEffect, useState } from 'react'
import { createProduct, deleteProduct, getProducts, updateProduct } from '../api/products'
import type { UpdateProductInput } from '../api/products'
import type { CreateProductInput, Product } from '../types/product'
import type { ProductFilters } from '../types/productFilters'
import { PAGE_SIZE } from '../types/productFilters'

interface UseProductsResult {
  products: Product[]
  total: number
  totalPages: number
  isLoading: boolean
  errorMessage: string | null
  create: (input: CreateProductInput) => Promise<void>
  save: (id: number, input: UpdateProductInput) => Promise<void>
  remove: (id: number) => Promise<void>
}

export function useProducts(filters: ProductFilters): UseProductsResult {
  const [products, setProducts] = useState<Product[]>([])
  const [total, setTotal] = useState(0)
  const [isLoading, setIsLoading] = useState(true)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)
  const [reloadToken, setReloadToken] = useState(0)

  useEffect(() => {
    let ignore = false
    setIsLoading(true)

    async function loadProducts() {
      try {
        const page = await getProducts(filters)
        if (!ignore) {
          setProducts(page.data)
          setTotal(page.total)
          setErrorMessage(null)
        }
      } catch (error) {
        if (!ignore) {
          setErrorMessage(error instanceof Error ? error.message : 'Terjadi kesalahan')
        }
      } finally {
        if (!ignore) {
          setIsLoading(false)
        }
      }
    }

    loadProducts()

    return () => {
      ignore = true
    }
    // Sengaja memakai field satu-satu (bukan objek filters utuh), karena referensi objek
    // dibuat baru di setiap render ProductsPage — jika dipakai langsung, efek akan loop terus-menerus!
    // oxlint-disable-next-line react-hooks/exhaustive-deps
  }, [filters.q, filters.categoryId, filters.sort, filters.order, filters.page, reloadToken])

  async function create(input: CreateProductInput) {
    await createProduct(input)
    setReloadToken((current) => current + 1)
  }

  async function save(id: number, input: UpdateProductInput) {
    await updateProduct(id, input)
    setReloadToken((current) => current + 1)
  }

  async function remove(id: number) {
    await deleteProduct(id)
    setReloadToken((current) => current + 1)
  }

  const totalPages = Math.max(1, Math.ceil(total / PAGE_SIZE))

  return { products, total, totalPages, isLoading, errorMessage, create, save, remove }
}
```

> **Kenapa pakai `reloadToken` alih-alih mengubah state lokal langsung?** Karena dengan filter dan pengurutan aktif, produk yang baru saja ditambah mungkin masuk ke halaman 3 atau urutan paling bawah. Mengambil ulang data dari server menjamin data yang tampil selalu akurat sesuai filter yang aktif.

---

### 5. Buat Komponen Kontrol Filter (`ProductFilters.tsx`)

Buat `src/components/ProductFilters.tsx`:

```tsx
import type { Category } from '../types/category'
import type { ProductFilters as Filters } from '../types/productFilters'

interface ProductFiltersProps {
  filters: Filters
  categories: Category[]
  onChange: (next: Partial<Filters>) => void
}

function ProductFilters({ filters, categories, onChange }: ProductFiltersProps) {
  return (
    <div className="mb-6 flex flex-wrap items-end gap-3 rounded-lg border border-slate-200 bg-white p-4 shadow-sm">
      {/* Input Pencarian */}
      <label className="grid gap-1 text-sm font-medium text-slate-700">
        Cari Produk
        <input
          type="search"
          placeholder="Ketik nama produk..."
          value={filters.q}
          onChange={(e) => onChange({ q: e.target.value, page: 1 })}
          className="rounded-md border border-slate-300 px-3 py-1.5 text-sm text-slate-900 focus:border-emerald-500 focus:ring-1 focus:ring-emerald-500 focus:outline-none"
        />
      </label>

      {/* Filter Kategori */}
      <label className="grid gap-1 text-sm font-medium text-slate-700">
        Kategori
        <select
          value={filters.categoryId}
          onChange={(e) => onChange({ categoryId: e.target.value, page: 1 })}
          className="rounded-md border border-slate-300 px-3 py-1.5 text-sm text-slate-900 focus:border-emerald-500 focus:ring-1 focus:ring-emerald-500 focus:outline-none"
        >
          <option value="">Semua Kategori</option>
          {categories.map((cat) => (
            <option key={cat.id} value={String(cat.id)}>
              {cat.name}
            </option>
          ))}
        </select>
      </label>

      {/* Pengurutan */}
      <label className="grid gap-1 text-sm font-medium text-slate-700">
        Urutkan
        <select
          value={`${filters.sort}-${filters.order}`}
          onChange={(e) => {
            const [sort, order] = e.target.value.split('-') as [Filters['sort'], Filters['order']]
            onChange({ sort, order, page: 1 })
          }}
          className="rounded-md border border-slate-300 px-3 py-1.5 text-sm text-slate-900 focus:border-emerald-500 focus:ring-1 focus:ring-emerald-500 focus:outline-none"
        >
          <option value="created_at-desc">Terbaru</option>
          <option value="price-asc">Harga: Rendah ke Tinggi</option>
          <option value="price-desc">Harga: Tinggi ke Rendah</option>
        </select>
      </label>
    </div>
  )
}

export default ProductFilters
```

> **Aturan Emas UX:** Perhatikan bahwa setiap kali filter atau kata kunci pencarian berubah, kita selalu menyertakan **`page: 1`**. Jika user sedang di halaman 5 lalu mengganti filter, hasil pencarian baru mungkin hanya punya 1 halaman. Jika tidak di-reset ke halaman 1, layar akan kosong!

---

### 6. Buat Komponen Navigasi Halaman (`Pagination.tsx`)

Buat `src/components/Pagination.tsx`:

```tsx
import Button from './ui/Button'

interface PaginationProps {
  page: number
  totalPages: number
  onPageChange: (nextPage: number) => void
}

function Pagination({ page, totalPages, onPageChange }: PaginationProps) {
  if (totalPages <= 1) return null

  return (
    <nav className="mt-8 flex items-center justify-between border-t border-slate-200 pt-4">
      <Button
        variant="secondary"
        disabled={page <= 1}
        onClick={() => onPageChange(page - 1)}
      >
        ← Sebelumnya
      </Button>

      <span className="text-sm font-medium text-slate-600">
        Halaman <strong className="text-slate-900">{page}</strong> dari{' '}
        <strong className="text-slate-900">{totalPages}</strong>
      </span>

      <Button
        variant="secondary"
        disabled={page >= totalPages}
        onClick={() => onPageChange(page + 1)}
      >
        Berikutnya →
      </Button>
    </nav>
  )
}

export default Pagination
```

---

### 7. Gabungkan Semuanya di `src/pages/ProductsPage.tsx`

Lihat kode lengkap penggabungannya:

```tsx
import { useSearchParams } from 'react-router-dom'
import Pagination from '../components/Pagination'
import ProductFilters from '../components/ProductFilters'
import ProductForm from '../components/ProductForm'
import ProductList from '../components/ProductList'
import { useCategories } from '../hooks/useCategories'
import { useDebouncedValue } from '../hooks/useDebouncedValue'
import { useProducts } from '../hooks/useProducts'
import type { ProductFilters as Filters } from '../types/productFilters'
import { defaultFilters } from '../types/productFilters'

function readFilters(searchParams: URLSearchParams): Filters {
  return {
    q: searchParams.get('q') ?? defaultFilters.q,
    categoryId: searchParams.get('category') ?? defaultFilters.categoryId,
    sort: (searchParams.get('sort') as Filters['sort']) ?? defaultFilters.sort,
    order: (searchParams.get('order') as Filters['order']) ?? defaultFilters.order,
    page: Number(searchParams.get('page') ?? defaultFilters.page),
  }
}

function ProductsPage() {
  const [searchParams, setSearchParams] = useSearchParams()
  const urlFilters = readFilters(searchParams)

  // Nilai pencarian di-debounce 400ms sebelum dikirim ke API
  const debouncedQuery = useDebouncedValue(urlFilters.q, 400)
  const activeFilters: Filters = { ...urlFilters, q: debouncedQuery }

  const { products, totalPages, isLoading, errorMessage, create, save, remove } =
    useProducts(activeFilters)
  const categories = useCategories()

  function handleFilterChange(next: Partial<Filters>) {
    const merged = { ...urlFilters, ...next }
    setSearchParams({
      q: merged.q,
      category: merged.categoryId,
      sort: merged.sort,
      order: merged.order,
      page: String(merged.page),
    })
  }

  return (
    <section className="mx-auto max-w-5xl p-6">
      <h1 className="mb-6 text-2xl font-bold text-slate-900">Katalog Produk UMKM</h1>

      <ProductForm categories={categories} onSubmit={create} />

      <ProductFilters filters={urlFilters} categories={categories} onChange={handleFilterChange} />

      {isLoading ? (
        <p className="text-slate-500">Memuat produk...</p>
      ) : errorMessage !== null ? (
        <p role="alert" className="text-red-600">
          Gagal memuat produk: {errorMessage}
        </p>
      ) : (
        <>
          <ProductList
            products={products}
            categories={categories}
            onSave={save}
            onDelete={remove}
          />
          <Pagination
            page={urlFilters.page}
            totalPages={totalPages}
            onPageChange={(page) => handleFilterChange({ page })}
          />
        </>
      )}
    </section>
  )
}

export default ProductsPage
```

---

## Verifikasi & Pengujian Hasil

Buka browser dan lakukan uji komprehensif berikut:
1. **Uji Debounce:** Ketik kata pencarian di kolom "Cari Produk". Buka tab Network — pastikan hanya 1 request yang terkirim setelah kamu berhenti mengetik selama 400ms.
2. **Uji Filter Kategori:** Pilih salah satu kategori — amati URL di browser berubah menjadi `/?category=...&page=1` dan daftar produk terfilter.
3. **Uji Pengurutan:** Pilih "Harga: Rendah ke Tinggi" — pastikan produk termurah berada di posisi teratas.
4. **Uji Paginasi:** Klik "Berikutnya" — halaman berpindah ke 2, produk halaman berikutnya muncul. Tombol "Sebelumnya" menjadi aktif.
5. **Uji Ketahanan Refresh:** Salin URL lengkap dari address bar (misal: `http://localhost:5173/?category=2&sort=price&order=asc&page=2`), buka di tab baru atau tekan F5 — pastikan seluruh filter tetap aktif sama persis!

---

**Lanjut ke:** `03d-latihan-dan-pemantapan-slice7.md` (Latihan Pemantapan Slice 7)
