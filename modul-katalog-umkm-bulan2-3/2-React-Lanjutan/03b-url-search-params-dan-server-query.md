# 2.3b State di URL (useSearchParams) & Server-side Query

> **Bacaan wajib sebelum sesi:** Modul React Programmer Pit — **Bab 3.5** (React Router Advanced Features — URL Search Params).  
> **Prasyarat:** Menguasai React Router dasar (`BrowserRouter`, `Routes`, `useParams`) dari Bulan 2 (Slice 4).

---

## Kenapa Unit Ini Ada?

Ketika pengguna memfilter data produk (misalnya memilih kategori "Makanan", mengurutkan harga "Termurah", dan membuka "Halaman 2"), di manakah pilihan filter tersebut sebaiknya disimpan?

Kebanyakan pemula menyimpannya di `useState` lokal di dalam komponen:
```tsx
// ❌ Jangan simpan filter kompleks hanya di useState lokal:
const [category, setCategory] = useState('')
const [page, setPage] = useState(1)
```

Pendekatan `useState` lokal ini punya 3 kelemahan fatal di aplikasi web:
1. **Tidak Bisa Dibagikan (*Not Shareable*):** Jika kamu menyalin URL dari address bar dan mengirimkannya ke teman lewat WhatsApp, temanmu akan melihat halaman katalog kosong/default, bukan hasil pencarian yang sedang kamu lihat!
2. **Hilang Saat Refresh (*State Loss on Reload*):** Pengguna yang menekan tombol **F5 / Refresh** akan kehilangan seluruh filter yang sudah dipilih dengan susah payah.
3. **Merusak Tombol Back/Forward Browser:** Menekan tombol "Kembali" di browser tidak membatalkan filter sebelumnya, melainkan langsung keluar dari halaman.

Solusi standar web modern: **Jadikan URL sebagai Single Source of Truth (*Satu-satunya Sumber Kebenaran*)!**

---

## 1. Membaca & Menulis Query String dengan `useSearchParams`

React Router menyediakan hook `useSearchParams` yang perilakunya mirip dengan `useState`, tetapi nilainya tersimpan langsung di address bar browser:

```text
https://katalog-umkm.id/?q=kopi&category=2&sort=price&order=asc&page=2
                          └─── Query String (Search Params) ───┘
```

### Langkah A: Membaca Filter dari URL (`readFilters`)

```ts
import { defaultFilters } from '../types/productFilters'
import type { ProductFilters as Filters } from '../types/productFilters'

function readFilters(searchParams: URLSearchParams): Filters {
  return {
    q: searchParams.get('q') ?? defaultFilters.q,
    categoryId: searchParams.get('category') ?? defaultFilters.categoryId,
    sort: (searchParams.get('sort') as Filters['sort']) ?? defaultFilters.sort,
    order: (searchParams.get('order') as Filters['order']) ?? defaultFilters.order,
    page: Number(searchParams.get('page') ?? defaultFilters.page),
  }
}
```

Perhatikan: nilai dari URL selalu berupa string atau `null`. Operator `??` (*nullish coalescing*) memastikan jika parameter belum ada di URL, aplikasi menggunakan nilai standar (*default*).

### Langkah B: Menulis Filter ke URL (`setSearchParams`)

Saat ada filter yang berubah, kita perbarui URL:

```tsx
const [searchParams, setSearchParams] = useSearchParams()
const urlFilters = readFilters(searchParams)

function handleFilterChange(next: Partial<Filters>) {
  const merged = { ...urlFilters, ...next }
  setSearchParams({
    q: merged.q,
    category: merged.categoryId,
    sort: merged.sort,
    order: merged.order,
    page: String(merged.page),
  })
}
```

Ketika `setSearchParams` dipanggil, URL di browser langsung berubah menjadi `/?category=2&page=1`, dan React Router secara otomatis memicu re-render komponen dengan nilai filter yang baru!

---

## 2. Server-side Query: Mengapa Bukan Filter di Frontend?

Jika katalog UMKM kita nanti memiliki **5.000 produk**, apakah kita akan mengambil 5.000 data sekaligus lalu memfilternya dengan JavaScript di browser pengguna? Tentu tidak! Itu akan membuat browser HP pengguna hang dan menghabiskan kuota internet.

Kita mengirimkan parameter filter langsung ke server:
- `q=sepatu` — mencari nama produk yang mengandung kata sepatu
- `category_id=3` — hanya produk dari kategori ID 3
- `_sort=price&_order=asc` — urutkan harga dari termurah ke termahal
- `_page=1&_limit=6` — ambil hanya 6 produk untuk halaman 1

### Menggunakan `URLSearchParams` Standar Browser
Di `src/api/products.ts`, jangan gabungkan string URL secara manual (seperti `"?q=" + q + "&cat=" + cat`) karena karakter spasi atau simbol bisa merusak URL. Gunakan API resmi `URLSearchParams`:

```ts
const params = new URLSearchParams()
if (filters.q.trim().length > 0) params.set('q', filters.q.trim())
if (filters.categoryId.length > 0) params.set('category_id', filters.categoryId)
params.set('_sort', filters.sort)
params.set('_order', filters.order)
params.set('_page', String(filters.page))
params.set('_limit', String(PAGE_SIZE))

// Menghasilkan string yang aman dan ter-encode:
// "/products?q=kopi+susu&_sort=price&_order=asc&_page=1&_limit=6"
return fetchPage<Product>(`/products?${params.toString()}`)
```

---

## 3. Membaca Total Data dari Header HTTP (`X-Total-Count`)

Ketika server hanya mengembalikan 6 produk untuk halaman 1, bagaimana frontend tahu **berapa total seluruh halaman** yang ada?

Server REST (seperti `json-server` dan nanti NestJS di Bulan 4) mengirimkan jumlah total seluruh data yang cocok di **Header Respons HTTP** bernama `X-Total-Count`.

Kita buat fungsi `fetchPage<T>` di `src/api/http.ts` yang membaca data sekaligus header tersebut:

```ts
export interface Page<T> {
  data: T[]
  total: number
}

export async function fetchPage<T>(path: string, init?: RequestInit): Promise<Page<T>> {
  const response = await fetch(`${API_URL}${path}`, init)

  if (!response.ok) {
    throw new ApiError(response.status, `Permintaan gagal dengan kode ${response.status}`)
  }

  const data = (await response.json()) as T[]
  const totalHeader = response.headers.get('X-Total-Count')
  const total = totalHeader !== null ? Number(totalHeader) : data.length

  return { data, total }
}
```

Dari `total` ini, kita bisa menghitung jumlah halaman dengan rumus matematika sederhana:
```ts
const totalPages = Math.max(1, Math.ceil(total / PAGE_SIZE))
```
Contoh: Ada 14 produk dengan `PAGE_SIZE = 6`.  
`Math.ceil(14 / 6)` = `Math.ceil(2.33)` = **3 halaman**.

---

## Latihan Mandiri (30 Menit)

1. **Inspeksi Header di DevTools:**
   Buka tab **Network** di DevTools browser, klik request `GET /products?...`, lalu buka tab **Headers**. Temukan baris `x-total-count` di bagian *Response Headers*.
2. **Ketik Langsung di Address Bar:**
   Coba ketik manual di address bar browser: `http://localhost:5173/?page=2`, lalu tekan Enter. Perhatikan bagaimana aplikasi langsung membuka halaman 2 secara otomatis!

---

## Cek Pemahaman

1. Mengapa menyimpan state pencarian dan filter di URL jauh lebih unggul dibandingkan menyimpannya di `useState` biasa?
2. Apa bahaya menggabungkan query string secara manual tanpa menggunakan `new URLSearchParams()`?
3. Mengapa total seluruh data dikirim lewat header `X-Total-Count`, bukan dimasukkan di dalam array data produk?

---

**Lanjut ke:** `03c-cari-filter-pagination.md` (Slice 7 — Implementasi Penuh Cari, Filter, Urutkan & Pagination)
