# 01c. Prompt Engineering Dasar: Cara Mengobrol dengan AI

**Minggu 1: AI Literacy | Sesi 3 (Rabu)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Cheat Sheet Prompt Engineering per Squad

---

## 1. Mengapa Ini Penting?

Banyak orang mengeluh: *"AI jawabannya muter-muter dan nggak sesuai harapan."*  
Masalahnya hampir selalu bukan pada kecerdasan AI-nya, melainkan pada kualitas perintah yang diberikan: **"Garbage In, Garbage Out"**.

Jika kamu memberikan instruksi kabur, kamu akan mendapat jawaban acak. Namun jika kamu memberikan instruksi presisi, AI bisa menjadi asisten riset, analis data, dan konsultan produk yang luar biasa tajam.

Hari ini kita akan mempelajari cara menyusun prompt profesional menggunakan kerangka standar industri.

---

## 2. Anatomi Prompt Profesional: Kerangka R-C-I-C-O

Prompt berkinerja tinggi umumnya mengandung 5 elemen berikut:

```text
┌────────────────────────────────────────────────────────┐
│              ANATOMI PROMPT PROFESIONAL                │
├────────────────────────────────────────────────────────┤
│ 1. [R] Role       : Siapa peran AI yang diinginkan?    │
│ 2. [C] Context    : Apa latar belakang & situasinya?   │
│ 3. [I] Instruction: Tindakan spesifik apa yang diminta?│
│ 4. [C] Constraint : Apa batasan atau larangan tegasnya?│
│ 5. [O] Output     : Bagaimana format hasil yang dicari?│
└────────────────────────────────────────────────────────┘
```

### Mari bandingkan contohnya:

❌ **Prompt Pemula (Buruk):**
> *"Bikinin cara ngatur produk buat warung."*  
> *(Hasilnya: penjelasan 10 paragraf panjang lebar tentang manajemen ritel modern yang tidak relevan untuk warung kecil).*

✅ **Prompt Terstruktur (Profesional):**
> **[Role]** Bertindaklah sebagai konsultan digitalisasi UMKM berpengalaman di Indonesia.  
> **[Context]** Kami sedang merancang katalog digital untuk toko sembako kelontong milik Ibu Nur di pedesaan Jawa Tengah. Bu Nur tidak terbiasa dengan istilah teknologi rumit.  
> **[Instruction]** Buatkan skema pengelompokan (kategori) barang dagangan toko sembako yang paling masuk akal dan mudah dipahami oleh pembeli maupun Bu Nur.  
> **[Constraint]** Batasi maksimal 5 kategori utama. Jangan gunakan istilah bahasa Inggris (hindari kata seperti 'beverages' atau 'household').  
> **[Output Format]** Sajikan dalam bentuk tabel Markdown dengan kolom: Nama Kategori, Contoh Produk (3 buah), dan Alasan Pengelompokan.

Perhatikan perbedaannya: AI dipaksa berpikir dalam ruang lingkup yang sempit dan menghasilkan tepat apa yang kamu butuhkan.

---

## 3. Teknik Lanjutan: Zero-Shot vs Few-Shot

### 1. Zero-Shot Prompting
Memberikan instruksi langsung tanpa memberikan contoh sebelumnya.
- *Cocok untuk:* Pertanyaan konseptual sederhana atau perangkuman umum.
- *Contoh:* *"Jelaskan fungsi barcode pada sistem kasir minimarket."*

### 2. Few-Shot Prompting
Memberikan 1 sampai 3 contoh pola input-output yang diinginkan sebelum meminta AI menyelesaikan tugas sesungguhnya.
- *Cocok untuk:* Memastikan gaya bahasa konsisten, standardisasi format, atau ekstraksi data.
- *Contoh:*
  ```text
  Tolong ubah catatan informal stok pedagang menjadi format JSON:

  Contoh 1:
  Input: "Beras rojolele sisa 10 karung harga seratus dua puluh ribu"
  Output: {"nama": "Beras Rojolele", "stok": 10, "satuan": "karung", "harga": 120000}

  Contoh 2:
  Input: "Minyak goreng kita tinggal 5 botol harganya empat belas ribu lima ratus"
  Output: {"nama": "Minyak Goreng Kita", "stok": 5, "satuan": "botol", "harga": 14500}

  Sekarang kerjakan data berikut:
  Input: "Telur ayam sisa lima belas kilo sekilonya dua puluh delapan ribu"
  Output:
  ```

---

## 4. Prompting untuk Belajar & Debugging Logika

Sebagai calon engineer, gunakan template prompt berikut saat mempelajari materi sulit:

### A. Template Analogi Konsep (Feynman Technique)
> *"Saya sedang mempelajari konsep [Konsep, misal: Relasi Data 1-ke-Banyak]. Jelaskan konsep ini menggunakan analogi kehidupan sehari-hari penjual bakso keliling. Hindari jargon teknis di awal."*

### B. Template Uji Ketahanan Logika (Red Teaming)
> *"Berikut adalah draf alur flowchart pembayaran pesanan yang kami buat: [Sebutkan langkah]. Bertindaklah sebagai penguji sistem yang kritis. Tunjukkan 3 celah atau skenario tak terduga di mana alur ini bisa macet atau membuat pelanggan bingung."*

---

## 5. Workshop Praktik Squad (60 Menit)

### Tugas 1: "Bedah & Perbaiki Prompt Buruk"
Ubah 3 prompt buruk berikut menjadi prompt profesional menggunakan kerangka R-C-I-C-O:
1. *"Gimana cara bikin toko online laku?"*
2. *"Kasih tahu data apa aja yang ada di warung kopi."*
3. *"Jelasin apa itu ERD."*

Ujicobakan versi buruk vs versi perbaikan ke AI, dan dokumentasikan perbedaan mutunya!

### Tugas 2: "Eksperimen Few-Shot"
Rancang sebuah prompt Few-Shot yang mampu mengubah deskripsi produk acak dari penjual baju thrift menjadi spesifikasi produk katalog yang rapi (Nama Produk, Ukuran, Bahan, Kondisi, Harga).

---

## 6. Output Sesi: Cheat Sheet Prompt Engineering Squad

Tiap squad mengompilasi lembar panduan mini (maksimal 2 halaman Markdown) yang berisi:
1. Ringkasan formula R-C-I-C-O versi squad.
2. 3 Contoh prompt teruji untuk studi kasus Platform UMKM (misal: Prompt Riset Kebutuhan Mitra, Prompt Validasi Alur, Prompt Format Data).
3. Daftar "Kata Terlarang / Hindari" saat memberi prompt ke AI.

---

## 7. Cek Pemahaman Diri

1. Apa akibatnya jika kita tidak memberikan **Constraint** (batasan) pada prompt kita?
2. Kapan sebaiknya kita menggunakan teknik **Few-Shot** daripada **Zero-Shot**?

Lanjut ke: **[01d-ai-untuk-aktivitas-harian.md](file:///home/iqbaal/gelombang-3/modul%2012%20bulan/modul-pra-coding-bulan1/1-AI-Literacy/01d-ai-untuk-aktivitas-harian.md)**
