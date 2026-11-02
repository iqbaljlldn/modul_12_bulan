# 3.0a HTTP Methods & API Patterns — PATCH, DELETE, & ApiError

## Tujuan Sesi Ini

Memahami perbedaan metode HTTP dalam standar REST API (**GET, POST, PUT, PATCH, DELETE**), memahami kode status HTTP yang lazim ditemui (`200`, `201`, `204`, `400`, `404`, `500`), dan membuat kelas error khusus **`ApiError`** untuk menangani kegagalan jaringan secara elegan.

---

## Aktivitas Terbimbing di Kelas (Blok 1, 10-15 Menit)

Mentor akan memandu demonstrasi konsep:
- Perbedaan krusial antara **PATCH** (mengubah sebagian kolom saja) vs **PUT** (menimpa seluruh objek).
- Mengapa operasi **DELETE** umumnya mengembalikan status **204 No Content** (berhasil tanpa isi) dan bagaimana menanganinya agar tidak memicu error parsing JSON.
- Mengenal struktur kelas (*class*) TypeScript sederhana melalui `ApiError`.
- Menulis fungsi klien jaringan `updateProduct` dan `deleteProduct` di `src/api/products.ts`.

*(Bahan bacaan pendalaman opsional: Modul React Bootcamp Bab 2.4 tentang HTTP Methods Lanjutan).*

---

## Ringkasan Konsep Kunci & Analogi

### 1. Membedakan PUT vs PATCH

> **Analogi Sehari-hari:**  
> Bayangkan sebuah mobil di bengkel:  
> - **PUT (Ganti Total):** Mengganti seluruh mobil dengan unit baru. Kamu harus mengirimkan kembali semua data komponen (roda, mesin, spion, bodi), meskipun yang rusak sebenarnya hanya spionnya. Jika ada kolom yang lupa kamu kirimkan, kolom itu bisa terhapus di database.  
> - **PATCH (Tambal Sebagian):** Hanya mengganti spion kanan yang retak. Kamu cukup mengirimkan data yang berubah saja: `{ "price": 25000 }`. Kolom nama, deskripsi, dan foto tetap aman tidak disentuh.  
> Untuk aplikasi Katalog UMKM, **kita memilih PATCH** karena pedagang biasanya hanya ingin mengubah harga atau stok barang!

### 2. Mengapa Butuh Class `ApiError`?

> **Analogi Tiket Tilang Polisi:**  
> Objek `Error` standar bawaan JavaScript hanya memiliki pesan teks (`message: "Gagal"`). Kita tidak tahu apakah error itu karena internet mati, salah ketik kode, atau barang memang tidak ada di server.  
> Class `ApiError` seperti **surat tilang resmi berstempel**: selain membawa pesan tertulis, ia memiliki nomor pasal pelanggaran (**`status: 404`** atau **`status: 500`**). Dengan begitu, komponen React kita bisa membaca: *"Jika statusnya 404, tampilkan pesan 'Produk Tidak Ditemukan' ke pengguna"*.

### 3. Tipe Data Update: Eksplisit vs Partial

Saat mengedit produk, field mana pun boleh kosong jika tidak diubah. Kita bisa menuliskannya secara eksplisit dengan tanda tanya (`?`):

```ts
// src/api/products.ts

// Versi Eksplisit (Sangat mudah dibaca):
export interface UpdateProductInput {
  name?: string
  description?: string
  price?: number
  stock?: number
  status?: ProductStatus
  merchant_name?: string
}
```

> **Konsep Tambahan (Alternatif Cepat):**  
> Di TypeScript, ada *Utility Type* bawaan bernama `Partial`. Kamu juga bisa menulis:  
> `export type UpdateProductInput = Partial<CreateProductInput>`  
> Artinya: *"Jadikan semua field di CreateProductInput menjadi opsional (boleh diisi, boleh tidak)"*.

---

## Langkah demi Langkah: Memperluas API Client

### Langkah 1: Buat Class `ApiError` (`src/errors/ApiError.ts`)

Buat berkas `src/errors/ApiError.ts`:

```ts
// src/errors/ApiError.ts

// Class error khusus yang membawa nomor kode status HTTP dari server
export class ApiError extends Error {
  status: number

  constructor(status: number, message: string) {
    super(message)
    this.name = 'ApiError'
    this.status = status
  }
}
```

---

### Langkah 2: Perbarui Klien Fetch (`src/api/http.ts`)

Buka `src/api/http.ts`. Kita sesuaikan agar melempar `ApiError` dan menangani respons `204 No Content`:

```ts
// src/api/http.ts
import { API_URL } from '../config'
import { ApiError } from '../errors/ApiError'

export async function fetchJson<T>(path: string, init?: RequestInit): Promise<T> {
  const response = await fetch(`${API_URL}${path}`, init)

  // 1. Jika gagal, lemparkan ApiError dengan membawa nomor status HTTP
  if (!response.ok) {
    throw new ApiError(response.status, `Permintaan gagal dengan kode status ${response.status}`)
  }

  // 2. Tangani DELETE: status 204 No Content tidak memiliki isi data JSON
  if (response.status === 204) {
    return undefined as T
  }

  // 3. Untuk status 200/201, baca isi data JSON seperti biasa
  return (await response.json()) as T
}
```

---

### Langkah 3: Tambahkan `updateProduct` dan `deleteProduct` (`src/api/products.ts`)

Buka `src/api/products.ts`. Perhatikan bagian `// TODO:` dan lengkapi kodenya:

```ts
// src/api/products.ts
import type { CreateProductInput, Product } from '../types/product'
import { fetchJson } from './http'

// Tipe data input pembaruan produk (semua kolom opsional)
export type UpdateProductInput = Partial<CreateProductInput>

export function getProducts(): Promise<Product[]> {
  return fetchJson<Product[]>('/products')
}

export function createProduct(input: CreateProductInput): Promise<Product> {
  return fetchJson<Product>('/products', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ ...input, created_at: new Date().toISOString() }),
  })
}

// TODO 1: Implementasikan updateProduct dengan metode 'PATCH'
export function updateProduct(id: number, input: UpdateProductInput): Promise<Product> {
  return fetchJson<Product>(`/products/${id}`, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(input),
  })
}

// TODO 2: Implementasikan deleteProduct dengan metode 'DELETE'
export function deleteProduct(id: number): Promise<void> {
  return fetchJson<void>(`/products/${id}`, {
    method: 'DELETE',
  })
}
```

---

## Analisis Bug & Prediksi (Aktivitas Blok 2)

Diskusikan bersama rekan pairing:

1. **Prediksi Error 204:**  
   Jika di `fetchJson` kita lupa mengecek `if (response.status === 204)` dan langsung memanggil `await response.json()`, apa pesan error yang akan muncul di console browser saat pengguna menghapus produk?  
   *(Petunjuk: `json-server` tidak mengembalikan body teks apa pun pada status 204).*
2. **Kuis Status Code:**  
   Sebutkan kode status HTTP untuk:
   - Berhasil mengambil data: `...`
   - Berhasil membuat data baru: `...`
   - Berhasil menghapus tanpa mengembalikan data: `...`
   - Barang yang dicari tidak ada di database: `...`

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan secara mandiri di kelas. Simpan hasilnya di:  
`tugas/squad-<nomor>/<nama-kamu>/tugas_03a.md`

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Tuliskan identitas diri (Nama, Squad, Tanggal).
3. Lakukan pengujian langsung fungsi API melalui terminal (menggunakan `curl`) atau via browser console:
   - Jalankan perintah PATCH untuk mengubah harga produk ID 1 menjadi `22000`:
     ```bash
     curl -X PATCH http://localhost:3001/products/1 -H "Content-Type: application/json" -d "{\"price\": 22000}"
     ```
   - Catat respon yang dikembalikan server.
   - Buka `http://localhost:3001/products/1` di browser untuk memastikan harga sudah terupdate di `db.json`.
4. Jawab 2 pertanyaan pemahaman:
   - Mengapa kita menggunakan metode `PATCH` dan bukan `PUT` saat memperbarui harga atau stok produk UMKM di aplikasi kita?
   - Mengapa kita membuat class `ApiError` yang menyimpan properti `status: number` alih-alih cukup memakai `new Error("Gagal")` biasa?
5. Ajukan Pull Request ke repositori squad.

### Contoh Format Hasil (`tugas_03a.md`)

```markdown
# Tugas Mandiri 03a — HTTP Methods & API Patterns
Nama: Ilham Maulana
Squad: Squad 1
Tanggal: 16 November 2026

## 1. Bukti Uji Coba PATCH
Perintah cURL:
`curl -X PATCH http://localhost:3001/products/1 -H "Content-Type: application/json" -d "{\"price\": 22000}"`

Respon Server:
```json
{
  "id": 1,
  "name": "Keripik Tempe Renyah 250g",
  "description": "Keripik tempe kedelai lokal tanpa bahan pengawet.",
  "price": 22000,
  "stock": 45,
  "status": "active",
  "category_id": 1,
  "merchant_name": "Dapur Bu Sri",
  "created_at": "2026-01-15T08:00:00Z"
}
```

## 2. Jawaban Pertanyaan Pemahaman
1. `PATCH` hanya memperbarui kolom yang kita kirimkan (dalam contoh ini: kolom harga saja), sedangkan kolom lain yang tidak dikirimkan tetap utuh tersimpan di database. Jika kita memakai `PUT`, kita diwajibkan mengirim seluruh data objek lengkap; jika ada satu kolom terlewat, database bisa mengosongkan kolom tersebut.
2. `ApiError` menyimpan angka kode status HTTP (seperti 404 atau 500). Dengan informasi kode status ini, blok `catch` di komponen React kita dapat membuat keputusan cerdas: jika `error.status === 404`, kita bisa menampilkan teks "Produk tidak ditemukan", bukan sekadar pesan error generik yang membingungkan pengguna.
```

---

Lanjut ke: **03b-edit-hapus-dan-error.md** (Slice 3)
