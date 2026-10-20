# 2.0c Slice 1 — Katalog dari API (Fetch & Loading State)

## Tujuan slice ini

Data produk yang tadinya hardcode, sekarang diambil dari **API palsu** (`json-server`, sudah berjalan di `localhost:3001` sejak `npm run dev`). Ini pertama kalinya aplikasi kita "bicara" dengan server.

> **Prasyarat:** kamu sudah menyelesaikan `02a` (state & useState) dan `02b` (useEffect & lifecycle). Kalau belum, kerjakan dulu — slice ini pakai kedua konsep itu.

## Bacaan wajib (modul React bootcamp)

- **Bab 2.4** — API Integration & Async Operations (fetch API, loading states, error handling)
- **Bab 2.3** — Component Lifecycle & useEffect (review kalau belum solid)

## Kenapa ini penting untuk produk

Semua aplikasi nyata mengambil data dari server, bukan dari kode. Slice ini melatih pola yang akan dipakai **terus-menerus** sepanjang 12 bulan: `fetch` → tunggu → tampilkan / tangani error.

## Konsep yang dipakai

- **HTTP**: method `GET`, status code (`200` = sukses, `404` = tidak ada, dst.)
- **`fetch`** dan **`Promise`**
- **Generic function**: `fetchJson<T>()`
- **`useEffect`** untuk mengambil data saat komponen pertama muncul
- **Loading state** dan **error state**

## Langkah demi langkah

### 1. Bikin fungsi generic untuk fetch

Buat `src/api/http.ts`:

```ts
import { API_URL } from '../config'

export async function fetchJson<T>(path: string, init?: RequestInit): Promise<T> {
  const response = await fetch(`${API_URL}${path}`, init)

  if (!response.ok) {
    throw new Error(`Permintaan gagal dengan kode ${response.status}`)
  }

  return (await response.json()) as T
}
```

**Kenapa generic `<T>`?** Supaya fungsi ini bisa dipakai untuk mengambil produk (`fetchJson<Product[]>(...)`) maupun data lain nanti (kategori, dst.), dengan TypeScript tetap tahu tipe hasilnya — tanpa menulis fungsi fetch terpisah untuk tiap jenis data.

**Kenapa cek `response.ok`?** `fetch` **tidak** otomatis melempar error kalau server membalas `404` atau `500` — itu tetap dianggap "berhasil terkirim". Kita yang harus cek manual lewat `response.ok` (true kalau status 200-299).

### 2. Bikin fungsi khusus ambil produk

Buat `src/api/products.ts`:

```ts
import type { Product } from '../types/product'
import { fetchJson } from './http'

export function getProducts(): Promise<Product[]> {
  return fetchJson<Product[]>('/products')
}
```

### 3. Hapus data hardcode

Hapus `src/data/products.ts` — sudah tidak dipakai.

### 4. Pindahkan logika ke halaman tersendiri

Buat `src/pages/ProductsPage.tsx`. Ini komponen yang bertanggung jawab **mengambil data** dan **menampilkan status** (loading/error/hasil):

```tsx
import { useEffect, useState } from 'react'
import { getProducts } from '../api/products'
import ProductList from '../components/ProductList'
import type { Product } from '../types/product'

function ProductsPage() {
  const [products, setProducts] = useState<Product[]>([])
  const [isLoading, setIsLoading] = useState(true)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)

  useEffect(() => {
    let ignore = false

    async function loadProducts() {
      try {
        const data = await getProducts()
        if (!ignore) {
          setProducts(data)
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
  }, [])

  if (isLoading) {
    return <p>Memuat produk...</p>
  }

  if (errorMessage !== null) {
    return <p role="alert">Gagal memuat produk: {errorMessage}</p>
  }

  return (
    <section>
      <p>Menampilkan {products.length} produk</p>
      <ProductList products={products} />
    </section>
  )
}

export default ProductsPage
```

Ini pola yang **akan sering kamu tulis ulang** sepanjang program: `isLoading`, `errorMessage`, dan variabel `ignore` untuk mencegah update state setelah komponen dibongkar (misal karena pindah halaman sebelum fetch selesai). Jangan hafalkan literal, tapi paham **kenapa** tiga bagian ini selalu ada:

1. Sebelum data datang → tampilkan "Memuat...".
2. Kalau gagal → tampilkan pesan error, jangan halaman kosong/blank.
3. Kalau berhasil → tampilkan datanya.

### 5. Sederhanakan `App.tsx`

```tsx
import ProductsPage from './pages/ProductsPage'

function App() {
  return (
    <main>
      <h1>Katalog UMKM</h1>
      <ProductsPage />
    </main>
  )
}

export default App
```

### 6. Cek hasilnya

- Buka `localhost:5173` — sekarang data yang tampil harus sama dengan isi `db.seed.json`, bukan data hardcode lama.
- Buka DevTools browser → tab **Network** → refresh halaman → cari request ke `products`. Lihat status code-nya (harus `200`).
- Coba matikan API (`Ctrl+C` di terminal yang menjalankan `json-server`, atau matikan sebentar), refresh halaman — harus muncul pesan error, bukan halaman putih kosong.

## Latihan

1. Tambahkan `npm run dev:api:slow` (sudah tersedia di starter) untuk mensimulasikan API lambat (jeda 1,2 detik). Perhatikan tampilan "Memuat..." muncul lebih lama — ini cara mengecek loading state benar-benar berfungsi, bukan cuma kelewat cepat untuk dilihat.
2. Di DevTools, matikan koneksi internet (tab Network → Offline), refresh halaman, lihat pesan error yang muncul. Apakah pesannya cukup jelas buat user biasa?

## Cek pemahaman

- Kenapa kita butuh variabel `ignore` di dalam `useEffect`? Apa yang bisa terjadi kalau tidak ada?
- Apa bedanya "request gagal karena network down" dengan "request sukses terkirim tapi server membalas 404"? Bagaimana masing-masing ditangani di kode di atas?

## Kesalahan umum

| Gejala | Sebab | Solusi |
|---|---|---|
| Halaman terus menampilkan "Memuat..." | `setIsLoading(false)` tidak terpanggil (biasanya lupa di blok `finally`) | Pastikan `finally` selalu jalan baik sukses maupun gagal |
| `Uncaught (in promise)` di console | Error dari fetch tidak ditangkap `try/catch` | Cek lagi struktur `try { } catch { } finally { }` |
| Data tidak update setelah edit `db.seed.json` | `db.json` sudah dibuat sebelumnya dan tidak otomatis sinkron | Jalankan `npm run reset-db` |

## Kaitkan ke rujukan

`useEffect` dan fetch data sudah disinggung juga di pre-class (bagian JavaScript async) dan modul React bootcamp bagian **State Management & Hooks** — kalau bagian `Promise`/`async-await` masih kurang lancar, ini saat yang tepat untuk membuka ulang.

---

Lanjut ke: **03-form-tambah-produk.md** (Slice 2)
