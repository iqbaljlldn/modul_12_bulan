# 1.0b JSX & Komponen Bertipe — Menulis ProductCard Pertama

## Tujuan Sesi Ini

Menulis komponen React pertama untuk Katalog UMKM: `ProductCard` dan `ProductList`. Di sini kamu menggabungkan **JSX** (cara React mendeskripsikan tampilan visual) dengan **TypeScript** (tipe data yang menjaga ketepatan props antarkomponen).

---

## Aktivitas Terbimbing di Kelas (Blok 1, 10-15 Menit)

Mentor akan memandu pembahasan konsep dasar berikut:
- Mengapa JSX terlihat seperti HTML padahal sebenarnya adalah JavaScript murni.
- Aturan penulisan atribut di JSX (`className`, `htmlFor`, kurung kurawal `{}`).
- Menulis *Functional Component* yang menerima argumen data melalui *Props*.
- Mendefinisikan kontrak tipe props menggunakan `interface` sederhana.

*(Bahan bacaan pendalaman opsional: Modul React Bootcamp Bab 1.2 tentang JSX dan Bab 1.3 tentang Komponen & Props).*

---

## Ringkasan Konsep Kunci & Analogi

### 1. Apa itu Komponen dan Props?

> **Analogi Sehari-hari:**  
> Pikirkan komponen seperti **cetakan kartu identitas (KTP)**. Cetakan ini menentukan letak foto, letak nama, dan bingkai kartu.  
> **Props** adalah data asli orangnya (Nama: "Siti", Alamat: "Bandung") yang dimasukkan ke cetakan tersebut. Satu cetakan kartu bisa dipakai untuk mencetak ribuan kartu identitas warga yang berbeda-beda tanpa mengubah bingkainya.  
> Props bersifat **read-only** (hanya dibaca) — cetakan kartu tidak boleh mengubah nama pemilik kartu seenaknya.

### 2. Sintaks JSX vs HTML Standar

Karena JSX adalah ekspresi JavaScript, ada beberapa kata kunci HTML yang disesuaikan:

| HTML Biasa | JSX di React | Alasan |
|---|---|---|
| `class="kartu"` | `className="kartu"` | `class` adalah kata kunci bawaan JavaScript (*reserved keyword*). |
| `for="nama"` | `htmlFor="nama"` | `for` adalah kata kunci bawaan JavaScript (untuk perulangan). |
| `onclick="klik()"` | `onClick={handleClick}` | Menggunakan camelCase dan langsung mengoper fungsi, bukan teks string. |
| Teks statis biasa | `{ekspresiJavaScript}` | Kurung kurawal `{}` adalah "jendela" untuk mengeksekusi variabel atau operasi JS. |

---

## Langkah demi Langkah: Menulis Komponen Katalog

### Langkah 1: Siapkan Tipe Data Produk Sederhana

Untuk sesi awal ini, kita cukup menggunakan bentuk tipe data yang jelas dan sederhana di `src/types/product.ts`:

```ts
// src/types/product.ts
export type ProductStatus = 'active' | 'draft'

export interface Product {
  id: number
  name: string
  description: string
  price: number
  stock: number
  status: ProductStatus
  merchant_name: string
}
```

> Kita memakai `interface` untuk mendeskripsikan bentuk objek (`Product`), dan `type` untuk union pilihan nilai terbatas (`'active' | 'draft'`).

---

### Langkah 2: Lengkapi Komponen `ProductCard`

Buka atau buat berkas `src/components/ProductCard.tsx`. Jangan langsung menyalin! Perhatikan bagian `// TODO:` dan lengkapi logika conditional rendering untuk stok:

```tsx
// src/components/ProductCard.tsx
import type { Product } from '../types/product'

interface ProductCardProps {
  product: Product
}

function ProductCard({ product }: ProductCardProps) {
  // TODO 1: Tentukan apakah produk kehabisan stok (true jika stock === 0)
  const isOutOfStock = product.stock === 0

  return (
    <article className="product-card">
      <h3>{product.name}</h3>

      {/* Tampilkan badge draft HANYA jika status produk bernilai 'draft' */}
      {product.status === 'draft' && <span className="badge">Draft</span>}

      <p>{product.description}</p>
      
      <p>
        <strong>Rp {product.price.toLocaleString('id-ID')}</strong>
      </p>

      {/* TODO 2: Gunakan ternary operator: jika isOutOfStock bernilai true,
          tampilkan teks 'Stok habis', selain itu tampilkan `Stok: ${product.stock}` */}
      <p>{isOutOfStock ? 'Stok habis' : `Stok: ${product.stock}`}</p>

      <p>
        <small>UMKM: {product.merchant_name}</small>
      </p>
    </article>
  )
}

export default ProductCard
```

---

### Langkah 3: Membuat Komponen Pembungkus `ProductList`

Buat berkas `src/components/ProductList.tsx`:

```tsx
// src/components/ProductList.tsx
import type { Product } from '../types/product'
import ProductCard from './ProductCard'

interface ProductListProps {
  products: Product[]
}

function ProductList({ products }: ProductListProps) {
  // 1. Tangani kondisi jika daftar produk kosong (Empty State)
  if (products.length === 0) {
    return <p className="empty-message">Belum ada produk untuk ditampilkan.</p>
  }

  // 2. Lakukan perulangan list rendering dengan .map()
  return (
    <div className="product-list">
      {products.map((product) => (
        // ATURAN PENTING: Atribut 'key' wajib ada dan harus unik!
        <ProductCard key={product.id} product={product} />
      ))}
    </div>
  )
}

export default ProductList
```

---

## Analisis Bug & Prediksi (Aktivitas Blok 2)

Diskusikan bersama pasangan pairing:

1. **Temukan Bug:**  
   Perhatikan potongan JSX berikut:
   ```tsx
   <div class="card">
     <h1>{product.name}</h1>
     <p style="color: red">Diskon!</p>
   </div>
   ```
   Sebutkan dua kesalahan sintaks JSX pada kode di atas dan perbaiki agar valid di React!
2. **Prediksi Output TypeScript:**  
   Jika di berkas pemanggil kamu menulis `<ProductCard product={{ id: 1, name: 'Kopi' }} />`, pesan error apa yang akan diberikan compiler TypeScript?

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan secara mandiri di kelas. Simpan hasilnya di:  
`tugas/squad-<nomor>/<nama-kamu>/tugas_01b.md`

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Buat komponen baru bernama `ProductBadge.tsx` sederhana di dalam pikiranmu atau catatan kode. Komponen ini menerima dua props bertipe:
   - `text`: bertipe `string`
   - `isDanger`: bertipe `boolean` (opsional, nilai bawaan `false`)
3. Tuliskan kode komponen `ProductBadge` tersebut di dokumen markdown tugas.
4. Jawab 2 pertanyaan singkat:
   - Mengapa kita wajib menyertakan atribut `key={product.id}` saat menggunakan `.map()` di React? Apa risikonya jika kita menggunakan indeks array (`key={index}`)?
   - Apa yang dimaksud dengan sifat props yang *read-only*? Mengapa komponen `ProductCard` dilarang mengubah langsung `product.price = 5000` di dalam bodinya?
5. Commit berkas jawaban dan buat PR ke repository squad.

### Contoh Format Hasil (`tugas_01b.md`)

```markdown
# Tugas Mandiri 01b — JSX & Komponen Bertipe
Nama: Siti Aisyah
Squad: Squad 3
Tanggal: 4 November 2026

## Kode Komponen ProductBadge
```tsx
interface ProductBadgeProps {
  text: string
  isDanger?: boolean
}

function ProductBadge({ text, isDanger = false }: ProductBadgeProps) {
  return (
    <span className={`badge ${isDanger ? 'badge-danger' : 'badge-default'}`}>
      {text}
    </span>
  )
}

export default ProductBadge
```

## Jawaban Pertanyaan
1. Atribut `key` adalah pengenal unik bagi React untuk melacak item mana yang ditambah, dihapus, atau diubah urutannya. Jika menggunakan indeks array (`key={index}`), saat data diurutkan ulang atau disaring, React bisa keliru merender state elemen dan menyebabkan bug tampilan.
2. Sifat *read-only* berarti komponen anak hanya bertugas menampilkan data yang dikirimkan induknya tanpa hak mengubah sumber aslinya. Jika komponen anak mengubah nilai props langsung, alur data menjadi tidak terduga dan merusak prinsip alur data satu arah (*one-way data flow*).
```

---

Lanjut ke: **01c-styling-kartu-produk.md**
