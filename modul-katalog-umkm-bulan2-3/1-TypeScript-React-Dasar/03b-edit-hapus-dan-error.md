# 3.0b Slice 3 — Edit & Hapus Produk (PATCH, DELETE, & Error Handling)

> **Catatan Struktur Sesi (Dipecah 2 Hari Belajar):**  
> Unit Slice 3 ini dirancang untuk diselesaikan dalam **2 hari belajar** agar pemahaman murid mendalam dan tidak terburu-buru:  
> - **Hari 1 (Bagian 1):** Fitur Hapus Produk, Penanganan Status 204 No Content, Dialog Konfirmasi, dan Update Array via `.filter()`.  
> - **Hari 2 (Bagian 2):** Fitur Edit Produk Inline, State Lokal `isEditing`, Komponen Formulir `ProductEditForm`, dan Update Array via `.map()`.

---

## Tujuan Slice Ini

Menyelesaikan siklus **CRUD (Create, Read, Update, Delete)** secara utuh: pengguna dapat **mengedit** harga & stok produk secara langsung di kartu (*inline*), serta **menghapus** produk dengan aman disertai dialog konfirmasi dan pembaruan state tanpa refresh halaman.

---

## Aktivitas Terbimbing di Kelas (Blok 1, 10-15 Menit)

Mentor akan memandu demonstrasi konsep:
- **Hari 1:** Mengirimkan `DELETE` request dan memperbarui daftar state `products` menggunakan fungsi filter immutability.
- **Hari 2:** Mengapa mode edit (`isEditing`) harus berupa **state lokal di dalam masing-masing kartu `ProductCard`**, bukan diletakkan di halaman induk.
- Menangani form edit kecil (`ProductEditForm`) khusus untuk kolom yang sering berubah (harga dan stok).

*(Bahan bacaan pendalaman opsional: Modul React Bootcamp Bab 2.2 tentang Advanced List Rendering).*

---

## Ringkasan Konsep Kunci & Analogi

### 1. Di Mana State `isEditing` Seharusnya Berada?

> **Analogi Catatan Saku Kasir:**  
> Bayangkan ada 10 kasir yang masing-masing memegang kartu barang.  
> Jika kasir nomor 3 ingin mengoreksi harga barangnya (klik Edit), hanya kartu barang nomor 3 yang membuka kotak koreksi. Kasir 1, 2, 4, dst. tidak boleh ikut-ikutan membuka kotak edit!  
> Itulah sebabnya `const [isEditing, setIsEditing] = useState(false)` diletakkan **di dalam `ProductCard.tsx` (state lokal)**, bukan di halaman utama `ProductsPage.tsx`.

### 2. Memperbarui Array State Tanpa Fetch Ulang

Tinjau kembali dua jurus array JavaScript yang kita gunakan:

```tsx
// 1. MENGHAPUS: Buat array baru yang membuang barang dengan id target (.filter)
setProducts((current) => current.filter((product) => product.id !== targetId))

// 2. MENGEDIT: Buat array baru yang mengganti barang ber-id target dengan data baru (.map)
setProducts((current) =>
  current.map((product) => (product.id === targetId ? updatedProduct : product))
)
```

---

## Bagian 1 (Hari 1): Implementasi Fitur Hapus Produk

### Langkah 1: Tambahkan Handler Hapus di `ProductsPage.tsx`

Buka `src/pages/ProductsPage.tsx`. Tambahkan fungsi pemanggil API hapus dan teruskan ke komponen `ProductList`:

```tsx
// src/pages/ProductsPage.tsx
import { createProduct, deleteProduct, getProducts, updateProduct } from '../api/products'
import type { UpdateProductInput } from '../api/products'

// ...di dalam fungsi komponen ProductsPage:

async function handleDeleteProduct(id: number) {
  try {
    // 1. Panggil server untuk menghapus di database json-server
    await deleteProduct(id)
    // 2. Buang produk dari daftar state lokal
    setProducts((current) => current.filter((product) => product.id !== id))
  } catch (error) {
    alert(error instanceof Error ? error.message : 'Gagal menghapus produk')
  }
}
```

---

### Langkah 2: Teruskan Handler Lewat `ProductList.tsx`

Buka `src/components/ProductList.tsx`:

```tsx
// src/components/ProductList.tsx
import type { Product } from '../types/product'
import type { UpdateProductInput } from '../api/products'
import ProductCard from './ProductCard'

interface ProductListProps {
  products: Product[]
  onDelete: (id: number) => Promise<void>
  onSave: (id: number, input: UpdateProductInput) => Promise<void>
}

function ProductList({ products, onDelete, onSave }: ProductListProps) {
  if (products.length === 0) {
    return <p className="empty-message">Belum ada produk untuk ditampilkan.</p>
  }

  return (
    <div className="product-list">
      {products.map((product) => (
        <ProductCard
          key={product.id}
          product={product}
          onDelete={onDelete}
          onSave={onSave}
        />
      ))}
    </div>
  )
}

export default ProductList
```

---

## Bagian 2 (Hari 2): Implementasi Fitur Edit Produk Inline

### Langkah 3: Buat Formulir Edit Ringkas (`ProductEditForm.tsx`)

Buat berkas `src/components/ProductEditForm.tsx`:

```tsx
// src/components/ProductEditForm.tsx
import { useState } from 'react'
import type { FormEvent } from 'react'
import type { Product } from '../types/product'
import type { UpdateProductInput } from '../api/products'

interface ProductEditFormProps {
  product: Product
  onSave: (input: UpdateProductInput) => Promise<void>
  onCancel: () => void
}

function ProductEditForm({ product, onSave, onCancel }: ProductEditFormProps) {
  const [price, setPrice] = useState<string>(String(product.price))
  const [stock, setStock] = useState<string>(String(product.stock))
  const [isSubmitting, setIsSubmitting] = useState<boolean>(false)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)

  async function handleSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault()
    setIsSubmitting(true)
    setErrorMessage(null)

    try {
      // Kirim hanya field yang diedit (PATCH)
      await onSave({
        price: Number(price),
        stock: Number(stock),
      })
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : 'Gagal menyimpan perubahan')
    } finally {
      setIsSubmitting(false)
    }
  }

  return (
    <form className="product-edit-form" onSubmit={handleSubmit}>
      <h4>Edit Harga & Stok</h4>

      <div>
        <label>
          Harga (Rp):
          <input
            type="number"
            min="0"
            value={price}
            onChange={(e) => setPrice(e.target.value)}
            required
          />
        </label>
      </div>

      <div>
        <label>
          Stok:
          <input
            type="number"
            min="0"
            value={stock}
            onChange={(e) => setStock(e.target.value)}
            required
          />
        </label>
      </div>

      {errorMessage && <p role="alert" style={{ color: 'red' }}>{errorMessage}</p>}

      <div style={{ display: 'flex', gap: '8px', marginTop: '12px' }}>
        <button type="submit" disabled={isSubmitting}>
          {isSubmitting ? 'Menyimpan...' : 'Simpan'}
        </button>
        <button type="button" onClick={onCancel} disabled={isSubmitting}>
          Batal
        </button>
      </div>
    </form>
  )
}

export default ProductEditForm
```

---

### Langkah 4: Pasang Mode Edit & Tombol di `ProductCard.tsx`

Buka `src/components/ProductCard.tsx`. Perhatikan bagian `// TODO:` dan lengkapi kodenya:

```tsx
// src/components/ProductCard.tsx
import { useState } from 'react'
import type { Product } from '../types/product'
import type { UpdateProductInput } from '../api/products'
import { formatRupiah } from '../utils/format'
import ProductEditForm from './ProductEditForm'

interface ProductCardProps {
  product: Product
  onDelete: (id: number) => Promise<void>
  onSave: (id: number, input: UpdateProductInput) => Promise<void>
}

function ProductCard({ product, onDelete, onSave }: ProductCardProps) {
  // State lokal untuk menentukan apakah kartu ini sedang dalam mode edit
  const [isEditing, setIsEditing] = useState<boolean>(false)
  const isOutOfStock = product.stock === 0

  async function handleDeleteClick() {
    // Dialog konfirmasi bawaan browser untuk mencegah salah pencet
    const isConfirmed = window.confirm(`Apakah Anda yakin ingin menghapus "${product.name}"?`)
    if (isConfirmed) {
      await onDelete(product.id)
    }
  }

  // JIKA SEDANG DALAM MODE EDIT: Tampilkan formulir edit
  if (isEditing) {
    return (
      <article className="product-card">
        <h3>{product.name}</h3>
        <ProductEditForm
          product={product}
          onCancel={() => setIsEditing(false)}
          onSave={async (input) => {
            // TODO 1: Panggil prop onSave dengan mengirimkan product.id dan input baru
            await onSave(product.id, input)
            // Tutup kembali mode edit setelah berhasil
            setIsEditing(false)
          }}
        />
      </article>
    )
  }

  // TAMPILAN NORMAL KARTU
  return (
    <article className="product-card">
      <h3>{product.name}</h3>
      {product.status === 'draft' && <span className="badge">Draft</span>}
      <p>{product.description}</p>
      <p>
        <strong>{formatRupiah(product.price)}</strong>
      </p>
      <p className={isOutOfStock ? 'stock-warning' : ''}>
        {isOutOfStock ? 'Stok habis' : `Stok: ${product.stock}`}
      </p>
      <p>
        <small>UMKM: {product.merchant_name}</small>
      </p>

      {/* Tombol Aksi Edit & Hapus */}
      <div style={{ display: 'flex', gap: '8px', marginTop: '12px' }}>
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

---

### Langkah 5: Sambungkan `handleSaveProduct` di `ProductsPage.tsx`

Buka `src/pages/ProductsPage.tsx` dan lengkapi fungsi simpan:

```tsx
// src/pages/ProductsPage.tsx
async function handleSaveProduct(id: number, input: UpdateProductInput) {
  // 1. Kirim perubahan PATCH ke server
  const updatedProduct = await updateProduct(id, input)
  
  // 2. Perbarui state lokal menggunakan jurus .map()
  setProducts((current) =>
    current.map((product) => (product.id === id ? updatedProduct : product))
  )
}

// ...di JSX render ProductList:
<ProductList
  products={products}
  onDelete={handleDeleteProduct}
  onSave={handleSaveProduct}
/>
```

---

## Analisis Bug & Prediksi (Aktivitas Blok 2)

Diskusikan bersama rekan pairing:

1. **Prediksi Bug Salah Taruh State:**  
   Jika seorang murid meletakkan `const [isEditing, setIsEditing] = useState(false)` di dalam komponen `ProductsPage.tsx` dan mengoper nilai `isEditing` tersebut ke semua kartu, apa yang terjadi di layar saat pengguna mengeklik tombol "Edit" di kartu nomor 1?  
   *(Jelaskan mengapa tampilan aplikasi langsung kacau!).*
2. **Uji Konfirmasi Pembatalan Hapus:**  
   Klik tombol "Hapus" pada salah satu produk. Ketika dialog pop-up konfirmasi muncul, klik tombol **Cancel/Batal**. Pastikan produk tidak terhapus baik di layar maupun di server.

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan secara mandiri di kelas. Simpan hasilnya di:  
`tugas/squad-<nomor>/<nama-kamu>/tugas_03b.md`

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Tuliskan identitas diri (Nama, Squad, Tanggal).
3. Lakukan aksi nyata pada aplikasi di browsermu:
   - Pilih salah satu produk UMKM, klik tombol "Edit".
   - Ubah harga menjadi `32000` dan stok menjadi `8`.
   - Klik "Simpan". Periksa tab Network browser: catat Request Method (`PATCH`) dan URL tujuannya (contoh: `http://localhost:3001/products/3`).
   - Buka `db.json` di VS Code dan pastikan nilainya sudah benar-benar berganti permanen.
4. Jawab 2 pertanyaan pemahaman:
   - Mengapa kita menggunakan metode JavaScript `.filter()` untuk operasi hapus data dan `.map()` untuk operasi edit data di state React?
   - Mengapa meletakkan state `isEditing` di dalam `ProductCard.tsx` menjamin isolasi antarmuka yang bersih antar produk?
5. Ajukan Pull Request ke repositori squad.

### Contoh Format Hasil (`tugas_03b.md`)

```markdown
# Tugas Mandiri 03b — Slice 3: Edit & Hapus Produk
Nama: Wahyu Hidayat
Squad: Squad 5
Tanggal: 17 November 2026

## 1. Verifikasi Aksi PATCH di Network Tab
- Request URL: `http://localhost:3001/products/2`
- Request Method: `PATCH`
- Status Code: `200 OK`
- Request Payload:
```json
{
  "price": 32000,
  "stock": 8
}
```

Hasil terverifikasi di `db.json` pada produk ID 2: harga berubah menjadi 32000 dan stok menjadi 8.

## 2. Jawaban Pertanyaan Pemahaman
1. Metode `.filter()` menghasilkan array baru yang hanya meloloskan item yang lolos kriteria (semua produk kecuali yang id-nya cocok dengan yang dihapus). Sedangkan `.map()` menghasilkan array baru berukuran sama dengan menyisipkan satu objek produk hasil edit pada id yang cocok. Kedua metode ini menjaga prinsip *immutability* karena tidak memutasi array asli.
2. Karena setiap instance komponen `ProductCard` memiliki memori state independen masing-masing. Dengan meletakkan `isEditing` di level kartu, mengaktifkan mode edit pada kartu A tidak akan memengaruhi nilai state kartu B, C, atau D.
```

---

Lanjut ke: **03c-state-management-patterns.md**
