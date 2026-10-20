# 4.0b Slice 4 — Halaman Detail & Navigasi (React Router)

## Tujuan slice ini

Klik nama produk di daftar → pindah ke **halaman tersendiri** yang menampilkan detail produk itu, dengan URL sendiri (misal `/products/3`). Ini penutup Bulan 2 — setelah slice ini, Mini Katalog UMKM v1 selesai.

> **Prasyarat:** kamu sudah menyelesaikan `04a` (React Router dasar). Kalau `BrowserRouter`, `Route`, `Link`, dan `useParams` belum klik, baca lagi dulu.

## Bacaan wajib (modul React bootcamp)

- **Bab 3.4** — React Router Routing Dasar (review kalau belum solid)

## Kenapa ini penting untuk produk

Aplikasi nyata punya banyak halaman dengan URL masing-masing (bisa di-bookmark, di-refresh, dibagikan link-nya). Slice ini memperkenalkan itu lewat kasus paling sederhana: halaman detail.

## Konsep yang dipakai

- **React Router**: `BrowserRouter`, `Routes`, `Route`, `Link`, `useParams`
- **Route parameter** (`:id` di URL)
- Menyambungkan lagi ke fetch data (kali ini untuk **satu** produk, bukan daftar)

## Langkah demi langkah

### 1. Install React Router (kalau belum ada)

```bash
npm install react-router-dom
```

### 2. Bungkus aplikasi dengan `BrowserRouter`

Ubah `src/main.tsx`:

```tsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import { BrowserRouter } from 'react-router-dom'
import './index.css'
import App from './App.tsx'

createRoot(document.getElementById('root')!).render(
  <StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </StrictMode>,
)
```

`BrowserRouter` harus membungkus di level paling atas supaya semua komponen di dalamnya bisa memakai fitur routing (`Link`, `useParams`, dst).

### 3. Definisikan rute di `App.tsx`

```tsx
import { Route, Routes } from 'react-router-dom'
import ProductDetailPage from './pages/ProductDetailPage'
import ProductsPage from './pages/ProductsPage'

function App() {
  return (
    <main>
      <h1>Katalog UMKM</h1>
      <Routes>
        <Route path="/" element={<ProductsPage />} />
        <Route path="/products/:id" element={<ProductDetailPage />} />
      </Routes>
    </main>
  )
}

export default App
```

`:id` di `/products/:id` adalah **route parameter** — bagian URL yang berubah-ubah (misal `/products/1`, `/products/7`), yang nanti kita baca lewat `useParams()`.

### 4. Tambahkan fungsi ambil satu produk

Di `src/api/products.ts`, tambahkan:

```ts
export function getProduct(id: number): Promise<Product> {
  return fetchJson<Product>(`/products/${id}`)
}
```

### 5. Bikin halaman detail

Buat `src/pages/ProductDetailPage.tsx`:

```tsx
import { useEffect, useState } from 'react'
import { Link, useParams } from 'react-router-dom'
import { getProduct } from '../api/products'
import { ApiError } from '../errors/ApiError'
import type { Product } from '../types/product'
import { formatRupiah } from '../utils/format'

function ProductDetailPage() {
  // useParams selalu memberi string (dari URL), jadi id diubah ke number.
  const { id } = useParams<{ id: string }>()
  const [product, setProduct] = useState<Product | null>(null)
  const [isLoading, setIsLoading] = useState(true)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)

  useEffect(() => {
    let ignore = false

    async function loadProduct() {
      try {
        const data = await getProduct(Number(id))
        if (!ignore) {
          setProduct(data)
        }
      } catch (error) {
        if (!ignore) {
          setErrorMessage(
            error instanceof ApiError ? error.message : 'Terjadi kesalahan tak terduga',
          )
        }
      } finally {
        if (!ignore) {
          setIsLoading(false)
        }
      }
    }

    loadProduct()

    return () => {
      ignore = true
    }
  }, [id])

  if (isLoading) {
    return <p>Memuat produk...</p>
  }

  if (errorMessage !== null || product === null) {
    return (
      <div>
        <p role="alert">{errorMessage ?? 'Produk tidak ditemukan'}</p>
        <Link to="/">Kembali ke katalog</Link>
      </div>
    )
  }

  return (
    <article>
      <p>
        <Link to="/">Kembali ke katalog</Link>
      </p>
      <h2>{product.name}</h2>
      {product.status === 'draft' && <span className="badge">Draft</span>}
      <p>{product.description}</p>
      <p>
        <strong>{formatRupiah(product.price)}</strong>
      </p>
      <p>{product.stock === 0 ? 'Stok habis' : `Stok: ${product.stock}`}</p>
      <p>
        <small>{product.merchant_name}</small>
      </p>
    </article>
  )
}

export default ProductDetailPage
```

**Perhatikan `[id]` di dependency array `useEffect`.** Kalau user pindah dari `/products/1` langsung ke `/products/2` (tanpa lewat halaman katalog dulu), komponen ini **tidak dibongkar ulang** oleh React — cuma props/params-nya berubah. Karena `id` ada di dependency array, `useEffect` akan jalan lagi mengambil data produk yang baru. Kalau baris `[id]` ini dihapus (atau salah isi), halaman detail akan "nyangkut" menampilkan produk lama.

### 6. Sambungkan nama produk ke halaman detail

Ubah `src/components/ProductCard.tsx`, ganti judul jadi link:

```tsx
import { Link } from 'react-router-dom'

// ...

<h3>
  <Link to={`/products/${product.id}`}>{product.name}</Link>
</h3>
```

### 7. Cek hasilnya

- Dari halaman katalog, klik nama salah satu produk → harus pindah ke `/products/<id>` dan menampilkan detailnya.
- **Refresh halaman detail langsung** (bukan lewat klik) — harus tetap menampilkan data yang benar. Ini membuktikan routing berbasis URL, bukan cuma state di memori.
- Coba buka URL dengan id yang tidak ada, misal `/products/999` — harus muncul pesan "Produk tidak ditemukan", bukan halaman kosong/error mentah.
- Klik "Kembali ke katalog" — harus balik ke `/`.

## Latihan

1. Tambahkan tombol "Edit" dan "Hapus" juga di halaman detail (pakai fungsi API yang sudah ada dari Slice 3).
2. Setelah menghapus produk dari halaman detail, arahkan otomatis kembali ke `/` (cari fungsi `useNavigate` dari `react-router-dom`).
3. Bandingkan: apa yang terjadi kalau kamu ganti `<Link to="/">` dengan `<a href="/">` biasa? Coba dan amati bedanya (perhatikan apakah halaman reload penuh atau tidak).

## Cek pemahaman

- Kalau `BrowserRouter` di `main.tsx` dihapus, apa yang akan terjadi saat `App.tsx` mencoba merender `<Routes>`?
- Kenapa `id` dari `useParams()` selalu bertipe `string`, meski yang kita kirim ke `getProduct` butuh `number`?

## Kesalahan umum

| Gejala | Sebab | Solusi |
|---|---|---|
| Klik link, halaman refresh penuh (putih sebentar) | Pakai `<a href>` bukan `<Link to>` | React Router butuh `<Link>` supaya navigasi tanpa reload |
| Detail produk tidak berubah saat pindah dari satu produk ke produk lain | `id` tidak ada di dependency array `useEffect`, atau salah menuliskannya | Pastikan `useEffect(() => { ... }, [id])` |
| `useParams` memberi `undefined` | Path di `<Route>` tidak cocok, misal `path="/product/:id"` (tanpa s) sementara link mengarah ke `/products/:id` | Samakan penulisan path di `Route` dan di `Link to` |

## Penutup Bulan 2

Kalau slice ini sudah jalan, **Mini Katalog UMKM v1 selesai**: tampil, tambah, edit, hapus, dan halaman detail — semuanya lewat API palsu. Sebelum lanjut ke Bulan 3 (`2-React-Lanjutan`), lakukan showcase ke tribe dan cek **Checkpoint keluar Bulan 2** di kurikulum.

---

Kalau masih ada waktu dan ingin latihan tambahan sebelum Bulan 3, lihat: **LATIHAN-TAMBAHAN.md**
