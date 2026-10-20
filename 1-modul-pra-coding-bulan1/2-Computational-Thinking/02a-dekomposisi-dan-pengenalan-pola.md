# 02a. Dekomposisi & Pengenalan Pola dalam Bisnis UMKM

**Minggu 2: Computational Thinking & Algoritma | Sesi 1 (Senin)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Peta Dekomposisi & Pola Bisnis UMKM (Dokumen / Sticky Notes)

---

## 1. Mengapa Ini Penting?

Sebagian besar kegagalan dalam pembuatan aplikasi bukan karena programmer tidak tahu sintaks coding, melainkan karena mereka mencoba menyelesaikan masalah besar yang ruwet sekaligus dalam satu kepala.

Komputer tidak bisa memproses instruksi abstrak seperti: *"Bikin fitur toko online yang canggih."*  
Komputer hanya bisa mengeksekusi instruksi kecil, spesifik, dan bertahap.

Dua pilar pertama Computational Thinking—**Dekomposisi** dan **Pengenalan Pola**—adalah pisau bedah kita untuk memotong masalah raksasa menjadi potongan-potongan balok lego yang mudah dirakit.

---

## 2. Pilar 1: Dekomposisi (Membedah Masalah)

Dekomposisi adalah seni memecah satu proses besar menjadi beberapa sub-proses, lalu memecahnya lagi sampai ke tingkat instruksi terkecil yang mandiri (*atomic step*).

### Studi Kasus: Proses "Belanja di Katalog Online"

```text
                               PROSES BELANJA ONLINE
                     ┌───────────────────┴───────────────────┐
                     ▼                                       ▼
             1. EKSPLORASI PRODUK                    2. TRANSAKSI & PEMBAYARAN
        ┌────────────┴────────────┐             ┌────────────┴────────────┐
        ▼                         ▼             ▼                         ▼
   1.1 Cari Kata Kunci      1.2 Filter Harga   2.1 Cek Stok Barang   2.2 Pilih Metode Bayar
```

Jika kamu melihat struktur di atas, membangun "fitur pencarian produk" jauh lebih mudah dibayangkan dan dikerjakan daripada memikirkan "seluruh sistem belanja".

---

## 3. Pilar 2: Pengenalan Pola (Menemukan Kesamaan & Reusable Logic)

Setelah membedah masalah, kita mencari: **bagian mana yang polanya mirip atau berulang?**

Dalam rekayasa perangkat lunak, jika ada dua hal yang memiliki pola sama, kita tidak perlu membuat solusinya dua kali. Kita cukup membuat satu solusi yang bisa dipakai ulang (*reusable*).

### Contoh Pola di Bisnis UMKM:

| Aktivitas Nyata | Pola Logika di Balik Layar |
|---|---|
| **Warung Mie:** Pelanggan beli 1 porsi mie ayam | Kurangi stok mie mentah sebanyak 1 |
| **Toko Baju:** Pelanggan beli 1 kaos oblong | Kurangi stok kaos ukuran M sebanyak 1 |
| **Toko Bangunan:** Pelanggan beli 1 sak semen | Kurangi stok sak semen sebanyak 1 |

Ketiga bisnis di atas terlihat sangat berbeda di dunia nyata, tetapi bagi komputer, polanya identik:
```text
POLA: [Pengurangan Stok]
1. Periksa apakah stok_tersedia >= jumlah_dipesan
2. JIKA ya: stok_tersedia = stok_tersedia - jumlah_dipesan
3. JIKA tidak: tolak pesanan dengan pesan "Stok Habis"
```

---

## 4. Workshop Praktik Squad (60 Menit)

Hari ini setiap squad akan membedah **3 Proses Bisnis Utama UMKM**:

1. **Proses A: Menerima & Memproses Pesanan Baru** (Dari pembeli klik order sampai barang siap dibungkus).
2. **Proses B: Manajemen Stok & Restok Barang** (Dari barang menipis, pesan ke pemasok, sampai barang masuk rak).
3. **Proses C: Layanan Pelanggan & Retur Barang Cacat** (Pelanggan menerima barang rusak, komplain, sampai diganti/refund).

### Langkah Pengerjaan:
1. **Langkah 1 (Dekomposisi Pohon - 30 Menit):**
   Gunakan kertas tempel (*sticky notes*) atau papan Miro/FigJam. Pecah masing-masing dari ketiga proses di atas menjadi minimal **3 level kedalaman**.
   - *Level 1:* Tahapan besar (contoh: Validasi Pesanan, Pembungkusan, Pengiriman).
   - *Level 2:* Langkah spesifik di tiap tahap.
   - *Level 3:* Titik pengecekan data (apa syarat agar langkah ini bisa lanjut?).
2. **Langkah 2 (Ekstraksi Pola - 20 Menit):**
   Temukan minimal **2 pola berulang** yang muncul di lebih dari satu proses (contoh: pola "verifikasi status", pola "pencatatan waktu kejadian/timestamp", atau pola "notifikasi ke pengguna").
3. **Langkah 3 (Review Rekan Sebelah - 10 Menit):**
   Tukar hasil dekomposisi dengan squad sebelah. Apakah mereka bisa memahami alurnya tanpa kamu jelaskan secara lisan?

---

## 5. Output Sesi: Peta Dekomposisi & Pola Bisnis UMKM

Kumpulkan dokumen Markdown atau foto peta sticky notes squad yang memuat:
1. Diagram pohon dekomposisi untuk 3 proses bisnis UMKM (minimal 8-12 langkah per proses).
2. Tabel analisis pola: daftar 2 pola logika berulang yang berhasil diidentifikasi lengkap dengan komponen logikanya.

---

## 6. Cek Pemahaman Diri

1. Apa bahayanya jika seorang pengembang software langsung membuat antarmuka (UI) tanpa melakukan dekomposisi proses bisnis terlebih dahulu?
2. Sebutkan satu contoh pola yang sama antara proses "Login Akun" dan proses "Memasukkan PIN Dompet Digital"!

Lanjut ke: **[02b-abstraksi-dan-algoritma.md](file:///home/iqbaal/gelombang-3/modul 12 bulan/modul-pra-coding-bulan1/2-Computational-Thinking/02b-abstraksi-dan-algoritma.md)**
