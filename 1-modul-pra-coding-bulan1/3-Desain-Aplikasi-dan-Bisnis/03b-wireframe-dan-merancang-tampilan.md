# 03b. Wireframe: Merancang Struktur Tampilan Sebelum Coding

**Minggu 3: Desain Aplikasi & Bisnis | Sesi 2 (Selasa)**  
**Target Waktu:** 90 - 120 Menit  
**Tools:** Figma (akun gratis pribadi) + Figma AI bawaan  
**Output Sesi:** Wireframe 3 Halaman Utama Platform Katalog UMKM di Figma + Alur Interaksi *(link Figma & ekspor gambar di-push ke repo squad untuk dipresentasikan saat Daily Standup besok pagi)*

---

## 1. Mengapa Ini Penting?

Jika seorang tukang bangunan langsung menyusun batu bata dan mengecat tembok tanpa melihat gambar denah arsitektur, rumah itu kemungkinan besar akan memiliki pintu yang menabrak jendela atau kamar mandi tanpa saluran pipa pembuangan.

Dalam pengembangan perangkat lunak, **Wireframe adalah denah biru (*blueprint*) antarmuka**.

Wireframe sengaja dibuat **hitam-putih (grayscale), tanpa warna-warni brand, tanpa foto produk asli, dan tanpa dekorasi estetik**. Tujuannya satu: memastikan tata letak (*layout*), alur navigasi tombol, dan hierarki informasi sudah benar sebelum kita menulis kode komponen React di Bulan 2.

> [!NOTE]
> **Jangan Tertukar:**  
> **Wireframe** fokus pada *struktur & fungsi* (kotak hitam-putih kasar di tahap awal), sedangkan **Mockup / Desain Visual** baru memikirkan *warna, font estetik, dan foto asli*.

---

## 2. Anatomi & Simbol Menggambar Wireframe

Mulai sesi ini kita merancang wireframe langsung di **Figma**, tool desain antarmuka yang dipakai tim produk profesional. Apa pun tool-nya, simbol konvensi standarnya sama:

![Anatomi dan Simbol Wireframe Mobile-First Katalog UMKM](./assets/03b-anatomi-wireframe.jpg)

| Simbol pada Wireframe | Arti & Fungsi |
|---|---|
| **Kotak dengan silang (`X`)** | *Placeholder* area gambar atau foto produk (belum perlu foto asli). |
| **Teks polos / garis horizontal** | Judul produk, harga, atau blok teks deskripsi singkat. |
| **Kotak berbingkai tebal / blok gelap** | Tombol aksi utama (*Call to Action* / CTA) seperti `[ Pesan WA ]`. |
| **Garis panah antar layar** | Alur perpindahan halaman ketika sebuah tombol disentuh atau diklik. |

### Perkenalan Singkat Figma (Siapkan Sebelum Workshop)

| Kebutuhan | Cara di Figma |
|---|---|
| **Layar ponsel** | Buat *Frame* ukuran ponsel (pilih preset *Phone* di panel kanan, mis. 390 × 844). Satu frame = satu halaman. |
| **Kotak foto `X`** | Gambar persegi (`R`), lalu tarik dua garis diagonal (`L`) membentuk silang. |
| **Teks & tombol** | Teks (`T`) dan persegi berisi teks. Tombol CTA diberi isi hitam. |
| **Alur antar halaman** | Tab *Prototype*: tarik penghubung dari tombol ke frame tujuan. |

> [!NOTE]
> Nama menu dan tombol di Figma bisa berubah mengikuti pembaruan. Kalau tampilannya beda dari tabel di atas, cari fitur yang fungsinya sama atau tanya mentor/AI.

**Aturan wajib wireframe di Figma:** hanya hitam, putih, dan abu-abu. Jangan pakai warna brand, foto asli, atau ikon dekoratif.

---

## 3. Tiga Halaman Inti Platform Katalog UMKM

Mulai Bulan 2, produk pertama yang akan kalian bangun dengan React adalah **Mini Katalog UMKM**. Hari ini kita merancang cetak birunya dengan pendekatan **Mobile-First** (mengutamakan tampilan layar smartphone tegak terlebih dahulu, karena mayoritas pembeli dan pemilik UMKM lokal mengakses toko online lewat ponsel).

### Halaman 1: Katalog Utama (Daftar Produk)
- **Tujuan Pengguna:** Pembeli ingin melihat-lihat dagangan yang tersedia, mencari barang, atau menyaring kategori.
- **Komponen Kunci:** Header Nama Toko, Kolom Pencarian, Tombol Filter Kategori (*Tabs/Pills*), dan Grid Kartu Produk (Foto `X`, Nama, Harga, penanda **Stok Habis** jika stok `0`, serta tombol pesan/lihat detail).

### Halaman 2: Detail Produk
- **Tujuan Pengguna:** Pembeli ingin memeriksa detail barang, menentukan jumlah beli, lalu langsung memesan ke WhatsApp pedagang.
- **Komponen Kunci:** Tombol Kembali, Foto produk besar, Nama lengkap barang, Harga satuan & **Info Stok Tersedia**, Deskripsi singkat, Pemilih Jumlah (`-` / `+`), Form singkat (Nama & No. WA), serta Tombol Utama **"Pesan via WhatsApp"** di zona jempol bagian bawah layar *(atau tombol nonaktif jika stok habis)*.

### Halaman 3: Dashboard Kelola Produk Merchant
*(Scope: Merchant mengelola dagangan secara ringkas tanpa sistem login yang rumit).*
- **Tujuan Pengguna:** Pemilik UMKM ingin menambah produk baru atau memperbarui stok barang yang sudah habis dengan cepat.
- **Komponen Kunci:**
  1. **Form Tambah Produk:** Input Nama Produk, Harga (rupiah), Pilihan Kategori, Jumlah Stok, Kolom URL Foto, serta tombol **"Simpan Produk"** dan **"Batal"**.
  2. **Daftar Produk Ringkas:** Tabel/kartu produk milik toko dengan aksi cepat untuk **ubah stok / tandai habis / hapus**.

---

## 4. Workshop Praktik Squad (60 Menit)

### Persiapan (5 Menit)
Satu anggota squad membuat **1 file Figma squad** (akun gratis pribadi), lalu mengundang anggota lain sebagai editor. Beri nama file `Wireframe Katalog UMKM - [Nama Squad]`. Satu file cukup, dengan 3 frame (Halaman 1, 2, 3).

### Langkah Pengerjaan Tim:
1. **Langkah 1 — Gambar Manual di Figma, Tanpa AI (30 Menit):**  
   Buka kembali **3 Aturan UX Wajib** dari Sesi `03a`. Bagi tugas: tiap anggota menggambar satu halaman (atau satu bagian halaman) dalam frame ponsel tegak. Gambar manual dengan kotak `X`, teks, dan tombol hitam.  
   *Wajib gambar kondisi khusus:* kartu **Stok = 0** dan pesan error form berbahasa Indonesia yang ramah.  
   > *Kenapa tanpa AI dulu?* Wireframe melatih kalian berpikir tentang struktur. Kalau AI sudah menggambarkan semuanya, kalian tidak tahu kenapa tata letaknya begitu.
2. **Langkah 2 — Hubungkan Alur di Tab Prototype (10 Menit):**  
   Sambungkan tombol ke frame tujuan (Halaman 1 → Halaman 2, dst.). Jalankan mode *Present* di ponselmu atau browser, lalu minta satu anggota berpura-pura jadi pembeli awam.  
   - Apakah tombol utama mudah dijangkau satu jempol?  
   - Ada tombol yang buntu atau tidak membawa ke mana-mana?
3. **Langkah 3 — Figma AI sebagai Pengkritik & Pemberi Variasi (15 Menit):**  
   Pakai fitur AI bawaan Figma untuk dua hal:
   - **Kritik:** minta masukan terhadap tata letak, misalnya dengan prompt di bawah.
   - **Variasi:** minta alternatif tata letak Halaman 1, lalu bandingkan dengan buatan kalian.

   > **Template prompt kritik:**  
   > *"Ini wireframe halaman katalog untuk UMKM yang pembelinya awam teknologi dan memakai ponsel satu tangan. Nilai terhadap 4 prinsip UX: kebiasaan pengguna, jangkauan jempol tombol utama, visibilitas status sistem, dan pencegahan kesalahan. Beri 3 kelemahan paling serius dan saran perbaikannya."*

   **Aturan main:**
   - AI hanya memberi saran. **Squad yang memutuskan** saran mana yang dipakai.
   - Kalau AI menghasilkan desain berwarna atau penuh dekorasi, sederhanakan kembali jadi hitam-putih.
   - Kredit AI di akun gratis terbatas (ada kuota bulanan dan harian, cek di akunmu). Pakai seperlunya dan jangan dihabiskan dalam satu sesi.
   - Kalau kuota habis atau fitur AI tidak tersedia di akunmu, pakai asisten AI lain atau lanjut dengan kritik antaranggota squad.
4. **Langkah 4 — Finalisasi & Push ke Repo Squad (±15 Menit):**  
   Perbaiki wireframe berdasarkan hasil uji dan kritik AI. Ekspor tiap halaman sebagai PNG, simpan di folder `minggu-3/wireframe/` repo squad, lalu tulis link Figma beserta catatannya di `wireframe-squad.md`. Pastikan link Figma bisa dibuka oleh anggota lain (setelan *Anyone with the link can view*).

> [!TIP]
> **Cadangan:** Kalau ada anggota yang tidak bisa mengakses Figma (akun bermasalah atau tidak ada koneksi), sketsa di kertas HVS rasio `9:16` lalu foto tetap diterima untuk bagian halaman tersebut.

---

## 5. Output Sesi

*Push* dokumen `wireframe-squad.md` beserta ekspor gambar ke repositori squad (siap dipresentasikan saat **Daily Standup besok pagi**) berisi:
1. **Link file Figma squad** (akses *view* terbuka).
2. Ekspor **Wireframe Halaman 1** (Katalog Utama, termasuk contoh kartu *Stok Habis*).
3. Ekspor **Wireframe Halaman 2** (Detail Produk + Form Pemesanan WA).
4. Ekspor **Wireframe Halaman 3** (Dashboard Kelola Produk Merchant).
5. Penjelasan singkat **alur interaksi** (tombol mana menuju halaman mana) dan **bukti penerapan 3 Aturan UX Wajib** dari Sesi `03a`.
6. **Catatan Figma AI:** 1 saran AI yang kalian pakai, 1 saran yang kalian tolak, beserta alasannya.

---

## 6. Tugas Mandiri (Individual): Jembatan ke Kode HTML & CSS

- **Sifat:** Individu (dikerjakan di luar jam kelas dan di-*push* ke folder pribadimu di repo squad untuk dibahas saat Daily Standup besok pagi)
- **Target Waktu:** 25 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_03b.md`

> [!TIP]
> **Bekal Pre-Program → Jembatan Menuju Bulan 2:**  
> Di **2 bulan pre-program sebelumnya**, kamu sudah mempelajari dasar HTML dan CSS. Sekarang ubah rancangan kartu produk dari Wireframe Halaman 1 menjadi kode HTML & CSS statis hitam-putih dalam dua kondisi: **Stok Tersedia** dan **Stok Habis**!

### Instruksi:
1. Tulis kode HTML sederhana untuk 2 kartu produk versi wireframe (satu produk normal, satu produk dengan status **Stok Habis**).
2. Tulis CSS minimal hitam-putih (`border`, `padding`, `font-family: sans-serif`, dan style tombol aktif vs tombol nonaktif/`disabled`) agar menyerupai wireframe.
3. Simpan cuplikan kode beserta refleksi singkatmu di file `tugas_03b.md`.

### Contoh Hasil yang Diharapkan:
````markdown
# Tugas Mandiri 03b — Wireframe HTML/CSS Hitam-Putih
Nama: [Nama Kamu]

## 1. Kode HTML & CSS:
```html
<html>
  <head>
  </head>
  <body>
  </body>
</html>
```

## 2. Refleksi Singkat:
Mengubah wireframe menjadi HTML/CSS hitam-putih membantu saya melihat struktur komponen secara nyata—termasuk cara membedakan tampilan tombol saat stok masih ada vs saat stok habis untuk persiapan React di Bulan 2.
````

---

## 7. Cek Pemahaman Diri

1. Mengapa desainer dilarang memasukkan warna-warni estetik dan foto asli pada tahap pembuatan wireframe?
2. Mengapa pendekatan *Mobile-First* wajib diterapkan sejak awal saat merancang wireframe aplikasi UMKM lokal?
3. Bagaimana cara menandai produk yang stoknya `0` di wireframe Halaman 1 dan Halaman 2 agar selaras dengan prinsip pencegahan kesalahan (*Error Prevention*) dari Sesi `03a`?
4. Mengapa kita menggambar wireframe secara manual dulu sebelum meminta bantuan Figma AI? Apa risikonya kalau urutannya dibalik?
5. Ceritakan satu saran Figma AI yang kamu tolak dan alasanmu menolaknya!

---

Lanjut ke: **[03c-value-proposition-dan-model-bisnis.md](03c-value-proposition-dan-model-bisnis.md)**
