# 03d. Sudut Pandang Pelanggan: Persona UMKM & Prioritisasi Fitur

**Minggu 3: Desain Aplikasi & Bisnis | Sesi 4 (Kamis)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Dokumen Persona UMKM + Daftar Fitur Prioritas (Metode MoSCoW)

---

## 1. Mengapa Ini Penting?

Bila kamu bertanya ke calon pengguna: *"Ibu mau aplikasi yang kayak gimana?"*  
Jawabannya hampir pasti: *"Mau yang bisa semuanya mas! Mau ada live streaming, ada pinjaman online, ada game berhadiah, ada gratis ongkir!"*

Jika seorang engineer mencoba mengabulkan semua permintaan itu sekaligus:
- Proyek akan molor berbulan-bulan (*scope creep*).
- Aplikasi menjadi terlalu berat dan rumit.
- Produk akhirnya tidak pernah selesai dirilis.

Kunci sukses produk software adalah **fokus tajam pada satu profil pengguna nyata (Persona)** dan **keberanian memprioritaskan fitur mana yang wajib ada sekarang vs mana yang ditunda**.

---

## 2. Mengenal User Persona

**User Persona** adalah representasi fiktif yang realistis dari pengguna ideal produk kita, berdasarkan fakta dan perilaku di lapangan.

### Contoh Persona UMKM:

```text
┌────────────────────────────────────────────────────────┐
│ PROFIL: Ibu Sri Mulyani (48 Tahun)                    │
│ Usaha : Sambal Pecel Madiun "Berkah Ibu"               │
│ Lokasi: Sidoarjo, Jawa Timur                           │
├────────────────────────────────────────────────────────┤
│ Perilaku Teknologi:                                    │
│ - Menggunakan smartphone Android kelas pemula (RAM 3GB)│
│ - Sangat lancar memakai WhatsApp & Facebook            │
│ - Takut mengklik menu berbahasa Inggris                │
│ - Selalu mengetik pesan dengan satu jari telunjuk      │
├────────────────────────────────────────────────────────┤
│ Masalah Terbesar (Pains):                              │
│ - Tiap pagi harus membalas puluhan chat: "Masih ada    │
│   sambal pedas sedang nggak bu? Harganya berapa?"      │
│ - Sering salah catat pesanan karena chat tertimbun     │
├────────────────────────────────────────────────────────┤
│ Harapan (Gains):                                       │
│ - Punya satu link simpel yang bisa ditaruh di bio WA   │
│ - Pembeli langsung lihat daftar rasa & stok yang sisa  │
└────────────────────────────────────────────────────────┘
```

Saat mendesain fitur, kamu tidak lagi bertanya: *"Keren nggak ya kalau ditambah fitur X?"*  
Melainkan: *"Apakah Bu Sri bisa dan mau memakai fitur X ini tanpa merasa pusing?"*

---

## 3. Brainstorming dengan AI & Metode Prioritisasi MoSCoW

### Menggunakan AI untuk Brainstorming Ide Fitur:
Kamu bisa meminta bantuan AI untuk memikirkan ide-ide fitur yang mungkin tidak terpikirkan sebelumnya:
> *"Berikut adalah profil persona Bu Sri: [masukkan profil di atas]. Berikan 10 ide fitur aplikasi web katalog yang paling relevan untuk membantu operasional jualan sambal Bu Sri secara ringkas."*

### Menyaring Hasil AI dengan Kerangka MoSCoW:
Dari 10 ide AI, kita wajib memilahnya ke dalam 4 kategori:

```text
┌──────────────┬────────────────────────────────────────────────────────┐
│  M - Must    │ Wajib Ada: Tanpa fitur ini, aplikasi tidak bisa jalan! │
│              │ (Contoh: Menampilkan daftar produk & tombol pesan WA). │
├──────────────┼────────────────────────────────────────────────────────┤
│  S - Should  │ Seharusnya Ada: Sangat penting tapi ada solusi alternatif│
│              │ sementara. (Contoh: Filter pencarian kategori).        │
├──────────────┼────────────────────────────────────────────────────────┤
│  C - Could   │ Bisa Ada: Fitur pelengkap yang bagus jika ada waktu.   │
│              │ (Contoh: Cetak struk pesanan format PDF).              │
├──────────────┼────────────────────────────────────────────────────────┤
│  W - Won't   │ Tidak Dulu: Jangan dibuat di tahap awal (Bulan 1-2).   │
│              │ (Contoh: Fitur live streaming dan integrasi AI chatbot)│
└──────────────┴────────────────────────────────────────────────────────┘
```

---

## 4. Workshop Praktik Squad (60 Menit)

### Tugas 1: Buat 1 Persona Merchant & 1 Persona Buyer
Buat profil lengkap persona nyata untuk Platform Katalog UMKM squad-mu (nama, foto/karikatur, demografi, alat yang dipakai, frustrasi harian, dan cita-cita usahanya).

### Tugas 2: Brainstorming AI & MoSCoW Sorting
1. Gunakan prompt terstruktur ke LLM untuk menghasilkan minimal 10 ide fitur yang menjawab penderitaan kedua persona tersebut.
2. Diskusikan di dalam squad dan kelompokkan 10 ide tersebut ke dalam tabel **MoSCoW Matrix**.
3. Tetapkan **Maksimal 3 Fitur "Must-Have"** yang akan menjadi fokus utama implementasi di Bulan 2 nanti.

---

## 5. Output Sesi

Kumpulkan dokumen Markdown berisi:
- Dokumen Persona Merchant & Buyer lengkap.
- Bukti log prompt brainstorming AI.
- Tabel Prioritas Fitur MoSCoW beserta alasan mengapa fitur tertentu digolongkan sebagai *Must-Have* atau *Won't-Have*.

---

## 6. Cek Pemahaman Diri

1. Mengapa seorang software engineer dilarang keras mencoba membuat semua fitur yang disarankan pengguna di rilis pertama aplikasinya?
2. Bagaimana persona Bu Sri mempengaruhi keputusan kita dalam memilih ukuran font dan tata letak tombol di wireframe?

Lanjut ke: **[03e-dari-desain-ke-rencana-fitur.md](file:///home/iqbaal/gelombang-3/modul 12 bulan/modul-pra-coding-bulan1/3-Desain-Aplikasi-dan-Bisnis/03e-dari-desain-ke-rencana-fitur.md)**
