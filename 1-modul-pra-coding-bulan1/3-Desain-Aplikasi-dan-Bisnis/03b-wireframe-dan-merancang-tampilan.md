# 03b. Wireframe: Merancang Struktur Tampilan Sebelum Coding

**Minggu 3: Desain Aplikasi & Bisnis | Sesi 2 (Selasa)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Wireframe 3 Halaman Utama Platform Katalog UMKM per Squad

---

## 1. Mengapa Ini Penting?

Jika seorang tukang bangunan langsung menyusun batu bata dan mengecat tembok tanpa melihat gambar denah arsitektur, rumah itu kemungkinan besar akan memiliki pintu yang menabrak jendela atau kamar mandi tanpa saluran pipa pembuangan.

Dalam pengembangan perangkat lunak, **Wireframe adalah denah biru (*blueprint*) antarmuka**.

Wireframe sengaja dibuat **tanpa warna-warni, tanpa foto asli, dan tanpa dekorasi estetik**. Tujuannya satu: memastikan tata letak (*layout*), alur navigasi tombol, dan hierarki informasi sudah benar sebelum kita menulis kode komponen React di Bulan 2.

---

## 2. Anatomi & Simbol Menggambar Wireframe

Saat membuat wireframe di kertas atau aplikasi gambar, gunakan simbol konvensi standar berikut:

```text
┌──────────────────────────────────────────────┐
│  [Logo Toko]       [Cari Produk...]    (🔍)  │ ◄── Header & Pencarian
├──────────────────────────────────────────────┤
│  [ Semua ]  [ Makanan ]  [ Minuman ]         │ ◄── Kategori (Pills/Tabs)
├──────────────────────────────────────────────┤
│  ┌───────────────┐     ┌───────────────┐     │
│  │ ┌───────────┐ │     │ ┌───────────┐ │     │
│  │ │     X     │ │     │ │     X     │ │     │ ◄── Kotak Tanda 'X' =
│  │ └───────────┘ │     │ └───────────┘ │     │     Placeholder Foto Produk
│  │ Keripik Tempe │     │ Sambal Botol  │     │ ◄── Garis Teks = Nama & Info
│  │ Rp 15.000     │     │ Rp 25.000     │     │
│  │ [ Pesan WA ]  │     │ [ Pesan WA ]  │     │ ◄── Kotak Berisi Label = Tombol
│  └───────────────┘     └───────────────┘     │
└──────────────────────────────────────────────┘
```

### Konvensi Baku Gambar:
- **Kotak bersilang X:** Area gambar / foto produk.
- **Garis horizontal:** Blok teks atau paragraf informasi.
- **Kotak berbingkai tebal:** Tombol aksi (*Call to Action*).
- **Garis panah:** Alur perpindahan jika tombol disentuh/diklik.

---

## 3. Tiga Halaman Inti Platform Katalog UMKM

Bulan depan (Bulan 2), produk pertama yang akan kalian bangun dengan React adalah **Mini Katalog UMKM**. Hari ini kita merancang cetak birunya:

### Halaman 1: Katalog Utama (Daftar Produk)
- **Tujuan Pengguna:** Pembeli ingin melihat-lihat produk yang dijual, mencari barang, atau menyaring kategori.
- **Komponen Kunci:** Header Nama Toko, Kolom Pencarian, Tombol Filter Kategori, Grid Kartu Produk (Foto, Nama, Harga, Label Stok Habis jika stok 0, dan Tombol Pesan).

### Halaman 2: Detail Produk
- **Tujuan Pengguna:** Pembeli ingin membaca info lengkap sebelum memutuskan membeli.
- **Komponen Kunci:** Foto produk berukuran besar, Nama lengkap barang, Harga satuan, Deskripsi bahan/rasa, Tombol Utama *"Pesan via WhatsApp"* di bagian bawah layar.

### Halaman 3: Dashboard Kelola Produk Merchant
*(Scope: Merchant mengelola dagangan tanpa sistem login rumit).*
- **Tujuan Pengguna:** Pemilik UMKM ingin menambah barang jualan baru dengan cepat tanpa ribet.
- **Komponen Kunci:** Form Nama Produk, Input Harga (rupiah), Pilihan Kategori, Input Jumlah Stok, Kolom URL Foto, Tombol *"Simpan Produk"* dan *"Batal"*.

---

## 4. Workshop Praktik Squad (60 Menit)

### Langkah Pengerjaan Tim:
1. **Langkah 1 (Sketsa Kertas Mobile-First - 30 Menit):**  
   Gambarkan sketsa 3 halaman di atas pada kertas HVS dalam rasio layar ponsel tegak (9:16).  
   > *Catatan Penting:* Mayoritas pelaku UMKM dan pembeli lokal di Indonesia mengakses internet melalui smartphone (cek data resmi Kementerian Koperasi dan UKM / BPS untuk angka statistik terbaru). Oleh karena itu, kita selalu mendesain dengan pendekatan **Mobile-First** (mengutamakan layar ponsel terlebih dahulu).
2. **Langkah 2 (Uji Alur Jari / Paper Prototyping - 15 Menit):**  
   Minta salah satu anggota squad berpura-pura menjadi pembeli. Sentuhkan jari telunjuk ke tombol di kertas Halaman 1, lalu balik kertas ke Halaman 2. Apakah tata letaknya nyaman untuk satu jempol?
3. **Langkah 3 (Dokumentasi Rapi - 15 Menit):**  
   Foto sketsa kertas kalian atau salin ke tools digital hitam-putih sederhana (Excalidraw / Figma).

---

## 5. Output Sesi

Kumpulkan dokumen gambar atau foto sketsa tim berisi:
- Wireframe Halaman 1 (Katalog Utama).
- Wireframe Halaman 2 (Detail Produk).
- Wireframe Halaman 3 (Dashboard Tambah Produk Merchant).
- Keterangan alur interaksi: tombol mana yang membuka halaman mana jika diklik.

---

## 6. Tugas Mandiri (Individual): Jembatan ke Kode HTML & CSS

- **Sifat:** Individu (dikerjakan sendiri di luar jam kelas)
- **Target Waktu:** 25 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_03b.md`

> [!TIP]
> **Sentuhan Kode Mingguan (Jembatan Menuju Bulan 2):**  
> Di 2 bulan sebelumnya, kamu sudah mempelajari dasar HTML dan CSS. Sekarang ubah salah satu kartu produk dari wireframe Halaman 1 menjadi kode HTML & CSS statis hitam-putih sederhana!

### Instruksi:
1. Tulis kode HTML sederhana untuk 1 kartu produk (berisi placeholder gambar, judul barang, harga, dan tombol pesan).
2. Tulis kode CSS minimal dengan styling hitam-putih (border, padding, font sans-serif) agar menyerupai wireframe.
3. Simpan cuplikan kode tersebut di file `tugas_03b.md`.

### Contoh Hasil yang Diharapkan:
```markdown
# Tugas Mandiri 03b — Wireframe HTML/CSS Hitam-Putih
Nama: [Nama Kamu]

## 1. Kode HTML & CSS:
```html
<style>
  .card-produk {
    width: 200px;
    border: 2px solid #000;
    padding: 12px;
    font-family: sans-serif;
    background-color: #fff;
  }
  .placeholder-img {
    height: 120px;
    background-color: #eee;
    border: 1px dashed #666;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    color: #666;
    margin-bottom: 8px;
  }
  .nama-produk {
    font-size: 16px;
    margin: 4px 0;
  }
  .harga-produk {
    font-size: 14px;
    color: #333;
    margin-bottom: 12px;
  }
  .btn-wa {
    width: 100%;
    padding: 8px;
    background-color: #000;
    color: #fff;
    border: none;
    font-weight: bold;
    cursor: pointer;
  }
</style>

<div class="card-produk">
  <div class="placeholder-img">[ FOTO X ]</div>
  <h3 class="nama-produk">Keripik Balado</h3>
  <p class="harga-produk">Rp 15.000</p>
  <button class="btn-wa">Pesan via WhatsApp</button>
</div>
```

## 2. Refleksi Singkat:
Membuat kerangka HTML/CSS hitam-putih terasa seperti menggambar balok bangunan. Ini membuat saya siap menyusun komponen React di Bulan 2 nanti.
```

---

## 7. Cek Pemahaman Diri

1. Mengapa desainer pemula sangat dilarang memasukkan warna-warni estetik pada tahap pembuatan wireframe?
2. Mengapa pendekatan *Mobile-First* sangat wajib diterapkan untuk aplikasi platform UMKM lokal?

---

Lanjut ke: **[03c-value-proposition-dan-model-bisnis.md](03c-value-proposition-dan-model-bisnis.md)**
