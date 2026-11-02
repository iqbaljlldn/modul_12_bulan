# 02a. Dekomposisi & Pengenalan Pola dalam Bisnis UMKM

**Minggu 2: Computational Thinking & Algoritma | Sesi 1 (Senin)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Peta Dekomposisi & Pola Bisnis UMKM (2 Proses Utama)

---

## 1. Mengapa Ini Penting?

Sebagian besar kegagalan dalam pembuatan aplikasi bukan karena programmer tidak tahu cara mengetik kode, melainkan karena mereka mencoba menyelesaikan masalah besar yang rumit sekaligus dalam satu kepala.

Komputer tidak bisa memproses instruksi abstrak seperti: *"Bikin fitur toko online yang canggih."*  
Komputer hanya bisa mengeksekusi instruksi kecil, spesifik, dan bertahap.

Dua pilar pertama Computational Thinking—**Dekomposisi** dan **Pengenalan Pola**—adalah pisau bedah kita untuk memotong masalah raksasa menjadi potongan-potongan balok lego yang mudah dirakit dan dipahami.

---

## 2. Pilar 1: Dekomposisi (Memecah Masalah Jadi Bagian Kecil)

Dekomposisi adalah seni memecah satu proses besar menjadi beberapa sub-proses, lalu memecahnya lagi sampai ke tingkat instruksi terkecil yang mandiri (*atomic step*).

### Studi Kasus: Proses "Pemesanan Produk via WhatsApp"

```text
                       PROSES PEMESANAN KATALOG UMKM
                     ┌───────────────┴───────────────┐
                     ▼                               ▼
             1. EKSPLORASI PRODUK            2. PEMESANAN VIA WHATSAPP
        ┌────────────┴────────────┐             ┌────────────┴────────────┐
        ▼                         ▼             ▼                         ▼
   1.1 Buka Link Toko        1.2 Filter Kategori 2.1 Cek Stok Barang   2.2 Buka Chat WA
```

Jika kamu melihat struktur di atas, membangun "fitur filter kategori produk" jauh lebih mudah dibayangkan dan dirancang daripada memikirkan "seluruh sistem belanja".

---

## 3. Pilar 2: Pengenalan Pola (Menemukan Logika yang Berulang)

Setelah membedah masalah, kita mencari: **bagian mana yang polanya mirip atau berulang?**

Dalam rekayasa perangkat lunak, jika ada dua hal yang memiliki pola sama, kita tidak perlu membuat solusinya dua kali. Kita cukup membuat satu solusi yang bisa dipakai berulang kali (*reusable logic*).

### Contoh Pola di Bisnis UMKM:

| Aktivitas Nyata | Pola Logika di Balik Layar |
|---|---|
| **Warung Mie:** Pembeli pesan 1 porsi mie ayam | Kurangi stok mie mentah sebanyak 1 |
| **Toko Baju:** Pembeli pesan 1 kaos oblong | Kurangi stok kaos ukuran M sebanyak 1 |
| **Toko Kue:** Pembeli pesan 1 toples nastar | Kurangi stok toples nastar sebanyak 1 |

Ketiga bisnis di atas menjual produk yang sangat berbeda, tetapi bagi komputer, polanya identik:
```text
POLA: [Pengurangan Stok]
1. Periksa apakah stok_tersedia >= jumlah_dipesan
2. JIKA ya: kurangi stok_tersedia sebanyak jumlah_dipesan
3. JIKA tidak: tolak pesanan dengan pesan "Maaf, Stok Habis"
```

---

## 4. Workshop Praktik Squad (60 Menit)

Hari ini setiap squad akan membedah **2 Proses Bisnis Utama Platform UMKM**:

1. **Proses 1: Pembeli Memesan Produk via WhatsApp**  
   (Dari pembeli membuka katalog link toko, memilih produk, mengecek stok, hingga sistem membuatkan template pesan otomatis dan membuka aplikasi WhatsApp penjual).
2. **Proses 2: Pedagang Menambah & Mengelola Stok Produk**  
   (Dari pedagang membuka dashboard toko, mengisi form nama/harga/kategori, mengisi stok awal, hingga barang tampil di katalog).

### Langkah Pengerjaan Tim:
1. **Langkah 1 (Dekomposisi Bertahap - 30 Menit):**  
   Pecah masing-masing dari kedua proses di atas menjadi urutan langkah runtut (**minimal 6 sampai 8 langkah per proses**). Jangan melompat terlalu cepat!
2. **Langkah 2 (Temukan 1 Pola Berulang - 20 Menit):**  
   Identifikasi minimal **1 pola logika berulang** yang ada pada kedua proses tersebut (misal: pola validasi "apakah data yang diisi kosong atau tidak", atau pola "menampilkan pesan konfirmasi ke layar").
3. **Langkah 3 (Uji Silang - 10 Menit):**  
   Minta squad sebelah membaca alur dekomposisi timmu. Apakah mereka bisa memahami urutan langkahnya tanpa kamu jelaskan secara lisan?

---

## 5. Output Sesi

Kumpulkan dokumen Markdown atau foto peta catatan tim yang memuat:
1. Rincian dekomposisi untuk **Proses 1** (6–8 langkah bertahap).
2. Rincian dekomposisi untuk **Proses 2** (6–8 langkah bertahap).
3. 1 Analisis pola logika berulang yang ditemukan lengkap dengan penjelasannya.

---

## 6. Tugas Mandiri (Individual)

- **Sifat:** Individu (dikerjakan sendiri di luar jam kelas)
- **Target Waktu:** 20 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_02a.md`

### Instruksi:
1. Pilih satu proses jual-beli sederhana yang ada di warung/toko dekat rumahmu (misal: proses membeli tabung gas elpiji 3 kg atau membeli pulsa listrik).
2. Tuliskan dekomposisi proses tersebut dalam **6 sampai 8 langkah runtut**.
3. Sebutkan 1 pola pengecekan (*validasi*) yang selalu terjadi pada proses tersebut.

### Contoh Hasil yang Diharapkan:
```markdown
# Tugas Mandiri 02a — Dekomposisi Proses Jual-Beli Warung
Nama: [Nama Kamu]
Proses: Membeli Gas Elpiji 3 Kg di Warung Madura

## 1. Dekomposisi Langkah (7 Langkah Runtut):
1. Pembeli datang membawa tabung gas kosong 3 kg dan uang tunai.
2. Penjual memeriksa fisik tabung kosong (memastikan tidak bocor/rusak parah).
3. Penjual mengecek stok ketersediaan tabung gas isi 3 kg di tumpukan warung.
4. JIKA stok habis, penjual mengabarkan ke pembeli dan proses selesai.
5. JIKA stok ada, penjual menimbang/memeriksa segel karet tabung baru.
6. Pembeli menyerahkan uang pas Rp 22.000 ke penjual.
7. Penjual menyerahkan tabung gas baru dan menyimpan tabung kosong ke rak penampungan.

## 2. Pola Pengecekan Logika:
Pola Validasi Ketersediaan: Cek kondisi syarat (apakah ada tabung isi tersedia?), jika ya lanjutkan transaksi, jika tidak hentikan transaksi secara sopan.
```

---

## 7. Cek Pemahaman Diri

1. Apa bahayanya jika seorang pengembang software langsung membuat antarmuka (UI) tanpa melakukan dekomposisi proses bisnis terlebih dahulu?
2. Sebutkan contoh pola logika yang sama antara proses "Cek Pulsa HP" dan proses "Cek Saldo Rekening Bank"!

---

Lanjut ke: **[02b-abstraksi-dan-algoritma.md](02b-abstraksi-dan-algoritma.md)**
