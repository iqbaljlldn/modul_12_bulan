# 02b. Abstraksi & Penulisan Algoritma (Pseudocode)

**Minggu 2: Computational Thinking & Algoritma | Sesi 2 (Selasa)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Dokumen Pseudocode Logika Bisnis UMKM + Jembatan Kode JS

---

## 1. Mengapa Ini Penting?

Dua pilar berikutnya dalam Computational Thinking adalah **Abstraksi** dan **Algoritma**:
- **Abstraksi** mengajari kita menyaring informasi: membuang hal-hal yang tidak relevan (*noise*) dan hanya menyimpan data inti yang dibutuhkan sistem.
- **Algoritma** mengajari kita menyusun instruksi yang runtut, tegas, dan tidak bermakna ganda (*unambiguous*).

Sebelum kamu menulis kode JavaScript atau TypeScript di Bulan 2, kamu harus bisa menuliskan alur logika tersebut dalam bentuk **Pseudocode** (kode semu berbahasa Indonesia yang terstruktur). Jika logikamu dalam bahasa manusia saja masih rancu, menerjemahkannya ke kode komputer hanya akan memicu kebingungan dan error.

---

## 2. Pilar 3: Abstraksi (Fokus pada Data Inti)

Abstraksi adalah kemampuan menyaring fakta.

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

Warna baju, merek motor, dan leceknya uang kertas adalah *noise* yang sengaja dibuang. Sistem hanya mencatat data yang berpengaruh pada perhitungan transaksi dan stok.

---

## 3. Pilar 4: Algoritma & Format Baku Pseudocode

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

## 4. Workshop Praktik Squad (60 Menit)

Setiap squad menyusun pseudocode dan tabel uji manual (*Dry Run Table*) untuk **2 Kasus Nyata UMKM**:

### Kasus 1: "Algoritma Hitung Diskon & Ongkir Warung"
Aturan toko:
- Jika total belanja >= Rp 100.000, berikan potongan diskon 10% (maksimal diskon Rp 20.000).
- Jika jarak alamat pembeli <= 3 km, ongkir gratis (Rp 0). Jika lebih dari 3 km, tarif ongkir adalah Rp 2.500 per km kelebihannya.
- Hitung total akhir yang harus dibayarkan pembeli.

### Kasus 2: "Algoritma Peringatan Stok Menipis"
Sistem memeriksa daftar produk toko:
- Untuk setiap produk, cek stok yang tersisa.
- JIKA stok <= 3, catat nama produk ke daftar *"Peringatan Stok Menipis"*.
- Di akhir pengecekan, tampilkan daftar produk yang butuh restok segera ke dashboard penjual.

### Uji Coba Manual (Dry Run Table):
Uji Kasus 1 dengan 3 skenario angka pada tabel:
| Skenario | Total Belanja | Jarak (km) | Diskon Didapat | Biaya Ongkir | Total Akhir |
|---|---|---|---|---|---|
| A | Rp 50.000 | 2 km | Rp 0 | Rp 0 | Rp 50.000 |
| B | Rp 150.000 | 5 km | Rp 15.000 | Rp 5.000 | Rp 140.000 |
| C | Rp 300.000 | 1 km | Rp 20.000 (max) | Rp 0 | Rp 280.000 |

---

## 5. Output Sesi

Dokumen Markdown squad yang memuat:
1. Hasil abstraksi data untuk Kasus 1 dan Kasus 2.
2. Teks Pseudocode lengkap Kasus 1 dan Kasus 2 sesuai format baku.
3. Tabel Dry Run Kasus 1 membuktikan perhitungan akurat.

---

## 6. Tugas Mandiri (Individual): Jembatan ke Kode JavaScript

- **Sifat:** Individu (dikerjakan sendiri di luar jam kelas)
- **Target Waktu:** 25 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_02b.md`

> [!TIP]
> **Sentuhan Kode Mingguan (Jembatan Menuju Bulan 2):**  
> Ingat sintaks dasar JavaScript yang sudah kamu pelajari sebelumnya? Sekarang saatnya menyegarkan ingatan jarimu dengan menerjemahkan pseudocode Kasus 1 di atas menjadi satu fungsi JavaScript sederhana!

### Instruksi:
1. Tuliskan satu fungsi JavaScript bernama `hitungTotalBayar(totalBelanja, jarakKm)`.
2. Gunakan percabangan `if` dan `else` sederhana untuk menghitung diskon dan ongkir sesuai aturan Kasus 1.
3. Cocokkan hasil `console.log()` fungsi kodemu dengan tabel *Dry Run* di atas.
4. Tuliskan kode JS tersebut dan hasil ujinya di file `tugas_02b.md`.

### Contoh Hasil yang Diharapkan:
```markdown
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
Menerjemahkan pseudocode ke kode JavaScript terasa jauh lebih mudah saat kondisi `if-else` dan batas maksimalnya sudah kita tuliskan jelas di kertas sebelumnya.
```

---

## 7. Cek Pemahaman Diri

1. Apa perbedaan mendasar antara pseudocode dan kode JavaScript nyata?
2. Mengapa kita perlu membuat tabel uji (*dry run table*) sebelum langsung mempercayai logika algoritma kita?

---

Lanjut ke: **[02c-flowchart.md](02c-flowchart.md)**
