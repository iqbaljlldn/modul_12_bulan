# 2.4b Slice 8 — Konsolidasi & Kontrak API Tertulis

> **Bacaan wajib sebelum sesi:** Modul React Programmer Pit — **Bab 4.2** (Advanced Styling) & Dokumentasi API Katalog.  
> **Prasyarat:** Menyelesaikan `04a` (Desain Responsif) dan seluruh Slice 0-7.

---

## Tujuan Slice Ini

Ini bukan slice untuk membuat fitur baru — ini adalah slice untuk **merapikan seluruh kode** dan **menuliskan Kontrak API resmi (`docs/kontrak-api.md`)**.

Setelah slice ini selesai:
1. **Mini Katalog UMKM v2** tuntas dan siap didemokan (*production-ready MVP*).
2. Dokumen **Kontrak API** menjadi **spesifikasi resmi** yang wajib dipenuhi oleh Chapter Backend saat membangun REST API menggunakan NestJS & PostgreSQL di Bulan 4!

---

## Kenapa Ini Penting untuk Produk?

Hingga akhir Bulan 3, "kontrak" antara frontend dan backend mock (`json-server`) hanya tersimpan di kepala masing-masing developer atau tersebar di file-file `src/api/`.

Sebelum backend sungguhan dibangun bulan depan, kontrak ini **harus disepakati bersama oleh seluruh tribe**:
- **Chapter Backend** tahu persis nama endpoint, method HTTP, format payload JSON, dan kode status response yang diharapkan oleh frontend.
- Jika ada perilaku frontend yang ternyata mengandalkan trik khusus `json-server` (yang tidak standar di backend nyata), hal itu **terdeteksi sekarang**, bukan di tengah jalan Bulan 4 ketika integrasi sudah macet.

---

## Langkah demi Langkah Implementasi

### 1. Audit Endpoint dari Kode Frontend Sungguhan

Buka setiap file di dalam folder `src/api/`:
- `src/api/products.ts`
- `src/api/categories.ts`
- `src/api/http.ts`

Catat setiap request yang benar-benar dikirimkan oleh frontend kita. Jangan menebak dari ingatan — buka kode dan teliti baris demi baris!

---

### 2. Mengisi Dokumen `docs/kontrak-api.md`

Buka file template `docs/kontrak-api.md` di root repo. Lengkapi tabel spesifikasi endpoint seperti berikut:

#### Tabel Spesifikasi Endpoint Produk (`/products`)

| Method | Endpoint Path | Query Params / Body | Status Sukses | Respons Sukses (JSON / Header) | Status Error & Kondisi |
|---|---|---|---|---|---|
| `GET` | `/products` | Query: `q`, `category_id`, `_sort`, `_order`, `_page`, `_limit` | `200 OK` | Array `Product[]`, Total di Header `X-Total-Count` | `500` (Kesalahan Server) |
| `GET` | `/products/:id` | Param: `id` (number) | `200 OK` | Objek `Product` tunggal | `404 Not Found` (Produk tidak ada) |
| `POST` | `/products` | Body JSON: `CreateProductInput` (`name`, `price`, `stock`, `merchant_name`, `category_id`, `status`) | `201 Created` | Objek `Product` baru dengan `id` dari database | `400 Bad Request` (Validasi gagal) |
| `PATCH` | `/products/:id` | Param: `id`, Body JSON: `Partial<Product>` | `200 OK` | Objek `Product` yang sudah diperbarui | `400` (Data tidak valid), `404` (Tidak ditemukan) |
| `DELETE` | `/products/:id` | Param: `id` (number) | `200 OK` / `204 No Content` | Objek kosong `{}` atau status 204 | `404 Not Found` (Produk tidak ada) |

#### Tabel Spesifikasi Endpoint Kategori (`/categories`)

| Method | Endpoint Path | Query Params / Body | Status Sukses | Respons Sukses | Status Error |
|---|---|---|---|---|---|
| `GET` | `/categories` | *(tanpa param)* | `200 OK` | Array `Category[]` (`id`, `name`) | `500` (Server Error) |

---

### 3. Mendokumentasikan Catatan Perbedaan (*Mock vs Real Backend*)

Bagian paling krusial di `docs/kontrak-api.md` adalah bagian **"Catatan Perbedaan (json-server vs NestJS)"**. Ini adalah daftar temuan teknis yang harus diperhatikan oleh Chapter Backend di Bulan 4:

1. **Relasi Data Kategori:**
   - *Sekarang (json-server):* Frontend memanggil `GET /categories` dan `GET /products` secara terpisah, lalu mencocokkan `product.category_id === category.id` di sisi browser.
   - *Rencana Bulan 4 (NestJS + PostgreSQL):* Backend akan menggunakan klausa SQL `JOIN` sehingga endpoint `GET /products` langsung menyertakan objek relasi `{ id: 1, name: "Keripik", category: { id: 1, name: "Makanan Ringan" } }`.
2. **Validasi Input:**
   - *Sekarang:* `json-server` menerima data apa pun tanpa validasi (kita sepenuhnya mengandalkan validasi browser di `src/utils/validate.ts`).
   - *Rencana Bulan 4:* Backend NestJS **wajib** melakukan validasi ulang di sisi server menggunakan *Data Transfer Object* (DTO) dan `class-validator`.
3. **Paginasi & Header Metadata:**
   - *Sekarang:* Total data dibaca dari header khusus `X-Total-Count`.
   - *Rencana Bulan 4:* Tribe akan memutuskan apakah tetap memakai header `X-Total-Count` atau membungkus respons dalam *envelope* `{ data: [...], total: 24, page: 1, limit: 6 }`.
4. **Format Pesan Kesalahan (*Error Response Body*):**
   - *Sekarang:* `json-server` mengembalikan HTML atau string sederhana saat error 404.
   - *Rencana Bulan 4:* NestJS mengembalikan format standar JSON `{ statusCode: 404, message: "Produk dengan ID 99 tidak ditemukan", error: "Not Found" }`.

---

### 4. Mencatat Keputusan Arsitektur di `docs/decision-log.md`

Pastikan file `docs/decision-log.md` mencatat ringkasan keputusan teknis yang diambil tribe sepanjang Bulan 3:
1. **Standar Styling:** Tailwind CSS v4 dipilih untuk kecepatan pengembangan dan eliminasi konflik nama class.
2. **Arsitektur Validasi:** Menggunakan fungsi murni terpisah di `src/utils/validate.ts` untuk memisahkan logika dari JSX.
3. **State Filter:** Menggunakan URL Search Params via `useSearchParams` agar halaman *bookmarkable* dan tahan refresh.
4. **Arsitektur Notifikasi:** Menggunakan Context API dengan pemisahan 3 file (`ToastContext`, `ToastProvider`, `useToast`) untuk mendukung Vite Fast Refresh dan isolasi dependensi.

---

## Verifikasi & Pengujian Dokumen

1. Periksa apakah seluruh nama field di tabel kontrak API (misalnya `merchant_name`, `category_id`) menggunakan format `snake_case` yang konsisten dengan basis data `db.seed.json`.
2. Pastikan file `docs/kontrak-api.md` sudah di-commit ke Git.

---

**Lanjut ke:** `04c-code-audit-dan-persiapan-showcase.md` (Audit Kualitas Kode & Persiapan Showcase Akhir Bulan 3)
