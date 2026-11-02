# Modul Belajar — Bulan 1: Fondasi Pra-Coding

Modul ini adalah bahan ajar untuk **12 Bulan Kurikulum Project-Based Learning** (Platform Katalog & Manajemen UMKM), khusus **Bulan 1 — Fondasi Pra-Coding**. Bulan ini dirancang untuk membangun otot berpikir dan merancang sebelum coding intensif di Bulan 2: AI Literacy, Computational Thinking & Algoritma, Desain Aplikasi & Bisnis, serta Pitching & Showcase. Otot ngoding yang sudah dipelajari sebelumnya tetap dijaga lewat latihan kode terarah setiap minggu.

Coding React & TypeScript secara intensif dimulai di **Bulan 2**.

---

## 1. Cara Pakai

- **Mentor:** Baca `PANDUAN-MENTOR.md` di tiap folder sebelum mengajar minggu tersebut. Isinya urutan sesi, alokasi waktu, jebakan umum, beban tugas mandiri, serta checklist kapabilitas murid.
- **Peserta:** Ikuti materi sesuai urutan nomor sesi. Setiap sesi memiliki materi inti, workshop praktik tim (**menghasilkan artefak squad**), dan satu tugas mandiri individual berdurasi 20–30 menit.
- Semua output bersifat berbasis produk (*product-based*) — berpusat pada satu produk nyata: **Katalog UMKM dengan Pemesanan via WhatsApp**.

---

## 2. Ritme Mingguan

| Hari | Aktivitas | Durasi |
|---|---|---|
| **Senin–Jumat** | Standup (10-15m) + Materi & Workshop (75-90m) + Tugas Mandiri (20-30m setelah sesi) | ±90–120 menit di kelas |
| **Sabtu** | Sprint Review Mingguan (Demo 5 menit + Q&A 3 menit per squad) + Retrospektif | ±120 menit |

Total: **6 sesi/minggu**, **24 sesi/bulan**.

---

## 3. Sistem Squad

Peserta (18 orang) dibagi ke dalam **6 squad rolling @3 orang**, dirotasi setiap 1–2 minggu. Meskipun belum ngoding penuh, peserta dibiasakan bekerja dalam format tim pengembang perangkat lunak sejak hari pertama: ada rotasi peran (Driver/Notulis, Navigator/Fasilitator, Spokesperson/Presenter), standup harian, dan peer review.

Evaluasi dilakukan melalui **Checklist Kapabilitas** (status: *Siap*, *Hampir Siap*, atau *Perlu Pendampingan*) bersama catatan feedback mentor, tanpa sistem nilai angka atau vonis kelulusan yang menghukum.

---

## 4. Struktur Folder Modul

```text
1-modul-pra-coding-bulan1/
├── README.md                                 # Ringkasan bulan 1
├── 0-Orientasi/                              # Hari pertama pembukaan
│   ├── PANDUAN-MENTOR.md
│   ├── 01-tentang-bulan-pertama.md
│   └── 02-cara-kerja-squad.md
│
├── 1-AI-Literacy/                            # Minggu 1 (6 sesi)
│   ├── PANDUAN-MENTOR.md
│   ├── 01a-pengenalan-ai-dan-etika.md
│   ├── 01b-ct-dan-problem-solving-dengan-ai.md
│   ├── 01c-prompt-engineering-dasar.md
│   ├── 01d-ai-untuk-aktivitas-harian.md
│   ├── 01e-ai-untuk-belajar-mandiri.md
│   └── 01f-review-dan-evaluasi-minggu1.md
│
├── 2-Computational-Thinking/                 # Minggu 2 (6 sesi)
│   ├── PANDUAN-MENTOR.md
│   ├── 02a-dekomposisi-dan-pengenalan-pola.md
│   ├── 02b-abstraksi-dan-algoritma.md
│   ├── 02c-flowchart.md
│   ├── 02d-erd-dasar.md
│   ├── 02e-latihan-terpadu-ct.md
│   └── 02f-review-dan-evaluasi-minggu2.md
│
├── 3-Desain-Aplikasi-dan-Bisnis/             # Minggu 3 (6 sesi)
│   ├── PANDUAN-MENTOR.md
│   ├── 03a-prinsip-ux-dasar.md
│   ├── 03b-wireframe-dan-merancang-tampilan.md
│   ├── 03c-value-proposition-dan-model-bisnis.md
│   ├── 03d-sudut-pandang-pelanggan-umkm.md
│   ├── 03e-dari-desain-ke-rencana-fitur.md
│   └── 03f-review-dan-evaluasi-minggu3.md
│
└── 4-Pitching-dan-Showcase/                  # Minggu 4 (6 sesi)
    ├── PANDUAN-MENTOR.md
    ├── 04a-pitching-dasar.md
    ├── 04b-ai-untuk-merancang-alur-aplikasi.md
    ├── 04c-menyusun-pitch-deck.md
    ├── 04d-gladi-resik-dan-peer-feedback.md
    ├── 04e-git-untuk-mengelola-artefak.md
    └── 04f-showcase-pitch-day.md
```

---

## 5. Artefak yang Dihasilkan Peserta

| Minggu | Artefak Tim (Squad) | Sentuhan Kode & Praktik Nyata | Tugas Mandiri (Individual) |
|---|---|---|---|
| **1: AI Literacy** | Piagam Etika AI Tribe, Cheat Sheet Prompt Engineering, Draf Solusi UMKM (Asumsi) | Pengingat jembatan kode Minggu 2 | Refleksi kasus etika, sparring dekomposisi AI, prompt R-C-I-C-O, kurasi konten, Log Socratic 01e, refleksi Sprint 1 |
| **2: Computational Thinking** | Peta dekomposisi (2 proses), pseudocode diskon/ongkir, 2 Flowchart (Pemesanan WA & Tambah Produk), Draf ERD (ItemPesanan & data pembeli) | **Jembatan Kode 1:** Fungsi JS hitung diskon/ongkir + dry run table | Latihan dekomposisi warung, fungsi JS logika bisnis, flowchart validasi, draf relasi ERD, uji konsistensi diagram, refleksi Sprint 2 |
| **3: Desain UX & Bisnis** | Laporan UX Review, Wireframe 3 Halaman, Value Proposition Canvas, Catatan Wawancara 1 UMKM Nyata, Persona & MoSCoW, Backlog Slice 0 | **Jembatan Kode 2:** Halaman HTML/CSS statis hitam-putih dari wireframe | Observasi UX harian, halaman HTML/CSS kartu produk, catatan wawancara UMKM, mini persona nyata, penulisan user story & AC, refleksi Sprint 3 |
| **4: Pitching & Showcase** | User flow tervalidasi alur WA, Pitch Deck 7 Slide berbasis riset nyata, Repositori GitHub terorganisir | **Jembatan Kode 3:** Commit & PR kode latihan JS dan HTML/CSS ke repositori | Naskah hook 30 detik, audit skenario gagal alur WA, review slide mandiri, refleksi gladi resik, verifikasi branch Git, refleksi akbar Bulan 1 |

---

## 6. Checkpoint Kapabilitas Keluar Bulan 1

Di akhir Bulan 1, setiap peserta dievaluasi kesiapannya melangkah ke Bulan 2 melalui **8 Checkpoint Kapabilitas**:

1. **Computational Thinking:** Mampu memecah alur masalah nyata menjadi langkah runtut dan tidak ambigu (Dekomposisi, Pola, Abstraksi, Algoritma/Pseudocode).
2. **Visualisasi Flowchart:** Mampu membaca dan membuat diagram alur sistem dengan simbol standar baku, alur percabangan jelas, dan penanganan kegagalan.
3. **Pemodelan Data ERD Dasar:** Mampu membedakan entitas, atribut, primary key, relasi 1:N, serta menyelesaikan relasi N:N menggunakan entitas penghubung (`ItemPesanan`).
4. **Wireframe Antarmuka Mobile-First:** Mampu membuat denah antarmuka sederhana (Katalog, Detail, Dashboard Merchant) yang memprioritaskan kemudahan pengguna UMKM.
5. **Empati Pengguna & Value Proposition:** Mampu merumuskan nilai solusi berbasis riset wawancara UMKM nyata dan menyusun persona yang membumi.
6. **AI Literacy & Etika:** Mampu menggunakan AI sebagai sparring partner terstruktur (formula R-C-I-C-O), memvalidasi fakta tanpa menelan halusinasi, dan menjaga etika belajar.
7. **Komunikasi & Pitching:** Mampu menyampaikan narasi produk (Problem → Solusi → Bukti/Artefak → Dampak → Roadmap) secara percaya diri dalam batas waktu.
8. **Version Control Git Dasar:** Mampu mengelola artefak digital dan latihan kode lewat alur kerja branch, commit, dan Pull Request di GitHub.

---

## 7. Rujukan Kurikulum

Modul ini mengacu pada dokumen induk `kurikulum-pbl-12-bulan.md` Bagian "Bulan 1 — Fondasi Pra-Coding" dan Bagian 3 (Learning Philosophy).
