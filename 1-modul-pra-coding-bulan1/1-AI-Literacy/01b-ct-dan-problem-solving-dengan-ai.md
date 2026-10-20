# 01b. Computational Thinking & Problem Solving dengan AI

**Minggu 1: AI Literacy | Sesi 2 (Selasa)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Dokumen Dekomposisi Masalah (Komparasi Berpikir Sendiri vs Bantuan AI)

---

## 1. Mengapa Ini Penting?

Komputer dan AI hanyalah alat eksekusi. Mereka tidak bisa menyelesaikan masalah jika kamu sendiri tidak bisa merumuskan masalah tersebut secara terstruktur.

Keterampilan merumuskan masalah secara logis dan terstruktur disebut **Computational Thinking (CT)**. Ini adalah fondasi nomor satu seorang software engineer. Hari ini kita akan berkenalan dengan 4 pilar CT dan mempraktikkan bagaimana berkolaborasi dengan AI untuk menajamkan analisis masalah kita, bukan menggantikan otak kita.

---

## 2. Konsep Inti: 4 Pilar Computational Thinking

Bayangkan kamu diminta menyelesaikan masalah rumit: **"Sebuah warung makan nasi Padang sering kehabisan lauk rendang di jam makan siang, tapi lauk gulai sayur selalu bersisa banyak dan terbuang."**

Bagaimana 4 pilar CT membedah masalah ini?

```text
       ┌────────────────────────────────────────────────────────┐
       │             4 PILAR COMPUTATIONAL THINKING             │
       └────────────────────────────────────────────────────────┘
            │                  │                  │                  │
            ▼                  ▼                  ▼                  ▼
     1. DEKOMPOSISI      2. POLA (PATTERN)   3. ABSTRAKSI       4. ALGORITMA
     Pecah jadi kecil    Cari pengulangan    Fokus inti saja    Langkah runtut
```

### 1. Dekomposisi (*Decomposition*)
Memecah masalah besar yang membingungkan menjadi potongan-potongan kecil yang dapat dikelola (*manageable*).
- *Contoh:* Daripada pusing memikirkan "warung rugi", kita pecah:
  1. Proses pembelian bahan mentah di pasar pagi.
  2. Proses estimasi porsi memasak.
  3. Proses pencatatan pesanan kasir.
  4. Pola kedatangan pelanggan per jam.

### 2. Pengenalan Pola (*Pattern Recognition*)
Mencari kesamaan, tren, atau pola berulang di antara bagian-bagian masalah.
- *Contoh:* Kita melihat data catatan 2 minggu terakhir:
  - Pada hari Jumat siang, pembeli rendang naik 200% (karena banyak karyawan kantor mampir setelah salat Jumat).
  - Pada hari hujan lebat, pembeli makan di tempat turun drastis tetapi pesanan bungkus lewat ojek online meningkat.

### 3. Abstraksi (*Abstraction*)
Menyingkirkan detail-detail yang tidak relevan dan hanya berfokus pada informasi yang esensial.
- *Contoh:* Warna cat dinding warung, merek piring makan, atau obrolan santai pelanggan tidak relevan dengan stok lauk. Yang esensial: **Waktu, Jumlah Porsi Rendang Tersedia, Jumlah Porsi Terjual, Sisa Lauk**.

### 4. Perancangan Algoritma (*Algorithm Design*)
Menyusun aturan atau langkah-langkah bertahap yang runtut dan tidak ambigu untuk menyelesaikan masalah.
- *Contoh:*
  ```text
  JIKA hari == "Jumat" MAKA
      Masak rendang = 150 porsi
  LAINNYA
      Masak rendang = 70 porsi
  JIKA stok rendang tersisa <= 15 porsi SEBELUM jam 13:00 MAKA
      Tampilkan tanda "Stok Menipis" di etalase kasir
  ```

---

## 3. Berpikir Mandiri Dulu, Lalu Kolaborasi dengan AI

Bagaimana cara terbaik memadukan 4 pilar CT dengan AI?

```text
[ Otak Manusia ]                     [ AI Asisten ]
1. Brainstorming manual awal   ──►   2. Minta variasi sudut pandang
3. Seleksi poin yang masuk akal ──►   4. Minta AI menguji celah (edge cases)
5. Keputusan akhir manusia
```

- **Jangan:** Membuka AI dan mengetik: *"Pecahkan masalah stok warung makan."* (Hasilnya akan klise dan umum).
- **Lakukan:** Tulis dekomposisi versi kalian dulu di kertas, lalu tanyakan ke AI: *"Kami memecah proses stok warung Padang menjadi 4 bagian berikut: [A, B, C, D]. Menurutmu, titik rawan atau langkah apa yang mungkin terlewat dari proses ini?"*

---

## 4. Workshop Praktik Squad (60 Menit)

Pilihlah salah satu dari dua skenario masalah UMKM berikut:

### Skenario 1: "Toko Kelontong Bu Rahma — Barang Sering Hilang / Kadaluwarsa"
Toko kelontong Bu Rahma memiliki 300 jenis barang. Seringkali barang kalengan yang ada di rak pojok sudah melewati tanggal kadaluwarsa tanpa disadari, sementara minyak goreng sering habis tiba-tiba karena tidak terpantau.

### Skenario 2: "Laundry Kiloan Mas Dwi — Pakaian Tertukar & Antrean Menumpuk"
Di musim hujan, antrean cuci pakaian di laundry Mas Dwi menumpuk dari 3 hari menjadi 7 hari. Pelanggan komplain karena beberapa baju kemeja putih kelunturan dan celana jeans tertukar pemiliknya.

### Langkah Kerja:
1. **Langkah 1 (Berpikir Manual - 25 Menit):**
   - Tanpa membuka AI, squad menuliskan pemecahan masalah memakai lembar kerja 4 Pilar CT (Dekomposisi, Pola, Abstraksi, Algoritma).
2. **Langkah 2 (Sparring Partner dengan AI - 20 Menit):**
   - Buka LLM. Masukkan hasil pemikiran kalian ke AI dan minta masukan:
     > *"Kami sedang membedah masalah [Skenario] menggunakan 4 pilar Computational Thinking. Ini rancangan awal kami: [...]. Analisislah rancangan kami: di mana kelemahannya? Skenario tak terduga apa yang belum kami antisipasi?"*
3. **Langkah 3 (Sintesis & Keputusan - 15 Menit):**
   - Evaluasi kritik AI. Putuskan mana saran AI yang bernilai tinggi dan mana yang tidak realistis untuk diterapkan di warung lokal.

---

## 5. Output Sesi: Lembar Kerja Dekomposisi Masalah

Kumpulkan file Markdown atau foto lembar kerja fisik squad dengan format:

```markdown
# Analisis CT — [Nama Skenario] (Squad [Nama])

## 1. Dekomposisi
- Komponen Masalah Versi Kami: [1, 2, 3...]
- Masukan AI yang Diterima: [...]
- Alasan Menerima/Menolak Saran AI: [...]

## 2. Pengenalan Pola
- Pola/Tren yang Berulang: [...]

## 3. Abstraksi
- Informasi Kritis yang Wajib Dicatat Sistem: [...]
- Detail yang Diabaikan (Noise): [...]

## 4. Draf Algoritma Awal
- Langkah 1: ...
- Langkah 2: JIKA ... MAKA ...
- Langkah 3: ...
```

---

## 6. Cek Pemahaman Diri

1. Apa perbedaan mendasar antara *Dekomposisi* dan *Abstraksi*?
2. Mengapa kita disarankan merumuskan dekomposisi sendiri sebelum bertanya kepada AI?

Lanjut ke: **[01c-prompt-engineering-dasar.md](file:///home/iqbaal/gelombang-3/modul%2012%20bulan/modul-pra-coding-bulan1/1-AI-Literacy/01c-prompt-engineering-dasar.md)**
