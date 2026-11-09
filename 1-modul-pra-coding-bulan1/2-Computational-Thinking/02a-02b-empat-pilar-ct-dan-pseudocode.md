# 02a & 02b. Empat Pilar Computational Thinking & Algoritma (Pseudocode)

**Minggu 2: Computational Thinking & Algoritma | Sesi Gabungan (Selasa)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Dokumen Terpadu 4 Pilar CT (Dekomposisi, Pola, Abstraksi, & Pseudocode) + Jembatan Kode JS

---

## 1. Mengapa Ini Penting?

Sebagian besar kegagalan dalam pembuatan aplikasi bukan karena programmer tidak tahu cara mengetik kode, melainkan karena mereka mencoba menyelesaikan masalah besar yang rumit sekaligus dalam satu kepala.

Komputer tidak bisa memproses instruksi abstrak seperti: *"Bikin fitur toko online yang canggih."*  
Komputer hanya bisa mengeksekusi instruksi kecil, spesifik, bertahap, dan tidak bermakna ganda (*unambiguous*).

Hari ini kita akan menguasai **4 Pilar Computational Thinking (CT)** secara utuh dalam satu alur menyambung:
1. **Dekomposisi:** Memecah masalah besar menjadi langkah-langkah kecil.
2. **Pengenalan Pola:** Menemukan logika serupa yang berulang.
3. **Abstraksi:** Menyaring data inti dan membuang detail yang tidak relevan (*noise*).
4. **Algoritma (Pseudocode):** Menyusun instruksi logika yang tegas menggunakan struktur bahasa Indonesia baku sebelum diterjemahkan menjadi kode JavaScript/TypeScript.

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

Jika kamu melihat struktur di atas, membangun *"fitur filter kategori produk"* atau *"cek stok barang"* jauh lebih mudah dibayangkan dan dirancang daripada memikirkan *"seluruh sistem belanja"* sekaligus.

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

## 4. Pilar 3: Abstraksi (Fokus pada Data Inti)

Setelah tahu langkah dan polanya, kita harus menentukan **data apa yang wajib dicatat sistem** dan **detail apa yang harus diabaikan**. Kemampuan menyaring fakta ini disebut **Abstraksi**.

### Contoh Kasus di Toko Kelontong:
Seorang pembeli datang membeli 2 kg beras:
- *Detail Nyata di Toko:* Pembeli memakai baju biru, naik motor matic, bercanda tentang cuaca panas, dan membayar dengan uang kertas Rp 50.000 yang agak lecek.
- *Abstraksi Sistem Kasir:*
  ```text
  ID_Barang      : BRG-001 (Beras Ramos)
  Jumlah_Beli    : 2
  Harga_Satuan   : Rp 14.000
  Total_Bayar    : Rp 28.000
  Uang_Diterima  : Rp 50.000
  Kembalian      : Rp 22.000
  ```

Warna baju, merek motor, dan leceknya uang kertas adalah *noise* yang sengaja dibuang. Sistem hanya menyimpan data yang berpengaruh pada perhitungan transaksi dan stok.

---

## 5. Pilar 4: Algoritma & Format Baku Pseudocode

Sebelum menulis kode JavaScript atau TypeScript di Bulan 2, kita menuliskan alur logika dalam bentuk **Pseudocode** (kode semu berbahasa Indonesia yang terstruktur). Jika logikamu dalam bahasa manusia saja masih rancu, menerjemahkannya ke kode komputer hanya akan memicu error.

Algoritma dibangun dari 3 blok dasar:
1. **Sekuensial:** Langkah berjalan berurutan dari atas ke bawah.
2. **Percabangan (Kondisional):** Mengambil keputusan berdasarkan kondisi.
3. **Perulangan (Looping):** Mengulang aksi selama syarat terpenuhi.

### Format Kata Kunci Baku Bahasa Indonesia:
Gunakan kata kunci kapital berikut agar logikamu seragam dan mudah dibaca:
- `MULAI` / `SELESAI`
- `MASUKKAN` / `TAMPILKAN`
- `JIKA ... MAKA ... LAINNYA ... AKHIR-JIKA`
- `UNTUK SETIAP ... LAKUKAN ... AKHIR-UNTUK`

### Contoh Pseudocode: Logika Pemesanan Produk via WhatsApp
```text
ALGORITMA BuatPesananWhatsApp
MULAI
    MASUKKAN nama_pembeli, nomor_wa_pembeli, id_produk, jumlah_beli

    AMBIL data_produk BERDASARKAN id_produk
    
    JIKA data_produk TIDAK DITEMUKAN MAKA
        TAMPILKAN "Error: Produk tidak ditemukan di katalog"
        SELESAI
    AKHIR-JIKA

    JIKA data_produk.stok < jumlah_beli MAKA
        TAMPILKAN "Maaf, stok hanya tersisa: " + data_produk.stok
        SELESAI
    LAINNYA
        HITUNG total_harga = data_produk.harga * jumlah_beli
        BUAT template_pesan = "Halo " + data_produk.nama_toko + ", saya " + nama_pembeli + " ingin memesan: " + data_produk.nama_produk + " sejumlah " + jumlah_beli + " pcs. Total: Rp " + total_harga
        BUKA_WHATSAPP DENGAN URL ("https://wa.me/" + data_produk.nomor_wa_toko + "?text=" + template_pesan)
        TAMPILKAN "Mengarahkan ke WhatsApp penjual..."
    AKHIR-JIKA
SELESAI
```

---

## 6. Workshop Praktik Squad Terpadu (60 Menit)

Agar ke-4 pilar langsung terpakai secara utuh tanpa memecah fokus, setiap squad akan membedah **1 Alur End-to-End Platform UMKM**: **"Alur Pemesanan via WhatsApp & Perhitungan Tagihan (Diskon + Ongkir)"**.

### Tahap 1: Dekomposisi & Pengenalan Pola (20 Menit)
1. **Dekomposisi (6–8 Langkah Runtut):**  
   Pecah proses **"Pembeli Memesan Produk di Katalog hingga Chat WhatsApp Terbuka"** menjadi 6 sampai 8 langkah berurutan. Jangan melompat terlalu cepat!
2. **Identifikasi 1 Pola Logika Berulang:**  
   Temukan minimal **1 pola pengecekan/validasi** yang sama antara proses *"Pembeli Memesan Produk"* dan proses *"Pedagang Menambah Produk Baru"* (misal: pola memeriksa apakah input kosong/tidak valid sebelum lanjut ke langkah berikutnya).

### Tahap 2: Abstraksi & Penulisan Pseudocode (25 Menit)
1. **Abstraksi Data Inti:**  
   Tuliskan variabel/data apa saja yang wajib ada untuk menghitung total bayar pembeli, dan sebutkan 2 contoh *noise* di dunia nyata yang tidak perlu dicatat aplikasi.
2. **Pseudocode Wajib — "Algoritma Hitung Diskon & Ongkir Warung":**  
   Tulis pseudocode dengan format baku (`MULAI`, `JIKA ... MAKA ... LAINNYA ... AKHIR-JIKA`, `SELESAI`) untuk aturan toko berikut:
   - Jika `total_belanja >= Rp 100.000`, berikan potongan diskon 10% (dengan batas **maksimal diskon Rp 20.000**).
   - Jika `jarak_km <= 3 km`, ongkir gratis (`Rp 0`). Jika lebih dari `3 km`, tarif ongkir adalah `Rp 2.500` per km kelebihannya.
   - Hitung `total_akhir` yang harus dibayarkan pembeli (`total_belanja - diskon + ongkir`).
3. **Tantangan Tambahan / Stretch Goal (Jika Waktu Masih Ada):**  
   Susun pseudocode perulangan (`UNTUK SETIAP ... LAKUKAN ... AKHIR-UNTUK`) untuk **"Algoritma Peringatan Stok Menipis"**: periksa daftar produk toko, dan jika `stok <= 3`, masukkan nama produk ke daftar *"Peringatan Restok Segera"*.

### Tahap 3: Uji Coba Manual / Dry Run Table (15 Menit)
Uji pseudocode Diskon & Ongkir buatan squad kalian dengan 3 skenario angka berikut untuk membuktikan tidak ada bug logika:

| Skenario | Total Belanja | Jarak (km) | Diskon Didapat | Biaya Ongkir | Total Akhir |
|---|---|---|---|---|---|
| **A** | Rp 50.000 | 2 km | Rp 0 | Rp 0 | Rp 50.000 |
| **B** | Rp 150.000 | 5 km | Rp 15.000 | Rp 5.000 | Rp 140.000 |
| **C** | Rp 300.000 | 1 km | Rp 20.000 (max) | Rp 0 | Rp 280.000 |

---

## 7. Output Sesi

Kumpulkan 1 dokumen Markdown squad yang memuat:
1. **Dekomposisi & Pola:** 6–8 langkah pemesanan via WhatsApp + 1 analisis pola validasi berulang.
2. **Abstraksi & Pseudocode:** Daftar variabel inti + teks Pseudocode lengkap *"Algoritma Hitung Diskon & Ongkir Warung"* (beserta kasus stok menipis jika dikerjakan).
3. **Tabel Dry Run:** Pembuktian perhitungan untuk Skenario A, B, dan C.

---

## 8. Tugas Mandiri (Individual): Jembatan ke Kode JavaScript

- **Sifat:** Individu (dikerjakan sendiri di luar jam kelas)
- **Target Waktu:** 25 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_02b.md`

> [!TIP]
> **Sentuhan Kode Mingguan (Jembatan Menuju Bulan 2):**  
> Ingat sintaks dasar JavaScript yang sudah kamu pelajari sebelumnya? Sekarang saatnya menyegarkan ingatan jarimu dengan menerjemahkan pseudocode Diskon & Ongkir yang sudah kalian rancang di kelas menjadi satu fungsi JavaScript sederhana!

### Instruksi:
1. Tuliskan satu fungsi JavaScript bernama `hitungTotalBayar(totalBelanja, jarakKm)`.
2. Gunakan percabangan `if` dan `else` sederhana untuk menghitung diskon dan ongkir sesuai aturan di atas.
3. Cocokkan hasil `console.log()` fungsi kodemu dengan tabel *Dry Run* (Skenario A, B, dan C).
4. Tuliskan kode JS tersebut dan hasil ujinya di file `tugas_02b.md`.

### Contoh Hasil yang Diharapkan:
````markdown
# Tugas Mandiri 02b — Jembatan Kode: Fungsi Diskon & Ongkir
Nama: [Nama Kamu]

## 1. Kode JavaScript Sederhana:
```javascript
function hitungTotalBayar(totalBelanja, jarakKm) {
  // 1. Hitung Diskon
  let diskon = 0;
  if (totalBelanja >= 100000) {
    diskon = totalBelanja * 0.10;
    if (diskon > 20000) {
      diskon = 20000;
    }
  }

  // 2. Hitung Ongkir
  let ongkir = 0;
  if (jarakKm > 3) {
    let kelebihanKm = jarakKm - 3;
    ongkir = kelebihanKm * 2500;
  }

  // 3. Total Akhir
  let totalAkhir = totalBelanja - diskon + ongkir;
  return totalAkhir;
}

// Uji coba skenario B: belanja 150rb, jarak 5km
console.log("Total Skenario B:", hitungTotalBayar(150000, 5));
// Output: 140000 (Cocok dengan Dry Run Table!)
```

## 2. Refleksi Singkat:
Menerjemahkan pseudocode ke kode JavaScript terasa jauh lebih mudah saat tahapan dekomposisi, kondisi `if-else`, dan batas maksimalnya sudah kita uji terlebih dahulu lewat Dry Run Table.
````

---

## 9. Cek Pemahaman Diri

1. Apa bahayanya jika seorang pengembang software langsung membuat antarmuka (UI) atau menulis kode tanpa melakukan **dekomposisi** dan **abstraksi** terlebih dahulu?
2. Sebutkan contoh **pola logika** yang sama antara proses *"Cek Pulsa HP"* dan proses *"Cek Stok Barang di Katalog"*!
3. Mengapa kita perlu menguji pseudocode dengan **tabel uji manual (*dry run table*)** sebelum langsung menulis kode programnya?

---

Lanjut ke: **[02c-flowchart.md](02c-flowchart.md)**
