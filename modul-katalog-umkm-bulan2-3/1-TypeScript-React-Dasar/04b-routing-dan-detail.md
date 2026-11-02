# 4.0b Slice 4 — Halaman Detail & Navigasi (React Router)

## Tujuan Slice Ini

Menyelesaikan **Slice 4**: ketika nama produk diklik pada kartu katalog, pengguna berpindah ke **halaman detail tersendiri** dengan URL khusus (contoh: `/products/1`). Di halaman ini, kita mengambil data satu produk dari endpoint `GET /products/:id`, mengelola status loading, dan **menangani secara khusus error 404** jika produk tidak ditemukan di server.

---

## Aktivitas Terbimbing di Kelas (Blok 1, 10-15 Menit)

Mentor akan memandu demonstrasi konsep:
- Menambahkan rute dinamis dengan parameter `:id` di `src/App.tsx`.
- Membaca parameter URL lewat `const { id } = useParams<{ id: string }>()`.
- Menulis fungsi API `getProduct(id: number)` di `src/api/products.ts`.
- **Menangani kasus khusus 404:** Menggunakan `instanceof ApiError` untuk mendeteksi `error.status === 404` dan menampilkan pesan ramah *"Produk tidak ditemukan"*.
- Mengapa variabel `id` **wajib** dicantumkan di dependency array `useEffect([id])`.

*(Bahan bacaan pendalaman opsional: Modul React Bootcamp Bab 3.4 tentang React Router Routing Dasar).*

---

## Ringkasan Konsep Kunci & Analogi

### 1. Parameter Rute Dinamis (`:id`)

> **Analogi Kotak Surat Pos:**  
> Rute `/products/:id` seperti **formulir pengambilan barang di loket kantor pos**.  
> Bentuk bangunannya sama persis untuk semua orang (satu komponen `ProductDetailPage`), tetapi nomor yang tertera di kupon (`:id`) menentukan laci barang mana yang dibuka oleh petugas (`GET /products/1` vs `GET /products/2`).

### 2. Mengapa Dependency Array `[id]` Sangat Krusial?

Jika pengguna sedang berada di halaman `/products/1` lalu mengklik tombol rekomendasi ke `/products/2`, React Router **tidak merobohkan dan memasang ulang** komponen `ProductDetailPage`.  
React menggunakan kembali (*re-use*) komponen yang sudah menempel di layar demi efisiensi.  
Jika kamu lupa menulis `[id]` di `useEffect` (atau hanya menulis `[]`), efek pengambilan data **tidak akan dijalankan ulang**, dan halaman akan "terkunci" menampilkan produk lama!

---

## Langkah demi Langkah Mengembangkan Slice 4

### Langkah 1: Tambahkan Fungsi `getProduct` di `src/api/products.ts`

Buka `src/api/products.ts` dan tambahkan fungsi pengambil satu produk berdasarkan id:

```ts
// src/api/products.ts
// ...fungsi getProducts, createProduct, updateProduct, deleteProduct...

// Mengambil detail satu produk berdasarkan ID
export function getProduct(id: number): Promise<Product> {
  return fetchJson<Product>(`/products/${id}`)
}
```

---

### Langkah 2: Daftarkan Rute di `src/App.tsx`

Buka `src/App.tsx` dan pasang komponen `ProductDetailPage`:

```tsx
// src/App.tsx
import { Routes, Route } from 'react-router-dom'
import ProductsPage from './pages/ProductsPage'
import ProductDetailPage from './pages/ProductDetailPage'

function App() {
  return (
    <main style={{ maxWidth: '1000px', margin: '0 auto', padding: '24px 16px' }}>
      <header style={{ marginBottom: '24px' }}>
        <h1>Katalog UMKM Nusantara</h1>
      </header>

      <Routes>
        <Route path="/" element={<ProductsPage />} />
        {/* Rute dinamis berparameter :id */}
        <Route path="/products/:id" element={<ProductDetailPage />} />
      </Routes>
    </main>
  )
}

export default App
```

---

### Langkah 3: Buat Komponen Halaman Detail (`src/pages/ProductDetailPage.tsx`)

Buat berkas `src/pages/ProductDetailPage.tsx`.  
Perhatikan bagaimana blok `catch` menangani `ApiError` dengan `error.status === 404` secara khusus:

```tsx
// src/pages/ProductDetailPage.tsx
import { useEffect, useState } from 'react'
import { Link, useParams } from 'react-router-dom'
import { getProduct } from '../api/products'
import { ApiError } from '../errors/ApiError'
import type { Product } from '../types/product'
import { formatRupiah } from '../utils/format'

function ProductDetailPage() {
  // 1. Ambil id dari parameter URL (selalu bertipe string)
  const { id } = useParams<{ id: string }>()
  const [product, setProduct] = useState<Product | null>(null)
  const [isLoading, setIsLoading] = useState<boolean>(true)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)

  useEffect(() => {
    let ignore = false

    async function loadProductDetail() {
      try {
        // Konversikan string id dari URL ke number untuk API
        const productId = Number(id)
        
        if (Number.isNaN(productId)) {
          throw new Error('ID produk pada URL tidak valid')
        }

        const data = await getProduct(productId)
        if (!ignore) {
          setProduct(data)
        }
      } catch (error) {
        if (!ignore) {
          // TODO: Periksa apakah error merupakan ApiError dengan status 404
          if (error instanceof ApiError && error.status === 404) {
            setErrorMessage('Produk tidak ditemukan')
          } else if (error instanceof ApiError) {
            setErrorMessage(error.message)
          } else if (error instanceof Error) {
            setErrorMessage(error.message)
          } else {
            setErrorMessage('Terjadi kesalahan tak terduga saat memuat detail')
          }
        }
      } finally {
        if (!ignore) {
          setIsLoading(false)
        }
      }
    }

    loadProductDetail()

    return () => {
      ignore = true
    }
  }, [id]) // WAJIB mencantumkan [id] di sini!

  // Kondisi 1: Sedang memuat data
  if (isLoading) {
    return <p className="loading-state">Memuat detail produk...</p>
  }

  // Kondisi 2: Terjadi error atau produk tidak ada (misal akses /products/999)
  if (errorMessage !== null || product === null) {
    return (
      <div className="error-container" style={{ padding: '24px 0' }}>
        <p role="alert" style={{ color: '#e53e3e', fontWeight: 600 }}>
          {errorMessage ?? 'Produk tidak ditemukan'}
        </p>
        <Link to="/" style={{ display: 'inline-block', marginTop: '12px' }}>
          ← Kembali ke Katalog Utama
        </Link>
      </div>
    )
  }

  // Kondisi 3: Data produk berhasil ditemukan
  const isOutOfStock = product.stock === 0

  return (
    <article className="product-detail" style={{ maxWidth: '650px', padding: '16px 0' }}>
      <p>
        <Link to="/">← Kembali ke Katalog Utama</Link>
      </p>

      <h2>{product.name}</h2>
      {product.status === 'draft' && <span className="badge">Draft</span>}

      <p style={{ fontSize: '1.05rem', margin: '16px 0', color: '#4a5568' }}>
        {product.description}
      </p>

      <p style={{ fontSize: '1.25rem' }}>
        Harga: <strong>{formatRupiah(product.price)}</strong>
      </p>

      <p className={isOutOfStock ? 'stock-warning' : ''}>
        {isOutOfStock ? 'Stok produk ini sedang habis' : `Tersedia: ${product.stock} unit`}
      </p>

      <div style={{ marginTop: '20px', padding: '12px', background: '#f7fafc', borderRadius: '8px' }}>
        <p style={{ margin: 0 }}>
          <small>
            Diproduksi oleh: <strong>{product.merchant_name}</strong>
          </small>
        </p>
      </div>
    </article>
  )
}

export default ProductDetailPage
```

---

### Langkah 4: Sambungkan Judul Kartu Menjadi Link di `ProductCard.tsx`

Buka `src/components/ProductCard.tsx`. Ganti elemen judul teks biasa `<h3>{product.name}</h3>` menjadi link yang bisa diklik:

```tsx
// src/components/ProductCard.tsx
import { Link } from 'react-router-dom'

// ...di dalam JSX kembalian ProductCard:
<h3>
  <Link to={`/products/${product.id}`} style={{ textDecoration: 'none', color: '#2b6cb0' }}>
    {product.name}
  </Link>
</h3>
```

---

## Analisis Bug & Prediksi (Aktivitas Blok 2)

Diskusikan bersama rekan pairing:

1. **Uji Kasus Khusus 404:**  
   Buka browsermu, ketikkan langsung di address bar URL produk dengan id yang pasti tidak ada di database:  
   `http://localhost:5173/products/999`  
   *Pertanyaan:* Periksa tampilan layar. Apakah layar menampilkan tulisan ramah *"Produk tidak ditemukan"* ataukah memunculkan error teknis mentah (*"Permintaan gagal dengan kode status 404"* atau layar putih)?
2. **Uji Navigasi URL Langsung (Deep Linking):**  
   Buka halaman detail salah satu produk (contoh `http://localhost:5173/products/1`). Tekan tombol **Refresh (F5)** browser.  
   Apakah data produk tetap muncul dengan benar? Mengapa ini menjadi bukti bahwa arsitektur routing kita bekerja dengan standar web sejati?

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan secara mandiri di kelas. Simpan hasilnya di:  
`tugas/squad-<nomor>/<nama-kamu>/tugas_04b.md`

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Tuliskan identitas diri (Nama, Squad, Tanggal).
3. Lakukan pengujian di browsermu:
   - Akses produk yang valid (`/products/1`): salin judul produk dan harga yang tampil.
   - Akses produk dengan ID palsu (`/products/999`): salin pesan yang tampil di layar dan pastikan tombol link "Kembali ke Katalog Utama" berfungsi.
   - Buka tab Network pada saat mengakses `/products/999`, catat status HTTP yang diberikan oleh `json-server` (`404 Not Found`).
4. Jawab 2 pertanyaan pemahaman:
   - Mengapa kita memeriksa `if (error instanceof ApiError && error.status === 404)` secara spesifik di `ProductDetailPage.tsx`? Apa bahayanya jika kita hanya menampilkan `error.message` mentah kepada pembeli umum?
   - Mengapa kita wajib menyertakan `[id]` di dalam dependency array `useEffect` pada `ProductDetailPage.tsx`?
5. Ajukan Pull Request ke repositori squad.

### Contoh Format Hasil (`tugas_04b.md`)

```markdown
# Tugas Mandiri 04b — Slice 4: Halaman Detail Produk
Nama: Bagas Wicaksono
Squad: Squad 3
Tanggal: 20 November 2026

## 1. Hasil Pengujian Halaman Detail
- Pengujian ID Valid (`/products/1`):
  - Nama: Keripik Tempe Renyah 250g
  - Harga: Rp 18.000 (Stok: 45)
- Pengujian ID Tidak Ada (`/products/999`):
  - Pesan Tampilan: `Produk tidak ditemukan`
  - Tombol Kembali: Berfungsi kembali ke URL `/`
  - Status Network Tab: `404 Not Found` pada request `http://localhost:3001/products/999`

## 2. Jawaban Pertanyaan Pemahaman
1. Pesan error teknis bawaan seperti "Permintaan gagal dengan kode status 404" terdengar menyeramkan dan membingungkan bagi pembeli UMKM biasa yang tidak mengerti istilah pemrograman. Dengan mendeteksi `error.status === 404`, kita bisa mengubah pesan teknis tersebut menjadi kalimat bahasa Indonesia yang ramah dan menenangkan ("Produk tidak ditemukan") disertai tautan kembali yang jelas.
2. Karena jika pengguna bernavigasi antar produk langsung dari halaman detail (misalnya melalui daftar produk serupa), React tidak akan membongkar komponen dari DOM. Memasukkan `[id]` memastikan bahwa setiap kali nomor ID di URL berganti, `useEffect` langsung dipicu kembali untuk mengambil data produk yang baru dari server.
```

---

Lanjut ke: **04c-konsolidasi-dan-refactor.md**
