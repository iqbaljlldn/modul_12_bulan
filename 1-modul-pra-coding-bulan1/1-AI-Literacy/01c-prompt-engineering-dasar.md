# 01c. Prompt Engineering Dasar: Cara Berkomunikasi Presisi dengan AI

**Minggu 1: AI Literacy | Sesi 3 (Rabu)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Cheat Sheet Prompt Engineering per Squad

---

## 1. Mengapa Ini Penting?

Banyak orang mengeluh: *"AI jawabannya muter-muter dan nggak sesuai harapan."*  
Masalahnya hampir selalu bukan pada kecerdasan AI-nya, melainkan pada cara kita memberikan perintah: **"Garbage In, Garbage Out"** (jika instruksi yang masuk asal-asalan, hasil yang keluar pun berantakan).

Jika kamu memberikan instruksi kabur, kamu akan mendapat jawaban acak. Namun jika kamu memberikan instruksi presisi, AI bisa menjadi asisten riset, analis alur, dan rekan diskusi yang luar biasa tajam.

Hari ini kita akan menguasai formula standar industri untuk menyusun prompt berkualitas tinggi.

---

## 2. Formula Anatomi Prompt: Kerangka R-C-I-C-O

Agar instruksimu tidak ambigu, gunakan kerangka **R-C-I-C-O**. Perhatikan baik-baik perbedaan antara kedua huruf **"C"** di dalamnya:

```text
┌────────────────────────────────────────────────────────────────────────┐
│                      FORMULA PROMPT R-C-I-C-O                          │
├────────────────────────────────────────────────────────────────────────┤
│ 1. [R] Role           : Siapa peran atau keahlian AI yang diinginkan?  │
│ 2. [C] Context        : Apa latar belakang, situasi, dan siapa user-nya?│
│                         (Penjelasan situasi / kondisi lapangan)        │
│ 3. [I] Instruction    : Perintah atau tugas spesifik yang diminta?     │
│ 4. [C] Constraint     : Apa batasan ketat, aturan, atau larangannya?   │
│                         (Pagar pembatas yang tidak boleh dilanggar)    │
│ 5. [O] Output         : Format bentuk penyajian hasil yang diinginkan? │
└────────────────────────────────────────────────────────────────────────┘
```

> [!IMPORTANT]
> **Perbedaan Kunci Dua "C":**
> - **Context (Konteks / Latar Belakang):** Menjelaskan dunia tempat masalah itu terjadi. *Contoh: "Warung sembako Bu Nur di desa, pembeli mayoritas ibu rumah tangga yang belanja harian."*
> - **Constraint (Batasan / Larangan):** Menaruh pagar agar AI tidak melantur. *Contoh: "Maksimal 5 kategori, jangan gunakan istilah bahasa Inggris, jangan sarankan fitur yang butuh laptop."*

### Mari Bandingkan Contohnya:

❌ **Prompt Pemula (Buruk & Asal-asalan):**
> *"Bikinin cara ngatur produk buat warung."*  
> *(Hasilnya: penjelasan 10 paragraf panjang tentang manajemen ritel modern ala supermarket besar yang mustahil diterapkan di warung kecil).*

✅ **Prompt Terstruktur (Formula R-C-I-C-O):**
> - **[Role]** Bertindaklah sebagai konsultan digitalisasi UMKM lokal Indonesia.  
> - **[Context / Latar Belakang]** Kami sedang merancang katalog digital untuk toko sembako kelontong Ibu Nur di desa. Bu Nur dan pelanggannya terbiasa belanja langsung dan kurang akrab dengan istilah teknologi rumit.  
> - **[Instruction / Perintah]** Buatkan skema pengelompokan (kategori) barang dagangan toko sembako yang paling masuk akal dan mudah dipahami.  
> - **[Constraint / Batasan]** Batasi maksimal 5 kategori utama. Jangan gunakan istilah bahasa Inggris (hindari kata seperti 'beverages' atau 'household').  
> - **[Output / Format Hasil]** Sajikan dalam bentuk tabel Markdown dengan kolom: Nama Kategori, Contoh Barang (3 buah), dan Alasan Pengelompokan.

Perhatikan perbedaannya: AI terkunci dalam ruang lingkup yang jelas dan menghasilkan jawaban yang langsung bisa digunakan!

---

## 3. Teknik Lanjutan: Zero-Shot vs Few-Shot

### 1. Zero-Shot Prompting (Tanpa Contoh)
Memberikan instruksi langsung tanpa menyertakan contoh sebelumnya.
- *Cocok untuk:* Pertanyaan konseptual sederhana, perangkuman umum, atau mencari variasi ide nama produk.
- *Contoh:* *"Jelaskan fungsi barcode pada kemasan barang warung dengan bahasa yang mudah dipahami."*

### 2. Few-Shot Prompting (Diberi Contoh Pola)
Memberikan 1 sampai 2 contoh pola masukan (*input*) dan keluaran (*output*) yang diinginkan sebelum meminta AI menyelesaikan tugas yang sesungguhnya.
- *Cocok untuk:* Menyamakan format data, menyeragamkan gaya bahasa, atau merapikan catatan yang berantakan.
- *Contoh:*
  ```text
  Ubah catatan lisan stok pedagang menjadi daftar ringkas terstruktur:

  Contoh 1:
  Masukan: "Beras rojolele sisa 10 karung harga seratus dua puluh ribu"
  Hasil:
  - Nama Barang: Beras Rojolele
  - Stok: 10 karung
  - Harga: Rp 120.000

  Contoh 2:
  Masukan: "Minyak botol kita tinggal 5 botol harganya empat belas ribu lima ratus"
  Hasil:
  - Nama Barang: Minyak Goreng Kita
  - Stok: 5 botol
  - Harga: Rp 14.500

  Sekarang ubah data berikut sesuai format di atas:
  Masukan: "Telur ayam sisa lima belas kilo sekilonya dua puluh delapan ribu"
  Hasil:
  ```

> [!NOTE]
> Format data yang lebih teknis (seperti JSON) akan kita pelajari secara bertahap saat kita mulai menghubungkan aplikasi React ke API di Bulan 2 dan 3. Untuk saat ini, fokuslah pada keteraturan daftar dan tabel.

---

## 4. Workshop Praktik Squad (60 Menit)

### Tugas 1: "Bedah & Perbaiki Prompt Buruk"
Ubah 3 prompt buruk berikut menjadi prompt profesional menggunakan formula lengkap R-C-I-C-O:
1. *"Gimana cara bikin toko online laku?"*
2. *"Kasih tahu data apa aja yang ada di warung kopi."*
3. *"Jelasin apa itu diagram alur."*

Uji versi buruk vs versi perbaikan ke AI kalian, lalu bandingkan hasilnya!

### Tugas 2: "Rancang Prompt Few-Shot"
Rancang sebuah prompt Few-Shot yang mampu mengubah deskripsi produk santai dari pedagang pakaian (misal: *"kaos oblong putih polos bahan katun combed ukuran XL sisa 3 pcs harga lima puluh ribu"*) menjadi kartu informasi produk yang rapi (Nama Barang, Kategori, Ukuran, Bahan, Stok, Harga).

---

## 5. Output Sesi: Cheat Sheet Prompt Engineering Squad

Tiap squad mengompilasi lembar panduan mini (file Markdown) yang berisi:
1. Penjelasan formula R-C-I-C-O versi squad beserta perbedaan tegas Context vs Constraint.
2. 3 Contoh prompt teruji yang dirancang khusus untuk studi kasus Platform Katalog UMKM.
3. 1 Contoh prompt Few-Shot format rapi.
4. Daftar "5 Kata Pantangan" saat meminta bantuan ke AI.

---

## 6. Tugas Mandiri (Individual)

- **Sifat:** Individu (dikerjakan sendiri di luar jam kelas)
- **Target Waktu:** 25 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_01c.md`

### Instruksi:
1. Pilih satu usaha kecil di dekat rumahmu (misal: penjual gorengan, warung jus buah, atau tukang pangkas rambut).
2. Tuliskan satu prompt lengkap dengan kerangka R-C-I-C-O untuk membantu usaha tersebut (misal: membuat daftar menu atau jadwal operasional mingguan).
3. Tandai dengan jelas bagian mana yang merupakan **Context (Latar Belakang)** dan mana yang **Constraint (Batasan)**.
4. Salin jawaban yang diberikan AI dan berikan penilaian 1 kalimat: apakah jawabannya sudah sesuai batasanmu?

### Contoh Hasil yang Diharapkan:
```markdown
# Tugas Mandiri 01c — Prompt Formula R-C-I-C-O
Nama: [Nama Kamu]
Target Usaha: Warung Jus Buah Segar Pak Mamat

## 1. Draf Prompt Saya:
[Role] Bertindaklah sebagai konsultan menu minuman sehat untuk pedagang gerobak.
[Context] Pak Mamat berjualan jus buah di depan sekolah dasar. Modal terbatas, blender hanya ada 2, dan waktu istirahat anak SD hanya 20 menit sehingga penyajian harus cepat.
[Instruction] Buatkan rekomendasi 4 kombinasi jus buah yang paling mudah dibuat, disukai anak-anak, dan terjangkau.
[Constraint] Bahan baku maksimal 2 kombinasi buah per menu. Jangan gunakan buah impor mahal seperti kiwi atau stroberi Jepang. Harga jual modal bahan di bawah Rp 5.000 per gelas.
[Output] Tabel dengan kolom: Nama Menu, Bahan, Estimasi Waktu Blender, Alasan Disukai Siswa.

## 2. Penilaian Terhadap Hasil AI:
AI memberikan 4 menu yang realistis (Jus Mangga Semangka, Jus Jeruk Melon, Jus Alpukat Cokelat, Jus Sirsak). Seluruh bahan mudah ditemukan di pasar lokal dan memenuhi batasan harga saya.
```

---

## 7. Cek Pemahaman Diri

1. Apa bedanya **Context (Latar Belakang)** dengan **Constraint (Batasan)** dalam menyusun prompt? Berikan contohnya!
2. Kapan teknik **Few-Shot Prompting** jauh lebih unggul dibandingkan hanya memberikan instruksi tanpa contoh?

---

Lanjut ke: **[01d-ai-untuk-aktivitas-harian.md](01d-ai-untuk-aktivitas-harian.md)**
