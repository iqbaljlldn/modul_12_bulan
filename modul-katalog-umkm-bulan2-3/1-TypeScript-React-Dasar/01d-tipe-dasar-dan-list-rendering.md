# 1.0d Slice 0 — Katalog Tampil (Tipe Dasar & List Rendering)

## Tujuan Slice Ini

Menampilkan daftar produk UMKM di halaman web dalam bentuk kartu-kartu rapi. Pada slice perdana ini, data produk masih bersifat **statis (hardcode)** dari file lokal. Ini sengaja dilakukan agar kamu fokus memahami **kontrak tipe TypeScript** dan **cara React merender daftar data** sebelum berurusan dengan server.

---

## Aktivitas Terbimbing di Kelas (Blok 1, 10-15 Menit)

Mentor akan memandu pembahasan:
- Cara merancang `interface` TypeScript untuk data produk UMKM.
- Perbedaan `interface` (bentuk objek) dan `type` (union pilihan tetap).
- Mengapa data backend menggunakan format `snake_case` (seperti `category_id`, `merchant_name`).
- Menggunakan fungsi bawaan JavaScript `Intl.NumberFormat` untuk mata uang Rupiah.

*(Bahan bacaan pendalaman opsional: Modul React Bootcamp Bab 4.1 tentang Dasar TypeScript pada React).*

---

## Ringkasan Konsep Kunci & Analogi

### 1. Apa itu TypeScript Interface?

> **Analogi Sehari-hari:**  
> Pikirkan `interface` seperti **formulir pendaftaran resmi dengan kolom bergaris tegas**:
> - Kolom *Nama*: wajib diisi huruf (string).
> - Kolom *Harga*: wajib diisi angka (number).
> - Kolom *Status*: hanya boleh dicentang salah satu: "Aktif" atau "Draft".  
> Jika seorang staf salah memasukkan teks "Murah Sekali" di kolom harga, petugas pemeriksa dokumen (**compiler TypeScript**) langsung menegur saat itu juga di ruang kerja (editor kodemu), sebelum dokumen itu sempat disebarkan ke publik (browser pengguna).

---

## Langkah demi Langkah Mengembangkan Slice 0

### Langkah 1: Definisikan Bentuk Data Produk

Buka berkas `src/types/product.ts` dan pastikan kontrak tipe produk tersusun rapi:

```ts
// src/types/product.ts

// Union type: status hanya boleh salah satu dari dua kata ini persis
export type ProductStatus = 'active' | 'draft'

// Interface: mendeskripsikan bentuk lengkap data satu produk
export interface Product {
  id: number
  name: string
  description: string
  price: number
  stock: number
  status: ProductStatus
  category_id: number
  merchant_name: string
  created_at: string
}
```

> **Catatan Penamaan Field:** Nama `category_id` dan `merchant_name` menggunakan `snake_case` karena menyesuaikan kesepakatan format data API backend (kontrak API).

---

### Langkah 2: Siapkan Data Contoh Statis (Sementara)

Buat berkas `src/data/products.ts`. Data ini menjadi jembatan sementara untuk Slice 0 dan nantinya akan diganti oleh panggilan API di Slice 1:

```ts
// src/data/products.ts
import type { Product } from '../types/product'

export const products: Product[] = [
  {
    id: 1,
    name: 'Keripik Tempe Renyah 250g',
    description: 'Keripik tempe kedelai lokal tanpa bahan pengawet.',
    price: 18000,
    stock: 45,
    status: 'active',
    category_id: 1,
    merchant_name: 'Dapur Bu Sri',
    created_at: '2026-01-15T08:00:00Z',
  },
  {
    id: 2,
    name: 'Sambal Roa Khas Manado 150g',
    description: 'Sambal ikan roa asap pedas gurih aroma khas.',
    price: 35000,
    stock: 0, // Stok habis untuk menguji tampilan conditional rendering
    status: 'active',
    category_id: 1,
    merchant_name: 'Warung Bu Ani',
    created_at: '2026-01-16T09:30:00Z',
  },
  {
    id: 3,
    name: 'Kopi Bubuk Robusta Dampit 200g',
    description: 'Biji kopi pilihan roasted medium dark khas Malang.',
    price: 28000,
    stock: 20,
    status: 'draft',
    category_id: 2,
    merchant_name: 'Kopi Sejahtera',
    created_at: '2026-01-17T11:00:00Z',
  },
]
```

---

### Langkah 3: Membuat Helper Format Mata Uang

Buat berkas `src/utils/format.ts`:

```ts
// src/utils/format.ts

// Mengubah angka 18000 menjadi format standar "Rp 18.000"
export function formatRupiah(amount: number): string {
  return new Intl.NumberFormat('id-ID', {
    style: 'currency',
    currency: 'IDR',
    maximumFractionDigits: 0,
  }).format(amount)
}
```

---

### Langkah 4: Rangkai Komponen `ProductCard.tsx`

Buka `src/components/ProductCard.tsx`:

```tsx
// src/components/ProductCard.tsx
import type { Product } from '../types/product'
import { formatRupiah } from '../utils/format'

interface ProductCardProps {
  product: Product
}

function ProductCard({ product }: ProductCardProps) {
  const isOutOfStock = product.stock === 0

  return (
    <article className="product-card">
      <h3>{product.name}</h3>
      {product.status === 'draft' && <span className="badge">Draft</span>}
      <p>{product.description}</p>
      
      {/* Tampilkan harga terformat */}
      <p>
        <strong>{formatRupiah(product.price)}</strong>
      </p>

      {/* TODO: Terapkan dynamic class dan teks stok bersyarat */}
      <p className={isOutOfStock ? 'stock-warning' : ''}>
        {isOutOfStock ? 'Stok habis' : `Stok: ${product.stock}`}
      </p>

      <p>
        <small>UMKM: {product.merchant_name}</small>
      </p>
    </article>
  )
}

export default ProductCard
```

---

### Langkah 5: Rangkai di `App.tsx`

Buka `src/App.tsx` dan hubungkan data dengan komponen:

```tsx
// src/App.tsx
import ProductList from './components/ProductList'
import { products } from './data/products'

function App() {
  return (
    <main style={{ maxWidth: '1000px', margin: '0 auto', padding: '24px 16px' }}>
      <header>
        <h1>Mini Katalog UMKM</h1>
        <p>Menampilkan {products.length} produk pilihan lokal</p>
      </header>

      {/* TODO: Render komponen ProductList dan kirimkan data products lewat props */}
      <ProductList products={products} />
    </main>
  )
}

export default App
```

---

## Analisis Bug & Prediksi (Aktivitas Blok 2)

Diskusikan bersama pasangan pairing:

1. **Prediksi Error TypeScript:**  
   Jika kamu sengaja menambahkan data baru di `products.ts` dengan status `'tersedia'` (bahasa Indonesia):
   ```ts
   status: 'tersedia'
   ```
   Tebak pesan error apa yang akan dimunculkan oleh compiler TypeScript di editor kodemu! Mengapa hal itu terjadi?
2. **Uji Coba Linter:**  
   Buka terminal dan jalankan `npm run lint`. Apakah ada peringatan impor yang tidak terpakai atau kesalahan format penulisan?

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan secara mandiri di kelas. Simpan hasilnya di:  
`tugas/squad-<nomor>/<nama-kamu>/tugas_01d.md`

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Tuliskan identitas diri (Nama, Squad, Tanggal).
3. Bayangkan produk UMKM membutuhkan satu informasi tambahan: nomor kode barang unik / SKU (*Stock Keeping Unit*), contoh: `"KRP-001"`.
   - Perbarui definisi `interface Product` di berkas tugasmu dengan menambahkan kolom `sku: string`.
   - Tunjukkan bagaimana baris JSX di `ProductCard.tsx` untuk menampilkan teks kode SKU tersebut di bawah nama produk (misalnya: `<small className="product-sku">SKU: {product.sku}</small>`).
4. Jawab 2 pertanyaan pemahaman:
   - Jika kita tidak sengaja menghapus atribut `key={product.id}` pada saat melakukan `.map()` di `ProductList.tsx`, apakah aplikasi langsung mati total (layar putih) atau tetap tampil dengan peringatan? Di mana peringatan itu bisa dilihat?
   - Mengapa kita meletakkan fungsi `formatRupiah` di folder `src/utils/` dan bukan menulisnya langsung berulang-ulang di dalam setiap komponen kartu?
5. Commit hasil kerjamu dan ajukan Pull Request ke repositori squad.

### Contoh Format Hasil (`tugas_01d.md`)

```markdown
# Tugas Mandiri 01d — Slice 0: List Rendering
Nama: Muhammad Farhan
Squad: Squad 4
Tanggal: 6 November 2026

## 1. Modifikasi Tipe Data Produk
```ts
export interface Product {
  id: number
  sku: string // Kolom tambahan kode unik barang
  name: string
  description: string
  price: number
  stock: number
  status: ProductStatus
  category_id: number
  merchant_name: string
  created_at: string
}
```

## 2. Penambahan Tampilan di ProductCard
```tsx
<p className="product-sku">
  <small>Kode SKU: {product.sku}</small>
</p>
```

## 3. Jawaban Pertanyaan
1. Aplikasi tidak langsung mati layar putih, kartu-kartu produk tetap muncul di halaman. Namun, browser console (F12) akan memunculkan pesan peringatan merah (*Warning: Each child in a list should have a unique "key" prop*).
2. Memisahkan fungsi ke `src/utils/format.ts` menerapkan prinsip *Don't Repeat Yourself (DRY)*. Fungsi tersebut dapat digunakan ulang di halaman lain (seperti halaman detail dan form keranjang) tanpa perlu menduplikasi kode logika yang sama.
```

---

Lanjut ke: **02a-state-dan-usestate.md** (Minggu 2)
