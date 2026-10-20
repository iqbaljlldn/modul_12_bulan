# 03b. Wireframe: Merancang Struktur Tampilan Sebelum Coding

**Minggu 3: Desain Aplikasi & Bisnis | Sesi 2 (Selasa)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Wireframe 3 Halaman Utama Platform Katalog UMKM per Squad

---

## 1. Mengapa Ini Penting?

Jika seorang tukang bangunan langsung menyusun batu bata dan mengecat tembok tanpa melihat denah arsitektur, rumah itu kemungkinan besar akan memiliki pintu yang menabrak jendela atau kamar mandi tanpa saluran pembuangan.

Dalam pengembangan perangkat lunak, **Wireframe adalah denah biru antarmuka**.

Wireframe sengaja dibuat **tanpa warna warni, tanpa foto asli, dan tanpa dekorasi estetik**. Tujuannya satu: memastikan tata letak (*layout*), alur navigasi, dan hierarki informasi sudah benar sebelum kita repot-repot memikirkan CSS atau menulis komponen React di Bulan 2.

---

## 2. Anatomi & Konvensi Menggambar Wireframe

Saat menggambar wireframe di kertas atau tools digital, gunakan simbol konvensi standar berikut:

```text
┌──────────────────────────────────────────────┐
│  [Logo Toko]       [Cari Produk...]    (🔍)  │ ◄── Header & Pencarian
├──────────────────────────────────────────────┤
│  [ Semua ]  [ Makanan ]  [ Kerajinan ]       │ ◄── Kategori (Pills/Tabs)
├──────────────────────────────────────────────┤
│  ┌───────────────┐     ┌───────────────┐     │
│  │ ┌───────────┐ │     │ ┌───────────┐ │     │
│  │ │     X     │ │     │ │     X     │ │     │ ◄── Kotak Berisi 'X' =
│  │ └───────────┘ │     │ └───────────┘ │     │     Placeholder Gambar
│  │ Keripik Tempe │     │ Sambal Bawang │     │ ◄── Garis Teks = Judul & Info
│  │ Rp 15.000     │     │ Rp 25.000     │     │
│  │ [ + Keranjang]│     │ [ + Keranjang]│     │ ◄── Kotak Berisi Teks = Tombol
│  └───────────────┘     └───────────────┘     │
└──────────────────────────────────────────────┘
```

### Konvensi Baku:
- **Kotak dengan garis silang X:** Area untuk foto/gambar produk.
- **Garis horizontal sejajar:** Teks paragraf atau deskripsi.
- **Kotak persegi panjang dengan label:** Tombol interaktif (*Call to Action*).
- **Garis putus-putus atau panah:** Arah klik perpindahan halaman.

---

## 3. Tiga Halaman Inti Platform Katalog UMKM

Bulan depan (Bulan 2), produk pertama yang akan kalian bangun dengan React adalah **Mini Katalog UMKM**. Hari ini kita merancang cetak birunya:

### Halaman 1: Katalog Utama (Daftar Produk)
- **Tujuan Pengguna:** Pembeli ingin melihat-lihat barang yang dijual, mencari produk tertentu, atau menyaring kategori.
- **Komponen Kunci:** Header/Pencarian, Filter Kategori, Grid Kartu Produk (Foto, Nama, Harga, Tag Kategori, Tombol Aksi), Indikator Stok Habis.

### Halaman 2: Detail Produk
- **Tujuan Pengguna:** Pembeli ingin membaca info lengkap sebelum memutuskan membeli.
- **Komponen Kunci:** Galeri foto besar, Nama lengkap produk, Harga & Varian (jika ada), Deskripsi rinci bahan/ukuran, Informasi Penjual/Merchant, Tombol Utama "Hubungi Penjual via WhatsApp" atau "Pesan Sekarang".

### Halaman 3: Form Tambah/Ubah Produk (Dashboard Merchant)
- **Tujuan Pengguna:** Pemilik UMKM ingin memajang barang jualan baru dengan cepat tanpa ribet.
- **Komponen Kunci:** Input Nama Produk, Input Harga (rupiah), Dropdown Kategori, Input Stok, Area Upload/Input Link Foto, Area Deskripsi, Tombol "Simpan Produk" dan "Batal".

---

## 4. Workshop Praktik Squad (60 Menit)

### Langkah Pengerjaan:
1. **Langkah 1 (Kertas & Spidol Dulu - 30 Menit):**
   Ambil kertas HVS atau buku sketsa. Gambarkan sketsa 3 halaman di atas dalam ukuran ponsel cerdas (*mobile-first*, rasio layar tegak 9:16).
   - *Kenapa mobile-first?* Lebih dari 85% pedagang dan pembeli UMKM di Indonesia mengakses internet lewat handphone, bukan laptop!
2. **Langkah 2 (Uji Alur Jari / Paper Prototyping - 15 Menit):**
   Minta salah satu anggota squad berpura-pura menjadi pembeli. Gunakan jarinya menyentuh tombol di kertas halaman 1, lalu balik kertas ke halaman 2. Apakah alurnya masuk akal? Apakah ada tombol yang terlewat?
3. **Langkah 3 (Digitalisasi Opsional / Dokumentasi Rapi - 15 Menit):**
   Foto sketsa kertas kalian atau salin ke Figma / Excalidraw sederhana hitam-putih.

---

## 5. Output Sesi

Kumpulkan foto dokumen fisik atau tangkapan layar digital berisi:
- Wireframe Halaman 1: Katalog Utama.
- Wireframe Halaman 2: Detail Produk.
- Wireframe Halaman 3: Form Tambah/Edit Produk.
- Catatan Alur Interaksi: Tombol mana yang berpindah ke halaman mana jika diklik.

---

## 6. Cek Pemahaman Diri

1. Mengapa desainer sangat dilarang memasukkan warna-warni cantik pada tahap awal pembuatan wireframe?
2. Apa yang dimaksud dengan pendekatan desain *Mobile-First* dan mengapa pendekatan ini wajib untuk produk UMKM?

Lanjut ke: **[03c-value-proposition-dan-model-bisnis.md](file:///home/iqbaal/gelombang-3/modul 12 bulan/modul-pra-coding-bulan1/3-Desain-Aplikasi-dan-Bisnis/03c-value-proposition-dan-model-bisnis.md)**
