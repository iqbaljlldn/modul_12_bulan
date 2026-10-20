# 02b. Abstraksi & Penulisan Algoritma (Pseudocode)

**Minggu 2: Computational Thinking & Algoritma | Sesi 2 (Selasa)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Dokumen Pseudocode Logika Bisnis UMKM

---

## 1. Mengapa Ini Penting?

Dua pilar terakhir Computational Thinking adalah **Abstraksi** dan **Algoritma**:
- **Abstraksi** mengajari kita membuang "kebisingan" (*noise*) dan fokus pada informasi penting yang dibutuhkan sistem.
- **Algoritma** mengajari kita menyusun instruksi yang runtut, tegas, dan tidak bermakna ganda (*unambiguous*).

Sebelum kamu menulis kode dalam bahasa JavaScript atau TypeScript di Bulan 2, kamu harus bisa menulis algoritma dalam bahasa manusia yang terstruktur—dikenal sebagai **Pseudocode**. Jika algoritmamu dalam bahasa Indonesia saja masih membingungkan, menerjemahkannya ke bahasa pemrograman hanya akan menghasilkan ribuan bug.

---

## 2. Pilar 3: Abstraksi (Fokus pada Inti, Buang yang Tidak Relevan)

Abstraksi adalah kemampuan menyaring fakta.

### Contoh Kasus di Toko Kelontong:
Ketika seorang pembeli bernama Pak Budi datang membeli 2 kg beras:
- *Detail Nyata:* Pak Budi memakai baju merah, naik motor matic warna biru, bercanda tentang cuaca panas, membayar pakai uang kertas Rp 50.000 yang agak lecek, dan tersenyum ramah.
- *Abstraksi Sistem Kasir:*
  ```text
  ID_Pembeli     : 08123456789 (Nomor HP jika member, atau 'Anonim')
  Item_Dibeli    : Beras Ramos (ID: PRD-001)
  Jumlah         : 2
  Total_Bayar    : Rp 28.000
  Uang_Diterima  : Rp 50.000
  Kembalian      : Rp 22.000
  Waktu_Transaksi: 10-10-2026 14:15:00
  ```

Warna baju, merek motor, dan leceknya uang adalah *noise*. Mengabaikan hal tersebut agar sistem bisa bekerja cepat adalah contoh penerapan abstraksi.

---

## 3. Pilar 4: Algoritma & Struktur Logika Dasar

Algoritma adalah serangkaian instruksi langkah-demi-langkah yang berurutan dan memiliki kondisi berhenti.

Setiap algoritma di dunia komputer dibangun dari **3 blok dasar**:

```text
1. SEKUENSIAL (Berurutan)       2. PERCABANGAN (If-Else)        3. PERULANGAN (Looping)
   Langkah 1                       JIKA kondisi MAKA               SELAMA ada item
   Langkah 2                          Lakukan A                       Lakukan B
   Langkah 3                       LAINNYA                         Selesai loop
                                      Lakukan B
```

### Format Standar Pseudocode Bahasa Indonesia:
Gunakan kata kunci kapital berikut agar logikamu rapi dan terstandar:
- `MULAI` / `SELESAI`
- `MASUKKAN` / `TAMPILKAN`
- `JIKA ... MAKA ... LAINNYA`
- `UNTUK SETIAP ... LAKUKAN` / `SELAMA ... LAKUKAN`

### Contoh Pseudocode: Validasi Pembelian Produk di Katalog UMKM
```text
ALGORITMA ProsesBeliProduk
MULAI
    MASUKKAN id_produk, jumlah_beli, uang_dibayar

    AMBIL data_produk BERDASARKAN id_produk
    
    JIKA data_produk TIDAK DITEMUKAN MAKA
        TAMPILKAN "Error: Produk tidak ditemukan di katalog"
        SELESAI
    AKHIR-JIKA

    JIKA data_produk.stok < jumlah_beli MAKA
        TAMPILKAN "Maaf, stok hanya tersisa: " + data_produk.stok
        SELESAI
    AKHIR-JIKA

    HITUNG total_tagihan = data_produk.harga * jumlah_beli

    JIKA uang_dibayar < total_tagihan MAKA
        TAMPILKAN "Uang tidak cukup. Kurang: " + (total_tagihan - uang_dibayar)
        SELESAI
    LAINNYA
        HITUNG kembalian = uang_dibayar - total_tagihan
        KURANGI data_produk.stok DENGAN jumlah_beli
        CATAT transaksi ke riwayat
        TAMPILKAN "Transaksi Berhasil! Kembalian Anda: " + kembalian
    AKHIR-JIKA
SELESAI
```

---

## 4. Workshop Praktik Squad (60 Menit)

Ambil hasil dekomposisi dari Sesi 02a kemarin. Setiap squad akan menyusun pseudocode untuk **2 Kasus Logika Nyata**:

### Kasus 1: "Algoritma Hitung Diskon & Ongkos Kirim UMKM"
Sebuah toko oleh-oleh memberlakukan aturan:
- Jika total belanja >= Rp 100.000, berikan diskon 10% (maksimal potongan Rp 20.000).
- Jika alamat pembeli berjarak <= 3 km dari toko, gratis ongkos kirim. Jika lebih dari 3 km, kenakan tarif Rp 2.500 per km kelebihannya.
- Hitung total akhir yang harus dibayar pembeli.

### Kasus 2: "Algoritma Cek Notifikasi Restok Otomatis"
Sistem harus memeriksa seluruh daftar produk di toko kue (ada 50 jenis kue).
- Untuk setiap kue, periksa jumlah stok yang tersisa.
- Jika stok <= 5 buah, tambahkan nama kue tersebut ke dalam "Daftar Peringatan Restok Besok".
- Di akhir pengecekan, jika daftar peringatan tidak kosong, kirim pesan rekapitulasi ke WhatsApp pemilik toko.

---

## 5. Output Sesi: Dokumen Pseudocode

Setiap squad mengumpulkan file Markdown berisi:
1. Daftar hasil **Abstraksi**: data apa saja yang disimpan dan data apa yang sengaja dibuang untuk Kasus 1 dan Kasus 2.
2. Teks **Pseudocode lengkap** untuk Kasus 1 dan Kasus 2 sesuai format baku di atas.
3. Uji Coba Manual (*Dry Run Table*): Uji algoritma Kasus 1 dengan 3 skenario angka nyata (misal: belanja 50rb jarak 2km; belanja 150rb jarak 5km; belanja 300rb jarak 1km) untuk membuktikan perhitungannya akurat!

---

## 6. Cek Pemahaman Diri

1. Apa bedanya pseudocode dengan bahasa pemrograman nyata seperti JavaScript?
2. Mengapa algoritma wajib memiliki instruksi penutup (`SELESAI`) dan tidak boleh berjalan tanpa henti tanpa batas?

Lanjut ke: **[02c-flowchart.md](file:///home/iqbaal/gelombang-3/modul 12 bulan/modul-pra-coding-bulan1/2-Computational-Thinking/02c-flowchart.md)**
