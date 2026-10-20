# 1.0d Slice 0 — Katalog Tampil (Tipe Dasar & List Rendering)

## Tujuan slice ini

Menampilkan daftar produk UMKM di halaman, sebagai kartu-kartu. Datanya masih **hardcode** (ditulis langsung di kode) — belum dari server. Itu boleh, karena tujuan slice ini adalah paham TypeScript dasar dan komponen React, bukan soal data asli dulu.

> **Prasyarat:** kamu sudah membaca dan menjalankan langkah di `01a` (orientasi), `01b` (JSX & komponen bertipe), dan `01c` (styling). Kalau belum, kerjakan dulu — slice ini membangun di atas semua itu.

## Bacaan wajib (modul React bootcamp)

Kalau belum dibaca dari sesi sebelumnya, baca sekarang:
- **Bab 1.2** — JSX & Rendering Elements (conditional rendering, list rendering dengan `map` + `key`)
- **Bab 1.3** — Components & Props (component composition)
- **Bab 4.1** — Pengenalan TypeScript pada React

## Kenapa ini penting untuk produk

Sebelum bisa menyambungkan ke database atau API, kita harus tahu **bentuk data** yang kita kerjakan. Slice ini melatih itu: mendefinisikan bentuk `Product`, lalu menampilkannya.

## Konsep yang dipakai

- **Tipe dasar TypeScript:** `string`, `number`, array (`Product[]`)
- **`interface`** untuk mendeskripsikan bentuk objek
- **Union type** / **literal type**: `'active' | 'draft'`
- **Komponen React** dengan **props bertipe**
- **List rendering**: `.map()` + `key`
- **Conditional rendering**: tampilan berbeda kalau kondisi tertentu (misal stok habis)

## Langkah demi langkah

### 1. Definisikan bentuk data `Product`

Buat `src/types/product.ts`:

```ts
export type ProductStatus = 'active' | 'draft'

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

**Kenapa `type` untuk `ProductStatus` tapi `interface` untuk `Product`?** Aturan sederhana yang kita pakai di modul ini: `interface` untuk bentuk objek, `type` untuk union/literal seperti `ProductStatus`. Dua-duanya sebenarnya bisa dipakai bergantian untuk banyak kasus — ini soal konsistensi tim, bukan aturan mutlak TypeScript.

**Kenapa `category_id`, bukan `categoryId`?** Karena ini bentuk data yang datang dari API/database nanti, dan tribe sudah sepakat field data pakai `snake_case` (lihat `docs/kontrak-api.md` dan konvensi di kurikulum Bagian 14.2). Variabel biasa di kode tetap `camelCase` — bedanya akan lebih jelas di slice-slice berikutnya.

### 2. Siapkan data contoh (sementara, hardcode)

Buat `src/data/products.ts`. Isi beberapa produk contoh sesuai tipe `Product` di atas (boleh contek dari `db.seed.json` kalau mau data yang sama). Ingat: file ini sementara — akan **dihapus** di Slice 1 saat data pindah ke API.

```ts
import type { Product } from '../types/product'

// Data sementara (hardcode) untuk Slice 0. Akan diganti data dari API di Slice 1.
export const products: Product[] = [
  {
    id: 1,
    name: 'Keripik Tempe Original',
    description: 'Keripik tempe renyah tanpa pengawet, kemasan 250 gram.',
    price: 18000,
    stock: 120,
    status: 'active',
    category_id: 1,
    merchant_name: 'Dapur Bu Sari',
    created_at: '2026-01-12T08:00:00Z',
  },
  // ...tambah beberapa lagi
]
```

### 3. Bikin fungsi bantu untuk format harga

Buat `src/utils/format.ts`:

```ts
export function formatRupiah(amount: number): string {
  return new Intl.NumberFormat('id-ID', {
    style: 'currency',
    currency: 'IDR',
    maximumFractionDigits: 0,
  }).format(amount)
}
```

`Intl.NumberFormat` adalah fitur bawaan JavaScript (bukan library tambahan) untuk format angka/mata uang sesuai lokal (`id-ID` = Indonesia).

### 4. Bikin komponen `ProductCard`

Buat `src/components/ProductCard.tsx`:

```tsx
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
      <p>
        <strong>{formatRupiah(product.price)}</strong>
      </p>
      <p>{isOutOfStock ? 'Stok habis' : `Stok: ${product.stock}`}</p>
      <p>
        <small>{product.merchant_name}</small>
      </p>
    </article>
  )
}

export default ProductCard
```

Perhatikan dua bentuk conditional rendering yang berbeda:
- `{product.status === 'draft' && <span>...</span>}` → tampil **atau tidak sama sekali**.
- `{isOutOfStock ? '...' : '...'}` → tampil **salah satu dari dua pilihan**.

### 5. Bikin komponen `ProductList`

Buat `src/components/ProductList.tsx`:

```tsx
import type { Product } from '../types/product'
import ProductCard from './ProductCard'

interface ProductListProps {
  products: Product[]
}

function ProductList({ products }: ProductListProps) {
  if (products.length === 0) {
    return <p>Belum ada produk.</p>
  }

  return (
    <div className="product-list">
      {products.map((product) => (
        <ProductCard key={product.id} product={product} />
      ))}
    </div>
  )
}

export default ProductList
```

**`key={product.id}` wajib.** React butuh cara mengenali tiap item dalam list supaya tahu mana yang berubah. Jangan pakai index array (`key={index}`) kalau list-nya bisa berubah urutan/isi — kita sudah punya `id` yang lebih aman.

Perhatikan juga **empty state**: kalau `products.length === 0`, kita tampilkan pesan, bukan halaman kosong tanpa penjelasan. Ini kebiasaan kecil yang penting dijaga terus.

### 6. Pasang di `App.tsx`

```tsx
import ProductList from './components/ProductList'
import { products } from './data/products'

function App() {
  return (
    <main>
      <h1>Katalog UMKM</h1>
      <p>Menampilkan {products.length} produk</p>
      <ProductList products={products} />
    </main>
  )
}

export default App
```

### 7. Cek hasilnya

```bash
npm run dev
```

Buka `localhost:5173` — harus muncul kartu-kartu produk.

## Latihan

1. Tambahkan field baru di `Product`, misal `sku: string`, lalu tampilkan di kartu. Perhatikan: TypeScript akan menegur di semua tempat yang butuh disesuaikan.
2. Ubah `ProductCard` supaya kartu produk dengan status `'draft'` punya warna latar sedikit berbeda (CSS sederhana).
3. Coba hapus `key={product.id}` sengaja, jalankan `npm run dev`, lihat peringatan apa yang muncul di console browser.

## Cek pemahaman

- Kalau `product.stock` berubah dari `number` jadi `string` di salah satu data, apa yang akan ditegur TypeScript, dan di mana?
- Apa bedanya `interface ProductCardProps` di sini dengan `interface Product` di `types/product.ts`? Kenapa dipisah?

## Kesalahan umum

| Gejala | Sebab | Solusi |
|---|---|---|
| `Type 'string' is not assignable to type 'ProductStatus'` | Menulis status selain `'active'`/`'draft'` (misal `'aktif'`) | Cocokkan persis dengan union type yang didefinisikan |
| Error `Cannot find module './types/product'` | Salah path import, atau lupa `import type` | `verbatimModuleSyntax` di starter mewajibkan `import type` untuk yang hanya dipakai sebagai tipe |
| Kartu tidak tampil sama sekali, tidak ada error | `products` array kosong, atau lupa render `<ProductList products={products} />` | Cek `console.log(products)` sementara di `App.tsx` |

## Kaitkan ke rujukan

Kalau masih ragu soal dasar komponen/props/JSX, buka bab **Pengenalan React** di modul React bootcamp sebagai penyegar.

---

Lanjut ke: **02-fetch-dan-loading-state.md** (Slice 1)
