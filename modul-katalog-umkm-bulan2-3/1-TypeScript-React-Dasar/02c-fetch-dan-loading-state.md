# 2.0c Slice 1 — Katalog dari API (Fetch, Loading, & Error State)

## Tujuan Slice Ini

Mengganti data produk yang tadinya statis (hardcode) menjadi data dinamis yang diambil langsung dari **API lokal** (`json-server` di port 3001). Ini adalah momen pertama aplikasi kita berkomunikasi secara nyata dengan jaringan server.

---

## Aktivitas Terbimbing di Kelas (Blok 1, 10-15 Menit)

Mentor akan memandu demonstrasi langsung:
- Menguji endpoint API di browser atau terminal (`http://localhost:3001/products`).
- Membuka tab **Network** di Developer Tools browser untuk melihat status kode HTTP `200 OK`.
- Memahami 3 kondisi wajib antarmuka: **Sedang Memuat (*Loading*)**, **Terjadi Kendala (*Error*)**, dan **Data Siap Ditampilkan (*Success*)**.
- Cara kerja pembungkus fungsi `fetchJson` sederhana.

*(Bahan bacaan pendalaman opsional: Modul React Bootcamp Bab 2.4 tentang API Integration & Async Operations).*

---

## Ringkasan Konsep Kunci & Analogi

### 1. Tiga Kondisi Wajib Antarmuka Jaringan

> **Analogi Sehari-hari:**  
> Mengambil data dari server mirip seperti memesan makanan di kasir restoran cepat saji:
> 1. **Fase Loading:** Papan nomor antreanmu berbunyi (pengguna diberi tanda *"Sedang memuat data..."* agar tahu sistem sedang bekerja).
> 2. **Fase Sukses:** Nampan makanan lezat disajikan di mejamu (daftar kartu produk tampil rapi di layar).
> 3. **Fase Error:** Jika gas kompor dapur mendadak habis, kasir segera menghampirimu dan menjelaskan kendalanya secara sopan (pesan error informatif, bukan membiarkan pelanggan menunggu selamanya di depan meja kosong!).

### 2. Mengapa Perlu Memeriksa `response.ok`?
Fungsi `fetch()` bawaan browser memiliki sifat unik: jika server membalas dengan status error seperti `404 Not Found` atau `500 Internal Server Error`, `fetch` **tidak menganggap itu sebagai error jaringan**. `fetch` hanya melempar error jika koneksi internet benar-benar terputus.  
Oleh karena itu, kita **wajib** memeriksa secara manual:

```ts
if (!response.ok) {
  throw new Error(`Permintaan gagal dengan kode status ${response.status}`)
}
```

---

## Langkah demi Langkah Mengembangkan Slice 1

### Langkah 1: Buat Modul Klien Jaringan (`src/api/http.ts`)

Mari buat fungsi pembantu untuk menangani pemanggilan API secara bersih.

```ts
// src/api/http.ts
import { API_URL } from '../config'

// Versi sederhana pembungkus fetch:
export async function fetchJson<T>(path: string, init?: RequestInit): Promise<T> {
  const response = await fetch(`${API_URL}${path}`, init)

  // Cek apakah status HTTP berada di rentang sukses (200-299)
  if (!response.ok) {
    throw new Error(`Permintaan gagal dengan kode status ${response.status}`)
  }

  return (await response.json()) as T
}
```

> **Catatan Pengenalan Generic `<T>`:**  
> Huruf `<T>` di atas adalah fitur TypeScript bernama *Generic*. Anggap `<T>` seperti kotak kosong fleksibel: jika kita memanggil `fetchJson<Product[]>('/products')`, TypeScript otomatis tahu bahwa hasil fungsi ini adalah array produk. Jika nanti kita memanggil `fetchJson<Category[]>('/categories')`, hasilnya otomatis berupa array kategori.

---

### Langkah 2: Buat Fungsi Khusus Pengambil Produk (`src/api/products.ts`)

Buat berkas `src/api/products.ts`:

```ts
// src/api/products.ts
import type { Product } from '../types/product'
import { fetchJson } from './http'

// Fungsi bersih dan terisolasi untuk mengambil daftar produk
export function getProducts(): Promise<Product[]> {
  return fetchJson<Product[]>('/products')
}
```

---

### Langkah 3: Hapus Berkas Data Hardcode

Hapus berkas `src/data/products.ts` karena kita tidak lagi menggunakan data tiruan statis!

---

### Langkah 4: Rangkai Halaman `ProductsPage.tsx`

Buat berkas `src/pages/ProductsPage.tsx`. Perhatikan bagian `// TODO:` dan lengkapi logika penanganan kondisinya:

```tsx
// src/pages/ProductsPage.tsx
import { useEffect, useState } from 'react'
import { getProducts } from '../api/products'
import ProductList from '../components/ProductList'
import type { Product } from '../types/product'

function ProductsPage() {
  const [products, setProducts] = useState<Product[]>([])
  const [isLoading, setIsLoading] = useState<boolean>(true)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)

  useEffect(() => {
    let ignore = false

    async function loadData() {
      try {
        const data = await getProducts()
        if (!ignore) {
          setProducts(data)
        }
      } catch (error) {
        if (!ignore) {
          setErrorMessage(error instanceof Error ? error.message : 'Terjadi kendala jaringan')
        }
      } finally {
        // TODO 1: Pastikan state loading diubah menjadi false baik sukses maupun gagal
        if (!ignore) {
          setIsLoading(false)
        }
      }
    }

    loadData()

    return () => {
      ignore = true
    }
  }, [])

  // TODO 2: Tampilkan pesan teks "Sedang memuat katalog..." jika isLoading bernilai true
  if (isLoading) {
    return <p className="loading-state">Sedang memuat data katalog UMKM...</p>
  }

  // TODO 3: Tampilkan pesan error dengan role="alert" jika errorMessage tidak null
  if (errorMessage !== null) {
    return <p role="alert" className="error-state">Gagal memuat produk: {errorMessage}</p>
  }

  // Tampilan ketika data berhasil didapatkan
  return (
    <section>
      <p>Menampilkan {products.length} produk dari server</p>
      <ProductList products={products} />
    </section>
  )
}

export default ProductsPage
```

---

### Langkah 5: Sambungkan ke `App.tsx`

Buka `src/App.tsx`:

```tsx
// src/App.tsx
import ProductsPage from './pages/ProductsPage'

function App() {
  return (
    <main style={{ maxWidth: '1000px', margin: '0 auto', padding: '24px 16px' }}>
      <header>
        <h1>Katalog UMKM Nusantara</h1>
      </header>
      <ProductsPage />
    </main>
  )
}

export default App
```

---

## Analisis Bug & Prediksi (Aktivitas Blok 2)

Diskusikan bersama rekan pairing:

1. **Eksperimen Server Mati:**  
   Buka terminal tempat `json-server` berjalan. Hentikan server sebentar (`Ctrl+C`). Kembali ke browser dan refresh halaman `localhost:5173`.  
   *Pertanyaan:* Apa yang ditampilkan di layar? Apakah aplikasi meledak menjadi layar putih kosong atau menampilkan pesan error ramah?
2. **Uji Coba Jaringan Lambat (Simulasi Nyata):**  
   Jalankan server dengan mode lambat menggunakan skrip `npm run dev:api:slow` yang tersedia di starter. Refresh halaman dan perhatikan teks *"Sedang memuat data..."* selama 1,2 detik. Mengapa pengujian ini penting sebelum aplikasi dirilis ke pengguna UMKM?

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan secara mandiri di kelas. Simpan hasilnya di:  
`tugas/squad-<nomor>/<nama-kamu>/tugas_02c.md`

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Tuliskan identitas diri (Nama, Squad, Tanggal).
3. Buka browser Developer Tools (tekan tombol F12 atau klik kanan > Inspect), buka tab **Network**, lalu refresh halaman katalogmu.
   - Temukan baris request ke `products`.
   - Catat: Request URL, Request Method, Status Code, dan Type.
   - Buka sub-tab **Response** dan tuliskan 1 contoh cuplikan objek produk yang dikembalikan server.
4. Jawab 2 pertanyaan pemahaman:
   - Apa yang akan terjadi pada tampilan pengguna jika seorang programmer lupa menulis blok `finally { setIsLoading(false) }` saat panggilan API mengalami error jaringan?
   - Mengapa kita tidak boleh menganggap bahwa `fetch()` otomatis melempar error saat server memberikan respons HTTP 404 (Not Found)?
5. Ajukan Pull Request ke repositori squad.

### Contoh Format Hasil (`tugas_02c.md`)

```markdown
# Tugas Mandiri 02c — Slice 1: Fetch API
Nama: Fajar Nugraha
Squad: Squad 2
Tanggal: 11 November 2026

## 1. Hasil Inspeksi Network Tab
- Request URL: `http://localhost:3001/products`
- Request Method: `GET`
- Status Code: `200 OK`
- Type: `fetch` / `json`

Contoh potongan data respons:
```json
{
  "id": 1,
  "name": "Keripik Tempe Renyah 250g",
  "price": 18000,
  "stock": 45,
  "status": "active"
}
```

## 2. Jawaban Pertanyaan Pemahaman
1. Jika lupa menulis `setIsLoading(false)` di blok `finally`, maka saat terjadi error, state `isLoading` akan tetap bernilai `true` selamanya. Akibatnya, pengguna akan terus-menerus melihat tulisan "Sedang memuat..." tanpa pernah tahu bahwa request-nya sebenarnya sudah gagal.
2. Karena spesifikasi bawaan `fetch()` hanya menolak Promise (*reject*) jika terjadi kegagalan jaringan fisik (misalnya komputer offline atau server down total). Selama server masih bisa menjawab (walaupun jawabannya adalah 404 atau 500), Promise tetap dianggap selesai (*resolved*). Oleh karena itu, kita wajib memeriksa properti `response.ok` secara manual.
```

---

Lanjut ke: **02d-event-handling-dan-form.md**
