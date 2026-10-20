# 1.0b JSX & Komponen Bertipe — Menulis ProductCard Pertama

## Tujuan sesi ini

Menulis komponen React pertama untuk Katalog UMKM: `ProductCard` dan `ProductList`. Di sini peserta menggabungkan **JSX** (cara React menulis UI) dengan **TypeScript** (tipe data untuk props).

## Bacaan wajib sebelum sesi

- **Bab 1.2 — JSX & Rendering Elements** (modul React): JSX syntax, embedding expressions, conditional rendering, list rendering
- **Bab 1.3 — Components & Props** (modul React): functional component, props, destructuring, default props, children, composition
- **Bab 4.1 — Pengenalan TypeScript pada React** (modul React): cara pakai TS di komponen React

## Ringkasan konsep

### JSX — HTML di dalam JavaScript

JSX terlihat seperti HTML, tapi sebenarnya JavaScript. Perbedaan utama dengan HTML biasa:

| HTML | JSX |
|---|---|
| `class="..."` | `className="..."` |
| `for="..."` | `htmlFor="..."` |
| `style="color: red"` | `style={{ color: 'red' }}` |
| Atribut lowercase | Atribut camelCase (`onClick`, `tabIndex`) |

```tsx
// JSX — ini JavaScript, bukan HTML
const greeting = <h1>Halo, {name}!</h1>
```

Kurung kurawal `{}` di JSX = "ini ekspresi JavaScript". Bisa isi variabel, operasi matematika, pemanggilan fungsi — tapi **bukan** statement (`if`, `for`).

### Functional Component

Komponen di React = **fungsi yang mengembalikan JSX**:

```tsx
function Greeting() {
  return <h1>Halo!</h1>
}
```

Dipakai seperti tag HTML:

```tsx
<Greeting />
```

### Props — Data dari Luar

Props = argumen yang dikirim ke komponen. Di TypeScript, kita **menentukan tipenya**:

```tsx
interface GreetingProps {
  name: string
}

function Greeting({ name }: GreetingProps) {
  return <h1>Halo, {name}!</h1>
}

// Dipakai:
<Greeting name="Budi" />
```

Props bersifat **read-only** — komponen tidak boleh mengubah props yang diterimanya.

### Conditional Rendering

Dua pola yang paling sering:

```tsx
// Tampil atau tidak sama sekali
{isAdmin && <span>Admin</span>}

// Pilih salah satu dari dua
{stock > 0 ? `Stok: ${stock}` : 'Stok habis'}
```

### List Rendering

```tsx
{items.map((item) => (
  <li key={item.id}>{item.name}</li>
))}
```

**`key` wajib** — React butuh ini untuk melacak mana item yang berubah/ditambah/dihapus.

## Langkah: tulis komponen Katalog

### 1. Definisikan bentuk data `Product`

Ini sudah dibahas detail di modul Slice 0 (`01d-tipe-dasar-dan-list-rendering.md`). Sekarang yang penting adalah: kita punya `interface Product` dengan field seperti `id`, `name`, `price`, `stock`, dll.

### 2. Tulis `ProductCard`

```tsx
// src/components/ProductCard.tsx
import type { Product } from '../types/product'

interface ProductCardProps {
  product: Product
}

function ProductCard({ product }: ProductCardProps) {
  return (
    <article className="product-card">
      <h3>{product.name}</h3>
      <p>{product.description}</p>
      <p><strong>Rp {product.price.toLocaleString('id-ID')}</strong></p>
      <p>{product.stock > 0 ? `Stok: ${product.stock}` : 'Stok habis'}</p>
    </article>
  )
}

export default ProductCard
```

Perhatikan:
- `ProductCardProps` mendefinisikan **tipe props** — TypeScript akan menegur kalau kita lupa mengirim `product` atau salah tipenya
- **Props destructuring** (`{ product }`) — lebih ringkas dari `props.product`
- **Conditional rendering** dengan ternary untuk stok

### 3. Tulis `ProductList`

```tsx
// src/components/ProductList.tsx
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

Perhatikan:
- **Empty state** ditangani (`products.length === 0`)
- **`key={product.id}`** wajib untuk list rendering
- `ProductList` memakai `ProductCard` — ini **component composition** (komponen besar dibangun dari komponen kecil)

## Latihan

1. Tambahkan `children` props ke `ProductCard`: buat supaya bisa menerima konten tambahan di antara tag pembuka dan penutupnya (lihat bab 1.3 modul React, bagian Children Props).
2. Buat komponen `Badge` terpisah yang menerima props `text` dan `color`. Pakai di `ProductCard` untuk menampilkan status (`active`/`draft`).
3. Coba hapus `: ProductCardProps` dari parameter fungsi — apa yang terjadi? Apakah TypeScript masih menegur kalau kamu kirim props yang salah?

## Cek pemahaman

- Apa bedanya `className` di JSX dan `class` di HTML? Kenapa?
- Kenapa `key` harus unik dalam list? Apa yang bisa terjadi kalau kita pakai index array sebagai key?
- Apa bedanya `interface` dan `type` di TypeScript? (Jawaban singkat: untuk kasus kita, boleh ditukar — kita pakai `interface` untuk bentuk objek dan `type` untuk union, sebagai konvensi tim.)

## Kaitkan ke rujukan

- **Bab 1.2** modul React: JSX syntax lengkap, termasuk komentar di JSX, inline style, embedding expressions
- **Bab 1.3** modul React: semua tentang komponen, props, composition
- **Bab 4.1** modul React: cara pakai TypeScript di React secara lebih lengkap

---

Lanjut ke: **01c-styling-kartu-produk.md**
