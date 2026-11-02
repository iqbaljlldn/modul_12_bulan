# Latihan Tambahan (Stretch) — Bulan 2

Untuk murid yang sudah menyelesaikan Slice 0-4 lebih cepat dari target squad-nya. **Sifat latihan ini opsional (tidak wajib)**, dan bukan pengganti aktivitas pairing — selalu dahulukan membantu rekan satu squad yang masih berjuang sebelum mengeksplorasi tantangan ini!

---

## Ide Tantangan Stretch (Eksplorasi Mandiri)

1. **Sorting Sederhana di Sisi Klien:**  
   Tambahkan dua tombol untuk mengurutkan daftar produk berdasarkan harga (*Termurah → Termahal* atau *Termahal → Termurah*). Lakukan pengurutan murni di memori React menggunakan salinan array `[...products].sort()`, tanpa mengubah request ke API.
2. **Indikator Badge Stok Kritis:**  
   Tampilkan badge peringatan warna kuning (misalnya teks *"Stok Menipis"*) jika jumlah `stock` berada di antara angka 1 sampai 5, sebagai pembeda yang jelas dari kondisi *"Stok Habis"* (`stock === 0`).
3. **Modal Dialog Konfirmasi Kustom:**  
   Ganti dialog kaku bawaan browser `window.confirm()` dengan komponen modal kustom `ConfirmDialog.tsx` yang memiliki tombol *"Ya, Hapus"* dan *"Batal"* dengan gaya visual kartu yang selaras.
4. **Efek Loading Skeleton:**  
   Alih-alih menampilkan teks biasa *"Sedang memuat katalog..."*, coba rancang 3 kotak abu-abu beranimasi denyut (*pulse skeleton*) yang meniru bentuk kartu produk asli saat data sedang di-fetch.
5. **Format Tanggal Lokal Indonesia:**  
   Tampilkan informasi tanggal pembuatan produk (`created_at`) di halaman detail menggunakan pustaka standar browser `Intl.DateTimeFormat('id-ID', { dateStyle: 'long' })` sehingga teks tampil rapi (contoh: *"15 Januari 2026"*).
6. **Eksplorasi Dokumentasi `json-server` 0.17.x:**  
   Buka dokumentasi resmi `json-server` versi 0.17.x (ingat, bukan versi 1.x!). Pelajari mengapa fitur query bawaan seperti `_expand` dan `_embed` sengaja dihindari di proyek ini demi mempersiapkan kita menghadapi arsitektur REST API murni di NestJS (Bulan 4).

---

## Yang TIDAK Perlu Dikerjakan Dulu

- **Fitur Kategori Dinamis:** Pembahasan relasi kategori dan filter kategori baru akan kita mulai secara mendalam di Bulan 3 (Slice 5). Jangan mendahului membuat tabel kategori sendiri agar struktur datamu tetap sinkron dengan squad lain.
- **Migrasi Styling ke Tailwind:** Standar desain dan tata kelola styling bersama (Tailwind CSS v4) akan diresmikan bersama tribe di awal Bulan 3. Jangan mengubah seluruh CSS menjadi Tailwind sekarang agar tidak terjadi kerja ganda.
