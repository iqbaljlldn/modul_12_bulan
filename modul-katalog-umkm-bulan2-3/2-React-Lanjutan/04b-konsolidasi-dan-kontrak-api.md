# 2.4b Slice 8 — Konsolidasi & Kontrak API Tertulis

> **Bacaan wajib sebelum sesi:** Modul React Programmer Pit — **Bab 4.2** (Advanced Styling) & Dokumentasi API Katalog.  
> **Prasyarat:** Menyelesaikan `04a` (Desain Responsif) dan seluruh Slice 0-7.

---

## Tujuan Slice Ini

Ini bukan slice untuk membuat fitur baru — ini adalah slice untuk **merapikan seluruh kode** dan **menuliskan Kontrak API resmi (`docs/kontrak-api.md`)**.

Setelah slice ini selesai:
1. **Mini Katalog UMKM v2** tuntas dan siap didemokan (*production-ready MVP*).
2. Dokumen **Kontrak API** menjadi **spesifikasi resmi** yang disepakati squad dan wajib dipenuhi oleh Chapter Backend saat membangun REST API menggunakan NestJS & PostgreSQL di Bulan 4!

---

## Kenapa Ini Penting untuk Produk?

Hingga akhir Bulan 3, "kontrak" antara frontend dan backend mock (`json-server`) hanya tersimpan di kepala masing-masing developer atau tersebar di file-file `src/api/`.

Sebelum backend sungguhan dibangun bulan depan, kontrak ini **harus disepakati bersama oleh seluruh tribe**:
- **Chapter Backend** tahu persis nama endpoint, method HTTP, format payload JSON, dan kode status response yang diharapkan oleh frontend.
- Jika ada perilaku frontend yang ternyata mengandalkan trik khusus `json-server` (yang tidak standar di backend nyata), hal itu **terdeteksi sekarang**, bukan di tengah jalan Bulan 4 ketika integrasi sudah macet.

---

## Langkah demi Langkah Implementasi (Blok 1 & Blok 2 Squad Consensus)

### 1. Audit Endpoint dari Kode Frontend Sungguhan

Buka setiap file di dalam folder `src/api/` dan `src/types/product.ts`:
- `src/api/products.ts`
- `src/api/categories.ts`
- `src/api/http.ts`

Catat setiap request dan field payload yang benar-benar dikirimkan oleh frontend kita. Jangan menebak dari ingatan — buka kode dan teliti baris demi baris!

---

### 2. Mengisi Dokumen `docs/kontrak-api.md`

Buat atau buka file `docs/kontrak-api.md` di root repo. Lengkapi tabel spesifikasi endpoint sesuai kode aktual dan skema `db.seed.json`:

#### Tabel Spesifikasi Endpoint Produk (`/products`)

| Method | Endpoint Path | Query Params / Body | Status Sukses | Respons Sukses (JSON / Header) | Status Error & Kondisi |
|---|---|---|---|---|---|
| `GET` | `/products` | Query: `q`, `category_id`, `_sort`, `_order`, `_page`, `_limit` | `200 OK` | Array `Product[]`, Total di Header `X-Total-Count` | `500` (Kesalahan Server) |
| `GET` | `/products/:id` | Param: `id` (number) | `200 OK` | Objek `Product` tunggal | `404 Not Found` (Produk tidak ada) |
| `POST` | `/products` | Body JSON: `CreateProductInput` (`name`, `description`, `price`, `stock`, `category_id`, `merchant_name`, `status`: `'active' \| 'draft'`) | `201 Created` | Objek `Product` baru dengan `id` & `created_at` | `400 Bad Request` (Validasi gagal) |
| `PATCH` | `/products/:id` | Param: `id`, Body JSON: `UpdateProductInput` (`Partial<Pick<Product, 'price' \| 'stock' \| ...>>`) | `200 OK` | Objek `Product` yang sudah diperbarui | `400` (Data tidak valid), `404` (Tidak ditemukan) |
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
   - *Rencana Bulan 4 (NestJS + PostgreSQL):* Backend akan menggunakan relasi tabel (*Foreign Key* + SQL `JOIN`) sehingga endpoint `GET /products` dapat langsung menyertakan objek relasi `{ id: 1, name: "Keripik Tempe", category: { id: 1, name: "Kuliner" } }`.
2. **Validasi Input & `created_at`:**
   - *Sekarang:* `json-server` menerima data apa pun tanpa validasi (kita mengandalkan `src/utils/validate.ts`), dan `created_at` sementara diisi dari browser.
   - *Rencana Bulan 4:* Backend NestJS **wajib** melakukan validasi ulang di sisi server menggunakan *Data Transfer Object* (DTO) + `class-validator` serta mengisi timestamp `created_at` di server/database.
3. **Paginasi & Header Metadata:**
   - *Sekarang:* Total data dibaca dari header khusus `X-Total-Count` (fitur `json-server@0.17.4`).
   - *Rencana Bulan 4:* Tribe akan memutuskan apakah tetap memakai header `X-Total-Count` atau membungkus respons dalam *envelope* `{ data: [...], total: 24, page: 1, limit: 6 }`.
4. **Format Pesan Kesalahan (*Error Response Body*):**
   - *Sekarang:* `json-server` mengembalikan `{}` atau HTML sederhana saat error 404.
   - *Rencana Bulan 4:* NestJS mengembalikan format standar JSON `{ statusCode: 404, message: "Produk dengan ID 99 tidak ditemukan", error: "Not Found" }`.

---

### 4. Mencatat Keputusan Arsitektur Squad di `docs/decision-log.md`

Diskusikan bersama anggota squad di Blok 2 dan pastikan `docs/decision-log.md` mencatat konsensus keputusan teknis sepanjang Bulan 3:
1. **Standar Styling:** Tailwind CSS v4 dipilih untuk kecepatan pengembangan dan eliminasi konflik nama class.
2. **Arsitektur Validasi:** Menggunakan fungsi murni terpisah (`validate`, `validateEdit`) di `src/utils/validate.ts` untuk memisahkan logika dari JSX.
3. **State Filter:** Menggunakan URL Search Params via `useSearchParams` agar halaman *bookmarkable* dan tahan refresh (`F5`).
4. **Arsitektur Notifikasi:** Menggunakan Context API dengan pemisahan 3 file (`ToastContext`, `ToastProvider`, `useToast`) untuk mendukung Vite Fast Refresh dan isolasi dependensi.

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan individual lalu sinkronkan catatan hasilnya bersama squad, simpan di repositori proyekmu pada:  
`tugas/tugas_04b.md`

1. Tuliskan identitas diri (Nama, Squad, Tanggal).
2. Pastikan seluruh nama field di `docs/kontrak-api.md` (seperti `merchant_name`, `category_id`, `created_at`) memakai `snake_case` yang identik dengan `db.seed.json`.
3. Jawab singkat: perubahan apa yang paling berdampak pada kode frontend saat nanti backend NestJS mengganti format respons pagination atau menambah objek `category` di `/products`?
4. Commit `docs/kontrak-api.md`, `docs/decision-log.md`, dan `tugas/tugas_04b.md` lewat PR untuk direview rekan squad.

---

**Lanjut ke:** `04c-code-audit-dan-persiapan-showcase.md` (Audit Kualitas Kode & Persiapan Showcase Akhir Bulan 3)
