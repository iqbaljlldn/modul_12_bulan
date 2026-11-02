# 02e. Latihan Terpadu CT: Menyatukan Logika, Alur, dan Data

**Minggu 2: Computational Thinking & Algoritma | Sesi 5 (Jumat)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Portofolio Terpadu 1 Fitur Pilihan (Dekomposisi Singkat + Pseudocode + 1 Flowchart + Potongan ERD)

---

## 1. Mengapa Ini Penting?

Sejauh minggu ini, kamu telah mempelajari potongan kemampuan secara terpisah:
- Senin: Memecah masalah (Dekomposisi) dan mencari kesamaan (Pola).
- Selasa: Menyaring data penting (Abstraksi) dan menulis langkah logis (Pseudocode).
- Rabu: Menggambar visual percabangan alur (Flowchart).
- Kamis: Menata tempat penyimpanan dan relasi informasi (ERD).

Hari ini adalah momen pembuktian kemampuan sejati seorang insinyur sistem: **mengintegrasikan seluruh potongan tersebut menjadi satu arsitektur solusi yang selaras pada satu fitur terpilih.**

Jika di flowchart kamu menyebut ada langkah *"Kurangi stok produk"*, maka di ERD wajib ada entitas `Produk` dengan atribut `stok`. Keterhubungan dan konsistensi inilah yang membedakan rancangan profesional dari coretan lepas.

---

## 2. Alur Integrasi: Dari Cerita Masalah ke Spesifikasi

```text
[ Cerita Masalah Toko UMKM ]
             │
             ▼ (Dekomposisi Singkat & Abstraksi)
[ Pseudocode Logika Bisnis ] 
             │
      ┌──────┴──────┐
      ▼             ▼
[ Flowchart Alur ] [ ERD Potongan Model Data ]
 (Visual Alur)      (Struktur Penyimpanan)
```

---

## 3. Pelajaran Nyata: Mengapa Selisih Milidetik Tidak Menjamin Stok Aman?

Perhatikan contoh kasus yang sering menjadi mitos programmer pemula:

> **Cerita Kasus: "Rebutan 1 Bungkus Keripik Terakhir"**  
> Toko Keripik Bu Tina hanya memiliki **1 bungkus keripik balado** tersisa.  
> Pada waktu yang hampir bersamaan, Pembeli A dan Pembeli B sama-sama menekan tombol konfirmasi pesanan.  
> *Mitos Pemula:* "Siapa yang menekan tombol lebih cepat 0,001 milidetik, dia yang pasti menang."  
> *Fakta Rekayasa Software:* Di server nyata yang melayani ribuan permintaan serentak (*concurrency*), selisih waktu milidetik di layar ponsel **tidak bisa diandalkan**. Jika kedua permintaan dibaca bersamaan, server bisa saja membaca bahwa stok masih 1 untuk kedua orang tersebut!

**Bagaimana Solusi Benarnya?**  
Bukan sekadar selisih waktu, melainkan **Transaksi Atomik di Database (*Atomic Database Transaction / Locking*)**. Database mengunci (*lock*) baris data stok tersebut pada level mesin: hanya satu instruksi pengurangan yang diizinkan selesai lebih dulu, dan instruksi kedua otomatis membaca bahwa stok sudah menjadi 0 sehingga ditolak.

*(Konsep transaksi database ini akan kamu bangun dengan kode NestJS & PostgreSQL di Bulan 4 nanti. Untuk Bulan 1, cukup pahami bahwa logika di balik layar harus mengantisipasi kondisi rebutan stok seperti ini).*

---

## 4. Workshop Praktik Squad: Rancang 1 Fitur Terpilih (60 Menit)

Agar tidak membebani tim dengan dokumen panjang, setiap squad **cukup memilih 1 Fitur Inti** dari scope katalog kita:

### Fitur Fokus Bulan 1 (Pilih Salah Satu):
- **Opsi A: Validasi Form Tambah Produk Merchant** (Mencegah produk tersimpan jika harga 0, nama kosong, atau stok minus).
- **Opsi B: Alur Pemesanan Cerdas via WhatsApp** (Cek stok ada/habis, buat pesan otomatis ramah, buka WhatsApp).

---

> [!NOTE]
> **Tantangan di Luar Scope Bulan 1 (Eksplorasi Lanjutan / Opsional):**  
> Fitur-fitur di bawah ini sangat menarik tetapi berada di luar batas scope Bulan 1 (katalog + WhatsApp). Fitur ini baru akan kita bangun pada bulan-bulan berikutnya:
> - *Fitur Kupon Promo Diskon Terbatas*
> - *Fitur Pembatalan Pesanan Otomatis (Auto-Cancel Timer)*
> - *Fitur Pre-Order (PO) dengan Kuota Produksi Harian*

---

### Tugas Squad untuk 1 Fitur Pilihan:
1. **Dekomposisi Singkat (4-6 baris):** Tuliskan urutan langkah inti fitur tersebut.
2. **Pseudocode:** Tulis logika penanganan sukses dan gagal menggunakan format `JIKA ... MAKA ... LAINNYA ... AKHIR-JIKA`.
3. **1 Flowchart:** Gambarkan diagram alurnya menggunakan sintaks Mermaid.
4. **Potongan ERD Sederhana (3-5 atribut):** Gambarkan entitas apa yang datanya dibaca atau diubah oleh fitur tersebut.

---

## 5. Output Sesi

Kumpulkan 1 file Markdown ringkas (`logika-fitur-terpadu.md`) yang berisi:
1. Nama fitur pilihan squad.
2. Teks Dekomposisi singkat & Pseudocode.
3. 1 Diagram Flowchart (Mermaid).
4. Potongan ERD yang memuat 3–5 atribut relevan.
5. Konfirmasi keselarasan: Buktikan bahwa setiap nama variabel di pseudocode memiliki kolom padanannya di ERD!

---

## 6. Tugas Mandiri (Individual)

- **Sifat:** Individu (dikerjakan sendiri di luar jam kelas)
- **Target Waktu:** 25 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_02e.md`

### Instruksi:
1. Pilih satu potongan logika: *"Ketika pembeli menekan tombol pesan, sistem mengurangi stok produk sebanyak jumlah yang dipesan"*.
2. Tuliskan 3 baris pseudocode untuk aksi tersebut.
3. Tuliskan nama entitas dan nama atribut di ERD yang wajib ada untuk mendukung pseudocode-mu.
4. Periksa: Apakah nama atribut di pseudocode dan ERD sudah sama persis? Jika ada perbedaan huruf, perbaiki agar konsisten.

### Contoh Hasil yang Diharapkan:
```markdown
# Tugas Mandiri 02e — Uji Konsistensi Pseudocode vs ERD
Nama: [Nama Kamu]

## 1. Pseudocode Potongan Aksi:
JIKA produk.stok >= pesanan.jumlah_beli MAKA
    HITUNG produk.stok = produk.stok - pesanan.jumlah_beli
    CATAT status_pesanan = "Diteruskan ke WA"
AKHIR-JIKA

## 2. Pengecekan Entitas & Atribut ERD:
- Entitas `PRODUK` wajib memiliki atribut: `stok` (tipe int)
- Entitas `ITEM_PESANAN` wajib memiliki atribut: `jumlah` (tipe int)
- Entitas `PESANAN` wajib memiliki atribut: `status_pesanan` (tipe string)

## 3. Hasil Pengecekan Konsistensi:
Semua variabel di pseudocode (`stok`, `jumlah_beli`/`jumlah`, `status_pesanan`) sudah memiliki padanan kolom atribut yang cocok di ERD, tidak ada variabel siluman tanpa tempat penyimpanan.
```

---

## 7. Cek Pemahaman Diri

1. Mengapa dalam sistem e-commerce besar, yang menjamin hanya satu orang yang berhasil mendapatkan 1 stok terakhir adalah transaksi database atomik dan bukan sekadar kecepatan klik milidetik?
2. Mengapa tidak boleh ada perbedaan penamaan atribut antara logika pseudocode dan rancangan ERD?

---

Lanjut ke: **[02f-review-dan-evaluasi-minggu2.md](02f-review-dan-evaluasi-minggu2.md)**
