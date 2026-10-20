# 4.0c Konsolidasi & Refactor — Rapikan Sebelum Showcase

## Tujuan sesi ini

Merapikan seluruh kode Katalog UMKM v1 sebelum showcase akhir bulan. Ini bukan sesi materi baru — ini sesi **memoles** dan **refleksi**.

## Yang perlu dilakukan

### 1. Rapikan import

Cek semua file — ada import yang tidak terpakai? Hapus. Oxlint biasanya sudah mengingatkan, tapi cek manual juga.

```tsx
// ❌ Import yang tidak terpakai
import { useState, useEffect, useCallback } from 'react'  // useCallback tidak dipakai

// ✅ Bersih
import { useState, useEffect } from 'react'
```

### 2. Hapus kode mati

- `console.log` yang ditinggal dari debugging
- Komentar TODO yang sudah diselesaikan
- File `src/data/products.ts` (hardcode dari Slice 0 — sudah diganti API)

### 3. Cek konsistensi penamaan

| Apa | Konvensi | Contoh |
|---|---|---|
| Komponen | PascalCase | `ProductCard`, `ProductsPage` |
| File komponen | PascalCase.tsx | `ProductCard.tsx` |
| Variabel/fungsi | camelCase | `handleDelete`, `isLoading` |
| Tipe/interface | PascalCase | `Product`, `ProductCardProps` |
| Field data dari API | snake_case | `category_id`, `merchant_name` |
| Folder | kebab-case | `api/`, `types/`, `errors/` |

### 4. Tulis README singkat

Buat atau perbarui `README.md` di root project:

```markdown
# Katalog UMKM

Mini Katalog UMKM — proyek belajar React + TypeScript (Bulan 2).

## Fitur
- Menampilkan daftar produk UMKM
- Menambah produk baru
- Mengedit harga dan stok produk
- Menghapus produk
- Halaman detail produk

## Cara menjalankan

```bash
npm install
npm run dev
```

Buka `http://localhost:5173` di browser.

## Tech stack
- React + TypeScript
- Vite
- json-server (API palsu)
```

### 5. Cek semua halaman berfungsi

Jalankan `npm run dev` dan cek manual:

- [ ] Halaman utama menampilkan daftar produk
- [ ] Klik nama produk → halaman detail muncul
- [ ] Tambah produk lewat form → produk baru muncul di daftar
- [ ] Edit harga/stok → perubahan tersimpan
- [ ] Hapus produk → produk hilang dari daftar
- [ ] Matikan API → pesan error muncul, bukan halaman kosong
- [ ] Refresh halaman detail → data tetap tampil (routing benar)

### 6. Jalankan linter

```bash
npm run lint
```

Perbaiki semua warning/error yang muncul sebelum showcase.

## Persiapan Showcase

**Format showcase:**
- Setiap peserta/pasangan mendemokan Katalog mereka ke tribe (~5 menit per orang)
- Tunjukkan: fitur yang jalan, satu bagian kode yang kamu bangga, satu hal yang masih bikin bingung
- Saling kasih peer feedback (bukan penilaian)

**Yang bisa ditunjukkan:**
- Demo live Katalog (tambah, edit, hapus, navigasi)
- Buka tab Network saat fetch data — jelaskan apa yang terjadi
- Tunjukkan satu PR yang sudah di-review
- Ceritakan satu bug yang ditemukan dan cara menyelesaikannya

## Refleksi Akhir Bulan 2

Jawab (untuk diri sendiri atau pasangan):
1. Konsep apa yang paling sulit di Bulan 2? Sudah lebih paham sekarang?
2. Kalau harus menjelaskan "apa itu React" ke teman yang belum pernah coding, apa yang akan kamu bilang?
3. Apa yang ingin kamu pelajari lebih dalam di Bulan 3?

---

Selamat — **Mini Katalog UMKM v1 selesai!** 🎉

Bulan 3 akan menambahkan kategori, validasi form, pencarian/filter, pagination, dan kontrak API. Lanjut ke folder `2-React-Lanjutan`.
