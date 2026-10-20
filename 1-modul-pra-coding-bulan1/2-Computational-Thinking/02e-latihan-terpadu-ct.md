# 02e. Latihan Terpadu CT: Menyatukan Logika, Alur, dan Data

**Minggu 2: Computational Thinking & Algoritma | Sesi 5 (Jumat)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Portofolio Terpadu Logika Fitur (Dekomposisi + Pseudocode + Flowchart + ERD)

---

## 1. Mengapa Ini Penting?

Sejauh minggu ini, kamu telah mempelajari potongan-potongan kemampuan secara terpisah:
- Senin: Memecah masalah (Dekomposisi) dan mencari kesamaan (Pola).
- Selasa: Menyaring data penting (Abstraksi) dan menulis langkah logis (Pseudocode).
- Rabu: Menggambar visual percabangan (Flowchart).
- Kamis: Menata tempat penyimpanan dan relasi informasi (ERD).

Hari ini adalah momen pembuktian kemampuan sejati seorang insinyur sistem: **mengintegrasikan seluruh potongan tersebut menjadi satu arsitektur solusi yang utuh dan selaras.**

Jika di flowchart kamu menyebut ada langkah *"Kurangi stok produk"*, maka di ERD wajib ada entitas `Produk` dengan atribut `stok`. Keterhubungan dan konsistensi inilah yang membedakan rancangan profesional dari sekadar coretan iseng.

---

## 2. Alur Integrasi: Dari Cerita Pengguna ke Spesifikasi Teknis

```text
[ Cerita Masalah Pengguna UMKM ]
             │
             ▼ (Dekomposisi & Abstraksi)
[ Pseudocode Logika Bisnis ] 
             │
      ┌──────┴──────┐
      ▼             ▼
[ Flowchart Alur ] [ ERD Model Data ]
 (Visual Alur)      (Struktur Penyimpanan)
```

---

## 3. Tantangan Integrasi Terpadu: Kasus "Flash Sale / Rebutan Stok"

Mari pelajari skenario nyata yang sering merusak sistem e-commerce:

> **Cerita Kasus:**  
> Toko Keripik Bu Tina mengadakan diskon kilat. Stok Keripik Balado hanya tersisa **1 bungkus**.  
> Pada detik yang sama persis, Pembeli A dan Pembeli B sama-sama membuka aplikasi, memasukkan keripik ke keranjang, dan menekan tombol konfirmasi bayar.  
> Jika sistem tidak dirancang cermat, kedua pembeli akan merasa berhasil membayar, tetapi Bu Tina hanya punya 1 bungkus keripik! Bu Tina bingung, salah satu pembeli marah besar dan memberi ulasan bintang satu.

Bagaimana seorang engineer menyelesaikan ini dengan Computational Thinking?

1. **Dekomposisi:** Pisahkan proses pengecekan stok dari proses pembayaran.
2. **Abstraksi:** Jangan hanya catat `status: "lunas"`. Kita butuh konsep status sementara: `status: "dibooking_15_menit"`.
3. **Flowchart & Algoritma:** Saat Pembeli A klik bayar lebih dulu satu milidetik, stok langsung dikunci (*reserved*). Saat Pembeli B menekan tombol satu milidetik kemudian, sistem membaca stok tersedia = 0 dan langsung menolak pesanan B secara elegan.
4. **ERD:** Tambahkan atribut `stok_terkunci` atau entitas `ReservasiStok` dengan kolom waktu kadaluwarsa (`expires_at`).

---

## 4. Workshop Praktik Squad (60 Menit)

Setiap squad memilih salah satu fitur kunci dari **Platform Katalog UMKM**:

- **Pilihan 1: Fitur Diskon Kupon Promo Terbatas** (Hanya berlaku untuk 10 pembeli pertama yang belanja di atas Rp 50.000).
- **Pilihan 2: Fitur Pembatalan Pesanan Otomatis** (Jika pembeli tidak mengunggah bukti bayar dalam 30 menit, pesanan batal dan stok kembali).
- **Pilihan 3: Fitur Pre-Order (PO) Kue Lebaran** (Toko hanya menerima maksimal 20 pesanan per hari produksi, jika kuota penuh, tanggal tersebut ditutup).

### Tugas Squad:
1. **Dekomposisi & Abstraksi:** Tuliskan batasan masalah dan data apa saja yang relevan.
2. **Pseudocode:** Tulis logika penanganan kondisi sukses, kondisi gagal, dan *edge cases* (kasus ekstrem).
3. **Flowchart (Mermaid / Gambar):** Gambarkan diagram alurnya secara lengkap dengan terminator dan label cabang.
4. **ERD Snippet:** Tunjukkan potongan entitas dan atribut apa saja yang terlibat dalam fitur tersebut.
5. **Uji Konsistensi Silang:**
   - Cek apakah setiap variabel di pseudocode ada padanannya di ERD.
   - Cek apakah setiap cabang di flowchart sudah diakomodasi di logika pseudocode.

---

## 5. Output Sesi: Portofolio Terpadu Logika Fitur

Kumpulkan 1 dokumen Markdown lengkap (`logika-fitur-terpadu.md`) yang berisi:
- Deskripsi Cerita Fitur & Masalah.
- Analisis 4 Pilar CT (Dekomposisi, Pola, Abstraksi, Pseudocode).
- Flowchart Alur Lengkap.
- ERD Pendukung.
- Analisis Celah & Edge Cases yang berhasil diantisipasi.

Dokumen ini akan menjadi materi utama yang kalian pertahankan pada Sprint Review besok Sabtu!

---

## 6. Cek Pemahaman Diri

1. Apa yang dimaksud dengan *edge case* (kasus ekstrem) dalam perancangan sistem perangkat lunak?
2. Mengapa tidak boleh ada perbedaan nama atribut antara flowchart dengan ERD?

Lanjut ke: **[02f-review-dan-evaluasi-minggu2.md](file:///home/iqbaal/gelombang-3/modul 12 bulan/modul-pra-coding-bulan1/2-Computational-Thinking/02f-review-dan-evaluasi-minggu2.md)**
