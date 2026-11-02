# 4.0c Konsolidasi & Refactor — Rapikan Sebelum Showcase Akhir Bulan 2

## Tujuan Sesi Ini

Membersihkan seluruh basis kode Mini Katalog UMKM v1 (Slice 0-4), memastikan tidak ada peringatan linter (`oxlint`) atau error build TypeScript, mengaudit konsistensi penamaan berkas dan tipe data, serta mempersiapkan demo produk untuk **Sprint Review 4 / Showcase Akhir Bulan 2**.

> Sesi ini bukan tentang menambah fitur baru. Sesi ini melatih disiplin profesional seorang software engineer: memoles kode agar bersih (*clean code*), mudah dibaca oleh rekan tim, dan siap dilanjutkan ke Bulan 3.

---

## Aktivitas Terbimbing di Kelas (Blok 1, 10-15 Menit)

Mentor akan memandu checklist audit kualitas kode bersama di proyektor:
1. Menjalankan linter cepat `npm run lint` dan membedah arti pesan peringatan yang sering muncul.
2. Memeriksa impor yang tidak terpakai (*unused imports*) dan menghapus catatan sementara (`console.log`).
3. Memastikan berkas acuan statis sementara dari Slice 0 (`src/data/products.ts`) sudah dibersihkan sepenuhnya.
4. Menjalankan `npm run build` (`tsc -b && vite build`) untuk memverifikasi bahwa seluruh tipe data TypeScript valid 100%.

---

## Checklist Audit Kualitas Kode (Blok 2)

Kerjakan bersama pasangan pairing sebelum memasuki tugas mandiri:

### 1. Pembersihan Impor & Variabel Mati

Periksa seluruh berkas di dalam folder `src/`. Pastikan tidak ada sisa impor yang ditinggalkan:

```tsx
// ❌ Buruk: Menyisakan hook atau tipe yang tidak terpakai
import { useState, useEffect, useCallback } from 'react' // useCallback tidak pernah dipanggil!

// ✅ Bersih: Hanya mengimpor apa yang benar-benar digunakan
import { useState, useEffect } from 'react'
```

### 2. Standar Konsistensi Penamaan Tribe

Cocokkan seluruh berkas dan kode kalian dengan standar penamaan berikut:

| Kategori | Standar Konvensi | Contoh di Proyek Kita |
|---|---|---|
| **Komponen React** | PascalCase | `ProductCard`, `ProductForm`, `ProductsPage` |
| **Berkas Komponen** | PascalCase.tsx | `src/components/ProductCard.tsx` |
| **Fungsi & Variabel** | camelCase | `handleDeleteProduct`, `isLoading`, `formatRupiah` |
| **Tipe & Interface** | PascalCase | `Product`, `CreateProductInput`, `ApiError` |
| **Field Data API Backend** | snake_case | `category_id`, `merchant_name`, `created_at` |
| **Folder Modul** | kebab-case | `src/components/`, `src/pages/`, `src/api/` |

---

### 3. Uji Menyeluruh Alur Fitur (Smoke Test)

Lakukan pengujian manual dari awal hingga akhir di browsermu:

- [ ] **Katalog Utama (Slice 0 & 1):** Daftar produk tampil rapi dari API `json-server`, harga berformat Rupiah, dan indikator badge status terlihat jelas.
- [ ] **Tambah Produk (Slice 2):** Form tambah produk dapat diisi, tombol berubah menjadi disabled saat proses simpan, dan produk baru langsung muncul di daftar tanpa refresh.
- [ ] **Edit Produk Inline (Slice 3):** Klik tombol "Edit" hanya membuka form edit pada kartu yang bersangkutan. Nilai baru berhasil disimpan ke server.
- [ ] **Hapus Produk (Slice 3):** Muncul dialog konfirmasi browser `window.confirm`. Jika disetujui, produk hilang dari daftar dan terhapus dari `db.json`.
- [ ] **Halaman Detail (Slice 4):** Klik nama produk membuka halaman `/products/:id`. Refresh halaman detail tetap menampilkan data dengan aman.
- [ ] **Penanganan 404 (Slice 4):** Akses manual ke `/products/999` memunculkan pesan ramah *"Produk tidak ditemukan"* disertai tombol kembali ke katalog utama.
- [ ] **Penanganan Server Down:** Matikan API palsu sementara (`Ctrl+C`), aplikasi menampilkan pesan error yang ramah dan tidak meledak menjadi layar putih.

---

### 4. Eksekusi Pengujian Otomatis

Jalankan perintah ini di terminal dan pastikan tidak ada error merah:

```bash
# 1. Jalankan linter oxlint
npm run lint

# 2. Jalankan kompilasi TypeScript dan build produksi Vite
npm run build
```

---

## Panduan Showcase Akhir Bulan 2 (Sabtu)

Pada sesi Sprint Review hari Sabtu, tiap squad akan mendemokan Mini Katalog UMKM v1 di depan seluruh tribe (durasi 10-12 menit per squad):

1. **Live Demo Fitur (5 menit):** Tunjukkan alur lengkap: tambah produk UMKM baru → ubah harganya secara inline → klik nama barang untuk melihat detailnya → hapus produk contoh.
2. **Sorotan Kode Kebanggaan (3 menit):** Tunjukkan 1 bagian kode yang paling kalian pahami dan banggakan (misalnya penanganan `ApiError` 404 atau isolasi state `isEditing`).
3. **Pelajaran Berharga & Tantangan (2 menit):** Ceritakan 1 kendala atau bug paling menarik yang berhasil kalian pecahkan bersama selama Bulan 2.
4. **Tanya Jawab & Peer Feedback (2 menit):** Rekan squad lain memberikan apresiasi dan masukan membangun.

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan secara mandiri di kelas. Simpan hasilnya di:  
`tugas/squad-<nomor>/<nama-kamu>/tugas_04c.md`

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Tuliskan identitas diri (Nama, Squad, Tanggal).
3. Buka terminal di laptopmu, jalankan `npm run lint` dan `npm run build`. Salin baris output sukses yang dihasilkan terminal ke dalam berkas tugas.
4. Tuliskan refleksi pribadi singkat (3-5 kalimat) menjawab pertanyaan:
   - Dari seluruh materi Bulan 2 (JSX, Props, State, useEffect, Fetch API, Form Controlled, PATCH/DELETE, dan React Router), konsep mana yang awalnya terasa paling sulit tetapi sekarang sudah kamu pahami?
   - Mengapa proses refactoring dan membersihkan kode mati (*dead code*) sebelum showcase sangat penting bagi reputasi sebuah tim pengembang software?
5. Ajukan Pull Request ke repositori squad untuk dimerge sebelum hari Sabtu.

### Contoh Format Hasil (`tugas_04c.md`)

```markdown
# Tugas Mandiri 04c — Konsolidasi & Code Audit
Nama: Rahmat Hidayatullah
Squad: Squad 1
Tanggal: 23 November 2026

## 1. Bukti Output Terminal Build & Lint
```text
$ npm run lint
oxlint: 0 errors, 0 warnings found.

$ npm run build
vite v6.x.x building for production...
✓ 34 modules transformed.
dist/index.html                   0.48 kB │ gzip: 0.31 kB
dist/assets/index-D1a2B3c.css     2.15 kB │ gzip: 0.85 kB
dist/assets/index-X9y8Z7w.js    158.42 kB │ gzip: 51.20 kB
✓ built in 312ms
```

## 2. Refleksi Pribadi Akhir Bulan 2
- Konsep yang awalnya paling membingungkan bagi saya adalah `useEffect` dan dependency array `[id]`. Awalnya saya tidak mengerti mengapa fetch data tidak boleh ditaruh langsung di badan fungsi dan mengapa halaman detail sempat tidak mau mengupdate data saat URL berganti. Setelah dibantu mentor dengan analogi pelayan restoran dan praktik langsung kasus 404, sekarang saya paham betul bagaimana React mengontrol siklus hidup komponennya.
- Membersihkan kode mati dan merapikan impor sangat penting karena kode yang berantakan akan menyulitkan rekan satu squad yang harus membaca atau melanjutkan fitur kita di Bulan 3. Kode yang lolos lint dan build membuktikan bahwa tim kita bekerja secara profesional, teliti, dan bertanggung jawab terhadap kualitas produk yang diserahkan ke pengguna.
```

---

Selamat! **Mini Katalog UMKM v1 tuntas diselesaikan dengan standar software engineering yang solid!** 🎉  
Setelah sesi Sprint Review dan Retrospektif hari Sabtu, kita siap melangkah ke **Bulan 3: React Lanjutan (Slice 5 - 8)** di folder `2-React-Lanjutan/`.
