# 0.1 Tentang Modul Ini

## Cara belajar di program ini berbeda dari kelas biasa

Kalau di sekolah biasanya begini:

```text
Bulan ini belajar teori X → ujian → lanjut topik baru
```

Di sini:

```text
Kita butuh capability X untuk menyelesaikan bagian produk Y
  → konsep X diajarkan secukupnya
  → langsung dipraktikkan di produk asli
  → direview
  → lanjut
```

**Produk yang kita bangun bertahap:** Mini Katalog UMKM — aplikasi kecil untuk menampilkan, menambah, mengedit, dan menghapus produk jualan UMKM. Produk ini hidup sejak hari pertama, dan tumbuh sedikit demi sedikit lewat potongan kerjaan kecil yang kita sebut **slice**.

## Apa itu "slice"?

Satu **slice** = satu potongan kerja kecil yang bisa langsung dicoba dan dilihat hasilnya, dari tampilan sampai data. Bukan "belajar semua teori dulu, baru praktik di akhir".

Modul ini mencakup dua bulan pembelajaran frontend:
- **Bulan 2 (`1-TypeScript-React-Dasar`):** Slice 0-4 (Mini Katalog UMKM v1)
- **Bulan 3 (`2-React-Lanjutan`):** Slice 5-8 (Mini Katalog UMKM v2)

Tahap awal (Bulan 2) dibagi 5 slice:

| # | Slice | Isinya |
|---|---|---|
| 0 | Katalog tampil | Daftar produk muncul di halaman (data masih hardcode) |
| 1 | Katalog dari API | Data diambil dari server (bukan hardcode lagi) |
| 2 | Tambah produk | Ada form untuk menambah produk baru |
| 3 | Edit & hapus | Produk bisa diubah dan dihapus |
| 4 | Halaman detail | Klik produk → pindah ke halaman detailnya sendiri |

Tiap slice, kamu akan: baca konsep singkat → coba kode → commit → **Pull Request (PR)** → direview temen → revisi kalau ada masukan → merge → tunjukkan hasilnya (demo kecil).

## Kenapa harus tahu ini dari awal

Supaya kamu tidak bingung kenapa "belum belajar semua React" tapi sudah disuruh bikin form. Memang begitu maksudnya — kita belajar sambil membangun, bukan belajar dulu baru membangun.

## Sebelum lanjut

Pastikan kamu sudah selesai:
- **Bulan 1 — Fondasi Pra-Coding** (`modul-pra-coding-bulan1`): Computational Thinking, AI Literacy, Wireframe & UX, Value Proposition Canvas, dan kolaborasi Git.
- **Pre-class**: HTML, CSS, Git/GitHub, dan JavaScript (termasuk `fetch` dan `async/await`).
- Kalau ada bagian pre-class yang masih samar (terutama `fetch`, `Promise`, dan `async/await`), bilang ke mentor/pasanganmu **sekarang**, sebelum lanjut ke bab berikutnya. Modul React bootcamp juga bisa dibuka lagi kapan saja sebagai rujukan.

Lanjut ke: **02-setup-starter.md**
