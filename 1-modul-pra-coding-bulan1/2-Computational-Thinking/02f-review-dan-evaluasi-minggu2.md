# 02f. Review Mingguan: Sprint Review Gabungan (Minggu 1 & 2) & Bug Hunt

**Minggu 2: Computational Thinking & Algoritma | Sesi 5 (Sabtu)**  
**Target Waktu:** 120 Menit (Tanpa Tugas Mandiri Akhir Pekan)  
**Output Sesi:** Checklist Kapabilitas Minggu 1 & 2, Blueprint & Diagram Tervalidasi, Catatan Retrospektif

---

## 1. Format Sesi Hari Sabtu

Hari Sabtu adalah momen akuntabilitas untuk mengunci kembali ritme mingguan Tribe (Senin–Sabtu). Seluruh squad akan mempresentasikan karya puncak logika sistem mereka (sekaligus membuktikan penerapan AI Literacy dari Minggu 1) di hadapan mentor dan rekan tribe.

> [!NOTE]
> **Sabtu Bebas PR:** Tidak ada tugas mandiri individual setelah sesi Sabtu selesai. Seluruh evaluasi, tantangan praktik, dan refleksi diselesaikan tuntas di dalam kelas selama 120 menit agar kamu bisa beristirahat di akhir pekan sebelum memulai Minggu 3.

```text
┌─────────────────────────────────────────────────────────────┐
│                 AGENDA SPRINT REVIEW SABTU                  │
├─────────────────┬───────────────────────────────────────────┤
│ 1. Showcase     │ Presentasi Blueprint, ERD, & AI Sparring  │
│    (50 Menit)   │ (6 squad x 8 menit: 5m presentasi + 3m QA)│
├─────────────────┼───────────────────────────────────────────┤
│ 2. Uji Praktik  │ Live Bug Hunt: Membedah Blueprint &       │
│    (35 Menit)   │ Diagram Cacat yang ditampilkan Mentor     │
├─────────────────┼───────────────────────────────────────────┤
│ 3. Retrospektif │ Refleksi tim (Mad/Sad/Glad) & pengumuman  │
│    (35 Menit)   │ rolling squad baru untuk Minggu 3 & 4     │
└─────────────────┴───────────────────────────────────────────┘
```

---

## 2. Bagian 1: Showcase Portofolio Squad (50 Menit)

Setiap squad memiliki waktu **5 menit presentasi + 3 menit sesi kritik/tanya jawab**. Agar waktu 5 menit efektif dan seluruh anggota berbicara secara adil, bagi peran presentasi kepada 3 anggota squad dengan fokus pada karya puncak minggu ini:

| Peran Presenter | Durasi | Materi yang Didemokan |
|---|---|---|
| **Presenter 1**<br>*(Data Architect)* | **1,5 Menit** | **ERD Katalog UMKM (`02d`):** Tunjukkan struktur 5 entitas, penempatan `PK` & `FK`, serta bukti tabel simulasi baris data nyata antara `PESANAN` dan `ITEM_PESANAN`. |
| **Presenter 2**<br>*(Logic Architect)* | **2 Menit** | **Blueprint Fitur Terpadu (`02e`):** Tunjukkan fitur baru yang dipilih squad (Opsi A / Opsi B), alur Pseudocode & Flowchart-nya, serta **Tabel Audit Konsistensi** yang membuktikan tidak ada variabel siluman. |
| **Presenter 3**<br>*(AI & Code Bridge)* | **1,5 Menit** | **Bukti AI Sparring (M1) & Jembatan Kode JS (`02b`):** Tunjukkan 1 contoh prompt terbaik berformat **R-C-I-C-O** yang dipakai squad saat menguji celah logika bersama AI (mana saran AI yang diterima/ditolak), serta hasil uji fungsi JS `hitungTotalBayar`. |
| **Sesi Q&A & Live Tracing** | **3 Menit** | **Uji Lacak Mentor:** Mentor akan menunjuk 1 skenario ekstrem secara acak pada Flowchart/ERD kalian (misal: *"Jika stok di database tiba-tiba 0 saat tombol ditekan, panah diagrammu lari ke mana dan atribut tabel mana yang berubah?"*). Squad harus menunjukkan jalurnya secara tepat. |

---

## 3. Bagian 2: Tantangan Praktik Live — "Bug Hunt: Bedah Blueprint Cacat" (35 Menit)

Pada sesi ini, **mentor akan menampilkan sebuah studi kasus Pseudocode, Flowchart, dan ERD yang cacat di layar proyektor** (soal dirahasiakan hingga sesi dimulai!).

### Aturan Main Live Bug Hunt:
1. **Waktu Berburu Bug (15 Menit):**  
   Setiap squad berdiskusi tanpa bantuan AI untuk menemukan **4 kesalahan fatal** yang tersembunyi di dalam diagram proyektor dan menuliskan perbaikannya di lembar kerja tim.
2. **Pembahasan & Debat Terbuka (20 Menit):**  
   Mentor menunjuk perwakilan squad secara bergantian untuk membedah 1 bug yang mereka temukan dan menjelaskan bagaimana cara memperbaikinya.

### Kisi-Kisi 4 Celah Bug yang Wajib Diwaspadai:
Pastikan squad-mu memahami 4 jebakan klasik berikut sebelum sesi dimulai:
1. **Jebakan Alur Flowchart:** Simbol *Decision* (`{...}`) yang hanya memiliki satu panah keluar (tidak ada cabang `Tidak`), atau cabang error yang menggantung tanpa kembali ke input / menuju `Selesai`.
2. **Jebakan Mismatch Logika vs ERD:** Kondisi yang diperiksa di Pseudocode/Flowchart, tetapi kolom atributnya lupa dibuat di dalam tabel ERD.
3. **Jebakan Tabel Campur Aduk (*Redundancy*):** Menyimpan data profil toko atau riwayat transaksi pembeli langsung di dalam tabel master `PRODUK`.
4. **Jebakan Relasi Banyak-ke-Banyak (`N:N`):** Menghubungkan dua entitas `N:N` secara langsung tanpa entitas penghubung (*Junction Entity*), atau lupa mengunci `harga_satuan` di tabel penghubung.

---

## 4. Bagian 3: Sprint Retrospective & Persiapan Rolling Squad (35 Menit)

Karena Minggu 2 menandai berakhirnya paruh pertama Bulan 1, seluruh refleksi dilakukan bersama di dalam kelas menggunakan papan **Mad, Sad, Glad** sebelum pengumuman rotasi squad baru:

| Kolom Refleksi | Pertanyaan Diskusi Squad (15 Menit) |
|---|---|
| **Mad (Hambatan)** | Kendala komunikasi atau kebiasaan apa yang sempat menghambat kerja squad selama 2 minggu ini? |
| **Sad (Belum Optimal)** | Bagian materi mana (Pseudocode, Flowchart, ERD, atau fungsi JS) yang masih terasa paling menantang? |
| **Glad (Keberhasilan)** | Pencapaian apa yang paling membanggakan dari squad kalian, dan apresiasi apa yang ingin kalian berikan ke rekan satu tim? |

### Penutup Sesi (20 Menit):
1. **Berbagi Pelajaran Berharga (*Key Learnings*):** Perwakilan tiap squad menyampaikan 1 pelajaran terpenting dari 2 minggu pertama.
2. **Pengumuman Rolling Squad Minggu 3 & 4:** Mentor mengumumkan komposisi anggota squad yang baru untuk memasuki fase **Desain UX (Wireframe), Model Bisnis, & Wawancara UMKM Nyata** di hari Senin.

---

## 5. Output Sesi

1. Berita acara presentasi Showcase dan catatan umpan balik mentor.
2. Lembar jawaban tim dari sesi **Live Bug Hunt**.
3. Papan catatan Retrospektif Squad (*Mad, Sad, Glad*).

---

## 6. Checklist Kapabilitas Gabungan (Minggu 1 & Minggu 2)

Mentor memeriksa ketercapaian kapabilitas setiap peserta dengan 3 status: **Siap**, **Hampir Siap**, atau **Perlu Pendampingan**.

| Indikator Kapabilitas | Bukti Evaluasi | Status | Catatan Feedback Mentor |
|---|---|---|---|
| **AI Literacy & Prompt R-C-I-C-O (M1)** | Menggunakan formula R-C-I-C-O, melakukan kurasi manual atas halusinasi AI, dan menuntaskan artefak Minggu 1 (`tugas_01a` s/d `01e`) | [ ] Siap<br>[ ] Hampir Siap<br>[ ] Perlu Pendampingan | |
| **Dekomposisi & Pseudocode (M2)** | Langkah runtut, menggunakan kata kunci baku (`JIKA ... MAKA ... LAINNYA`), bebas dari makna ganda | [ ] Siap<br>[ ] Hampir Siap<br>[ ] Perlu Pendampingan | |
| **Kebenaran Flowchart (M2)** | Simbol standar, percabangan jelas (Ya/Tidak), alur pemesanan WA lengkap tanpa panah buntu | [ ] Siap<br>[ ] Hampir Siap<br>[ ] Perlu Pendampingan | |
| **Model Data ERD Dasar (M2)** | Entitas dan atribut terpisah benar, memahami PK/FK, serta relasi 1:N dan N:N (`ITEM_PESANAN`) | [ ] Siap<br>[ ] Hampir Siap<br>[ ] Perlu Pendampingan | |
| **Sinkronisasi Blueprint (`02e`)** | Mampu menyelaraskan Pseudocode, Flowchart, dan ERD tanpa variabel siluman | [ ] Siap<br>[ ] Hampir Siap<br>[ ] Perlu Pendampingan | |
| **Jembatan Kode JavaScript (`02b`)** | Mampu menerjemahkan pseudocode ke fungsi JS sederhana (`tugas_02b.md`) dan mencocokkan dry run table | [ ] Siap<br>[ ] Hampir Siap<br>[ ] Perlu Pendampingan | |
| **Analisis Live Bug Hunt (`02f`)** | Menemukan minimal 3 dari 4 celah kesalahan pada diagram uji Sabtu | [ ] Siap<br>[ ] Hampir Siap<br>[ ] Perlu Pendampingan | |

> *Catatan Mentor:* Peserta berstatus **Perlu Pendampingan** akan mendapatkan sesi klinik penelusuran diagram (*tracing clinic*) selama 15 menit bersama mentor atau rekan pairing sebelum memulai workshop Wireframe di Minggu 3.

---

## 7. Penutup Minggu 2 & Menatap Minggu 3

Kerja luar biasa! Kamu sudah menyelesaikan paruh pertama Bulan 1. Kamu sekarang mampu membedah masalah seperti seorang software engineer: terstruktur, logis, dan teliti.

Namun, sistem yang logikanya sempurna tetap bisa gagal total jika **tampilannya membingungkan pengguna awam (UX buruk)** atau **tidak menyelesaikan masalah nyata pedagang (Value Proposition meleset)**.

Selamat beristirahat di akhir pekan! Di **Minggu 3**, kita akan mempelajari dunia **Desain Antarmuka (Wireframe) & Riset Pengguna Nyata UMKM** bersama squad barumu!

---

Lanjut ke: **[3-Desain-Aplikasi-dan-Bisnis/PANDUAN-MENTOR.md](../3-Desain-Aplikasi-dan-Bisnis/PANDUAN-MENTOR.md)**
