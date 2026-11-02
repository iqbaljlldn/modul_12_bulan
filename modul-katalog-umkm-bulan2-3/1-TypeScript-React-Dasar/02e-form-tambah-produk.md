# 2.0e Slice 2 — Tambah Produk (Form & HTTP POST)

## Tujuan Slice Ini

Menambahkan formulir interaktif di aplikasi agar pemilik UMKM dapat **menambahkan produk baru** ke katalog. Data yang diisi akan dikirimkan ke mock API server lewat metode **HTTP POST**, tersimpan permanen di `db.json`, dan langsung muncul di daftar kartu tanpa perlu me-reload halaman browser.

---

## Aktivitas Terbimbing di Kelas (Blok 1, 10-15 Menit)

Mentor akan memandu demonstrasi konsep:
- Memahami metode **HTTP POST** untuk membuat data baru di server.
- Kontrak tipe data input: mendefinisikan apa saja yang diisi pengguna vs apa yang otomatis dibuat oleh server (seperti `id`).
- Konversi tipe data formulir: mengapa nilai elemen HTML `<input>` selalu berupa `string` dan bagaimana mengubahnya ke `number` secara aman via fungsi pembantu `toInput()`.
- Pengalaman pengguna (*User Experience*): mematikan tombol (*disable*) saat proses simpan sedang berlangsung untuk mencegah klik ganda (*double submit*).

*(Bahan bacaan pendalaman opsional: Modul React Bootcamp Bab 2.1 tentang Form Handling Lanjutan).*

---

## Ringkasan Konsep Kunci & Analogi

### 1. Tipe Data Formulir: Eksplisit vs Utility Type

Saat pengguna menambah produk baru, mereka **tidak menentukan ID** (karena ID unik dibuat otomatis oleh server) dan **tidak mengetik tanggal pembuatan** (`created_at`).  
Mari kita buat tipe data khusus untuk kiriman formulir di `src/types/product.ts`:

```ts
// src/types/product.ts

// Versi Eksplisit (Mudah dibaca dan dipahami pemula):
export interface CreateProductInput {
  name: string
  description: string
  price: number
  stock: number
  status: ProductStatus
  category_id: number
  merchant_name: string
}
```

> **Konsep Tambahan (Alternatif Cepat):**  
> Di TypeScript, ada jalan pintas bernama *Utility Type* `Omit`. Kamu juga bisa menulisnya dengan:  
> `export type CreateProductInput = Omit<Product, 'id' | 'created_at'>`  
> Artinya: *"Ambil seluruh tipe Product, tetapi kecualikan kolom id dan created_at"*. Kedua cara ini sah dan menghasilkan kontrak tipe yang sama persis!

### 2. Mengapa Nilai State Form Berupa String?

> **Analogi Kasir:**  
> Papan ketik mesin kasir selalu menerima ketikan tuts berupa simbol karakter/teks (string). Meskipun pengguna mengetik angka di `<input type="number">`, browser JavaScript tetap mengembalikan nilai `event.target.value` sebagai string (contoh: `"25000"`).  
> Sebelum dikirim ke API backend, kasir harus mengubah teks tersebut menjadi angka murni (`Number("25000") = 25000`). Jika kolom dibiarkan kosong, `Number("")` menghasilkan `0`.

---

## Langkah demi Langkah Mengembangkan Slice 2

### Langkah 1: Tambahkan Fungsi `createProduct` di Klien API

Buka berkas `src/api/products.ts` dan tambahkan fungsi pemanggil HTTP POST:

```ts
// src/api/products.ts
import type { CreateProductInput, Product } from '../types/product'
import { fetchJson } from './http'

// ...fungsi getProducts() tetap di atas...

export function createProduct(input: CreateProductInput): Promise<Product> {
  return fetchJson<Product>('/products', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    // created_at diisi sementara di sisi klien (di Bulan 4 backend yang akan mengisinya)
    body: JSON.stringify({ ...input, created_at: new Date().toISOString() }),
  })
}
```

---

### Langkah 2: Buat Komponen Formulir `ProductForm.tsx`

Buat berkas `src/components/ProductForm.tsx`. Perhatikan bagian `// TODO:` dan lengkapi logika konversi inputnya:

```tsx
// src/components/ProductForm.tsx
import { useState } from 'react'
import type { ChangeEvent, FormEvent } from 'react'
import type { CreateProductInput, ProductStatus } from '../types/product'

// Nilai input mentah dari elemen HTML form
interface FormValues {
  name: string
  description: string
  price: string
  stock: string
  status: ProductStatus
  merchant_name: string
}

const emptyValues: FormValues = {
  name: '',
  description: '',
  price: '',
  stock: '',
  status: 'active',
  merchant_name: '',
}

// Fungsi konversi nilai teks HTML menjadi objek CreateProductInput yang siap kirim
function toInput(values: FormValues): CreateProductInput {
  return {
    name: values.name.trim(),
    description: values.description.trim(),
    // TODO 1: Konversikan price dan stock dari string ke number
    price: Number(values.price),
    stock: Number(values.stock),
    status: values.status,
    category_id: 1, // Kategori sementara diisi 1 (Kuliner), akan dinamis di Bulan 3
    merchant_name: values.merchant_name.trim(),
  }
}

interface ProductFormProps {
  onSubmit: (input: CreateProductInput) => Promise<void>
}

function ProductForm({ onSubmit }: ProductFormProps) {
  const [values, setValues] = useState<FormValues>(emptyValues)
  const [isSubmitting, setIsSubmitting] = useState(false)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)

  function handleChange(
    event: ChangeEvent<HTMLInputElement | HTMLTextAreaElement | HTMLSelectElement>,
  ) {
    const { name, value } = event.target
    setValues((current) => ({ ...current, [name]: value }))
  }

  async function handleSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault()
    setIsSubmitting(true)
    setErrorMessage(null)

    try {
      // TODO 2: Panggil prop onSubmit dengan data yang sudah dikonversi via toInput(values)
      await onSubmit(toInput(values))
      // Kosongkan form kembali setelah berhasil
      setValues(emptyValues)
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : 'Terjadi kendala saat menyimpan')
    } finally {
      setIsSubmitting(false)
    }
  }

  return (
    <form className="product-form" onSubmit={handleSubmit} style={{ marginBottom: '32px' }}>
      <h2>Tambah Produk UMKM Baru</h2>

      <div>
        <label>
          Nama Produk:
          <input name="name" value={values.name} onChange={handleChange} required />
        </label>
      </div>

      <div>
        <label>
          Deskripsi:
          <textarea name="description" value={values.description} onChange={handleChange} />
        </label>
      </div>

      <div style={{ display: 'flex', gap: '16px' }}>
        <label style={{ flex: 1 }}>
          Harga (Rp):
          <input
            name="price"
            type="number"
            min="0"
            value={values.price}
            onChange={handleChange}
            required
          />
        </label>

        <label style={{ flex: 1 }}>
          Stok:
          <input
            name="stock"
            type="number"
            min="0"
            value={values.stock}
            onChange={handleChange}
            required
          />
        </label>
      </div>

      <div style={{ display: 'flex', gap: '16px' }}>
        <label style={{ flex: 1 }}>
          Status Publikasi:
          <select name="status" value={values.status} onChange={handleChange}>
            <option value="active">Aktif (Tersedia)</option>
            <option value="draft">Draft (Disimpan Sementara)</option>
          </select>
        </label>

        <label style={{ flex: 1 }}>
          Nama UMKM:
          <input
            name="merchant_name"
            value={values.merchant_name}
            onChange={handleChange}
            required
          />
        </label>
      </div>

      {errorMessage !== null && <p role="alert" style={{ color: 'red' }}>{errorMessage}</p>}

      <button type="submit" disabled={isSubmitting} style={{ marginTop: '12px' }}>
        {isSubmitting ? 'Menyimpan ke Server...' : 'Simpan Produk'}
      </button>
    </form>
  )
}

export default ProductForm
```

---

### Langkah 3: Hubungkan Formulir ke `ProductsPage.tsx`

Buka `src/pages/ProductsPage.tsx`. Tambahkan handler untuk menerima data dari formulir dan langsung memasukkan produk baru ke daftar tanpa fetch ulang:

```tsx
// src/pages/ProductsPage.tsx
import { createProduct, getProducts } from '../api/products'
import ProductForm from '../components/ProductForm'
import type { CreateProductInput, Product } from '../types/product'

// ...di dalam fungsi komponen ProductsPage, sebelum blok if (isLoading):

async function handleCreateProduct(input: CreateProductInput) {
  // 1. Kirim ke server lewat HTTP POST
  const newProduct = await createProduct(input)
  
  // 2. Perbarui state lokal secara instan (Optimistic-like feel tanpa reload)
  setProducts((currentProducts) => [...currentProducts, newProduct])
}

// ...di bagian JSX pengembalian, letakkan form sebelum komponen <ProductList>:
return (
  <section>
    <ProductForm onSubmit={handleCreateProduct} />
    <hr style={{ margin: '24px 0', border: 'none', borderTop: '1px solid #e2e8f0' }} />
    <p>Menampilkan {products.length} produk dari server</p>
    <ProductList products={products} />
  </section>
)
```

---

## Analisis Bug & Prediksi (Aktivitas Blok 2)

Diskusikan bersama rekan pairing:

1. **Prediksi Bug Nilai NaN:**  
   Jika di fungsi `toInput` seorang murid lupa menulis fungsi `Number(...)` dan hanya menulis:
   ```ts
   price: values.price as any
   ```
   Lalu di `ProductCard.tsx` harga diformat dengan `formatRupiah(product.price)`. Mengapa tampilan di browser bisa memunculkan tulisan aneh atau melempar error saat data dirender?
2. **Uji Perlindungan Tombol:**  
   Buka form di browser. Buka tab Network di Inspect Element. Klik tombol "Simpan Produk". Perhatikan apakah tombol langsung berubah teks menjadi *"Menyimpan ke Server..."* dan tidak bisa diklik ulang selama request berlangsung.

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan secara mandiri di kelas. Simpan hasilnya di:  
`tugas/squad-<nomor>/<nama-kamu>/tugas_02e.md`

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Tuliskan identitas diri (Nama, Squad, Tanggal).
3. Buka browser dan tambahkan 1 produk baru melalui form di aplikasi katalogmu (contoh: *"Kripik Singkong Balado 200g"*, Harga `15000`, Stok `30`).
   - Periksa tab Network browser: catat Request Method (`POST`) dan status respons yang diberikan server (`201 Created`).
   - Buka berkas `db.json` di VS Code dan pastikan produk barumu sudah tercatat dengan nomor `id` otomatis.
   - Salin objek JSON produk barumu tersebut ke dalam berkas tugas.
4. Jawab 2 pertanyaan pemahaman:
   - Mengapa kita menambahkan produk baru ke state `products` menggunakan sintaks spread `[...currentProducts, newProduct]` dan bukan melakukan fetch ulang seluruh daftar produk dari server?
   - Mengapa atribut `disabled={isSubmitting}` pada tombol submit sangat penting untuk kenyamanan dan keamanan transaksi pengguna?
5. Ajukan Pull Request ke repositori squad.

### Contoh Format Hasil (`tugas_02e.md`)

```markdown
# Tugas Mandiri 02e — Slice 2: Form Tambah Produk
Nama: Hendra Wijaya
Squad: Squad 4
Tanggal: 13 November 2026

## 1. Verifikasi Data Baru di `db.json`
Status HTTP saat simpan: `201 Created`

Data tersimpan di `db.json`:
```json
{
  "name": "Kripik Singkong Balado 200g",
  "description": "Pedas manis renyah khas Padang kemasan higienis.",
  "price": 15000,
  "stock": 30,
  "status": "active",
  "category_id": 1,
  "merchant_name": "Camilan Berkah",
  "created_at": "2026-11-13T07:15:22.123Z",
  "id": 13
}
```

## 2. Jawaban Pertanyaan Pemahaman
1. Menggunakan sintaks spread memperbarui state di memori browser secara langsung tanpa memicu request jaringan tambahan. Ini membuat aplikasi terasa sangat cepat dan responsif bagi pengguna, sekaligus menghemat penggunaan kuota dan bandwidth server.
2. Atribut `disabled={isSubmitting}` mencegah pengguna yang tidak sabaran mengeklik tombol submit berkali-kali secara cepat. Tanpa proteksi ini, aplikasi bisa mengirimkan 2 atau 3 request POST secara bersamaan yang menyebabkan produk yang sama tersimpan ganda (*duplicate entry*) di database.
```

---

Lanjut ke: **03a-http-methods-dan-api-patterns.md** (Minggu 3)
