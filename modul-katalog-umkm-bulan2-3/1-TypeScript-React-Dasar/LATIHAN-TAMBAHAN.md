# Latihan Tambahan (Stretch)

Untuk peserta yang sudah selesai Slice 0-4 lebih cepat dari squad-nya. **Bukan wajib**, dan bukan pengganti pairing — tetap bantu temen yang belum selesai dulu kalau ada yang butuh.

## Ide latihan

1. **Sorting sederhana**: tambahkan tombol untuk mengurutkan daftar produk berdasarkan harga (murah → mahal / mahal → murah), tanpa mengubah API. Cukup `.sort()` di sisi React.
2. **Badge stok menipis**: tampilkan badge kuning kalau `stock` di bawah angka tertentu (misal 5), sebagai pembeda dari "stok habis" (0) yang sudah ada.
3. **Ganti `window.confirm` dengan modal custom**: bikin komponen `ConfirmDialog` sederhana untuk konfirmasi hapus, menggantikan dialog bawaan browser yang kaku.
4. **Loading skeleton**: alih-alih teks "Memuat...", coba bikin tampilan kartu abu-abu berkedip (skeleton) — pengalaman lebih halus.
5. **Format tanggal**: tampilkan `created_at` di halaman detail, diformat jadi "12 Januari 2026" (bukan format ISO mentah). Cari cara pakai `Intl.DateTimeFormat` (mirip `Intl.NumberFormat` yang sudah dipakai di `formatRupiah`).
6. **Baca kode `json-server`**: buka dokumentasi resminya, cari tahu apa itu `_embed` dan kenapa itu juga tidak cocok dipakai untuk relasi `category_id` di project ini (mirip alasan `_expand` di README starter).

## Yang TIDAK perlu dikerjakan dulu

- Kategori produk yang sesungguhnya (baru masuk di Bulan 3, Slice 5) — jangan buru-buru bikin sendiri, nanti ada kemungkinan bentrok dengan cara yang dipakai bersama.
- Styling besar-besaran (Tailwind/CSS Module) — standar tribe baru diputuskan di Bulan 3, Slice 5. Kalau kamu ubah besar-besaran sekarang, nanti kerja dua kali.
