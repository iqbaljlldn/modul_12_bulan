# Panduan Mentor — Minggu 4: Pitching, Git Artefak, & Showcase Akhir Bulan

**Fokus Minggu Ini:** Menyatukan seluruh karya artefak Bulan 1 ke dalam satu narasi produk yang kuat, memvalidasi user flow alur WhatsApp dengan AI, mengelola version control artefak dengan alur branch dan PR di Git, melakukan gladi resik presentasi (7 menit), dan menggelar acara puncak: **Showcase Pitch Day Bulan 1**.

**Ritme:** 5 Sesi Materi & Workshop (Senin–Jumat) + 1 Sesi Showcase Akbar (Sabtu). Alokasi per sesi: ±90-120 menit; hasil workshop squad & catatan latihan mandiri di-*push* ke repositori squad dan dipresentasikan saat *Daily Standup* keesokan paginya. **Hari Sabtu (`04f`) bebas PR setelah kelas selesai.**

---

## 1. Peta Sesi Minggu 4

| Sesi | Hari | File Modul | Poin Mini-Lesson Mentor (20-30 Menit) | Output Sesi / Workshop Tim |
|---|---|---|---|---|
| 1 | Senin | `04a-pitching-dasar.md` | Struktur narasi pitch: Problem → Solusi → Bukti/Demo → Dampak → Roadmap; Formula Persona Hook (tanpa jargon teknis); Mengatasi demam panggung. | **Naskah Hook Pembuka 30 Detik Squad (`hook-pembuka-squad.md`)** |
| 2 | Selasa | `04b-ai-untuk-merancang-alur-aplikasi.md` | User Flow perjalanan pengguna vs Flowchart sistem; Scope Alur B (tanpa login); Audit titik buntu via AI + kendali batas scope MVP. | **User Flow Pemesanan WA Tervalidasi (`user-flow-tervalidasi.md`)** |
| 3 | Rabu | `04c-menyusun-pitch-deck.md` | Format baku 7 slide visual berbasis bukti; Kutipan wajib dari `catatan-wawancara-squad.md`; Ekspor wireframe Figma; Menghindari slide penuh teks. | **Draf Pitch Deck 7 Slide Tim** |
| 4 | Kamis | `04d-gladi-resik-dan-peer-feedback.md` | Simulasi panggung tepat 7 menit; Pembagian giliran bicara & *stage rescue*; Kerangka umpan balik *I Like, I Wish, What If*. | **Catatan Gladi Resik Squad (`catatan-gladi-resik.md`)** |
| 5 | Jumat | `04e-git-untuk-mengelola-artefak.md` | Alur kerja Git tim (branch per folder/tugas, commit pesan jelas, & Pull Request); Urutan update `README.md` terakhir; Merapikan repositori tim. | **Repositori GitHub Squad Rapi & Terorganisir** |
| 6 | Sabtu | `04f-showcase-pitch-day.md` | Acara Puncak Showcase Pitch Day Bulan 1: Presentasi 7 menit per squad (+3-5m Q&A); Evaluasi 8 Checkpoint Kapabilitas; Refleksi Akbar di kelas. | **Checklist Kapabilitas 8 Checkpoint & Refleksi Akbar** |

---

## 2. Beban Tugas Mandiri Minggu 4 (Individual)

Setiap murid mengerjakan catatan latihan mandiri pada hari Senin–Jumat dan menyimpannya di folder pribadi masing-masing dalam repo squad (`tugas-mandiri/[nama]/tugas_<kode-sesi>.md`). **Tugas mandiri bersifat catatan pribadi murid (bukan artefak utama tim), dan hari Sabtu (`04f`) bebas tugas mandiri.** Total estimasi waktu Senin–Jumat: **110 menit (±1,8 jam)**.

| Sesi | Kode File | Nama Tugas Mandiri | Estimasi Waktu |
|---|---|---|---|
| 04a | `tugas_04a.md` | Naskah Pembuka (*The Hook*) 30 Detik + Latihan Stopwatch | 20 menit |
| 04b | `tugas_04b.md` | Mengidentifikasi 1 Skenario Gagal pada Alur WhatsApp & Solusinya | 20 menit |
| 04c | `tugas_04c.md` | Audit Mandiri Slide Bagian Bicara Masing-Masing | 25 menit |
| 04d | `tugas_04d.md` | Catatan Evaluasi Diri Pasca-Gladi Resik (Waktu & Perbaikan) | 20 menit |
| 04e | `tugas_04e.md` | **Jembatan Kode 3:** Verifikasi Commit & Pull Request Kode Latihan di GitHub Tim | 25 menit |
| **Total** | | *(Hari Sabtu 04f bebas PR — refleksi dilakukan di kelas)* | **110 menit (1 jam 50 menit)** |

---

## 3. Poin Kunci yang Harus Ditekankan Mentor

1. **"Storytelling mengalahkan slide penuh teks":** Ajari peserta bahwa slide hanya latar belakang visual. Mereka yang harus berbicara dan menatap mata audiens, bukan membaca teks slide.
2. **"Artefak adalah bukti nyata (Proof of Work)":** Saat slide solusi ditampilkan, jangan hanya klaim kata-kata indah. Tampilkan ekspor wireframe Figma, diagram flowchart/user flow, dan cuplikan ERD yang sudah dirancang selama 3 minggu terakhir.
3. **"Fokus Git pada Kolaborasi (Branch & PR)":** Peserta sudah pernah belajar Git dasar di **2 bulan pre-program sebelumnya**. Jangan mengulang teori command line dari nol; fokuskan pada alur kerja tim (membuat branch terpisah, membagi folder agar tidak bentrok, Pull Request, review rekan setim, baru merge `README.md` di akhir).

---

## 4. Evaluasi Akhir: 8 Checkpoint Kapabilitas Pra-Coding (Sabtu)

Evaluasi Bulan 1 menggunakan **Checklist 8 Kapabilitas Inti** (status: **Siap**, **Hampir Siap**, atau **Perlu Pendampingan**). Tidak ada vonis "tidak lulus" atau pemotongan skor angka.

| # | Checkpoint Kapabilitas | Bukti Pengamatan Mentor | Status (Siap / Hampir Siap / Perlu Pendampingan) | Catatan Masukan |
|---|---|---|---|---|
| 1 | **Computational Thinking** | Mampu memecah masalah runtut tanpa ambigu (Dekomposisi, Pola, Abstraksi, Algoritma/Pseudocode). | | |
| 2 | **Flowchart Alur Baku** | Menggambar diagram alur dengan simbol standar, percabangan jelas, alur pemesanan WA lengkap. | | |
| 3 | **Model Data ERD Dasar** | Membedakan entitas, atribut PK, relasi 1:N, dan entitas penghubung `ItemPesanan`. | | |
| 4 | **Wireframe Mobile-First** | Menata denah antarmuka sederhana di Figma yang ramah bagi pengguna awam UMKM. | | |
| 5 | **Value Proposition & Riset** | Menjelaskan nilai solusi berbasis hasil wawancara UMKM nyata dan persona yang membumi. | | |
| 6 | **AI Literacy & Etika** | Menggunakan AI sebagai sparring partner terstruktur (R-C-I-C-O), memvalidasi fakta, dan patuh etika. | | |
| 7 | **Pitching & Komunikasi** | Menyampaikan narasi produk percaya diri (Problem → Solusi → Bukti → Dampak → Roadmap) tepat 7 menit. | | |
| 8 | **Version Control Git** | Mengelola artefak dan latihan kode ke repositori GitHub tim melalui alur branch dan Pull Request. | | |

---

## 5. Panduan Pendampingan Pra-Bulan 2

Bagi murid yang masih memiliki status *Perlu Pendampingan* pada 1–2 checkpoint di akhir Showcase:
1. **Clinic Day (Senin Pagi Sebelum Sesi React):** Mentor menggelar sesi klinik santai selama 45 menit untuk menuntaskan materi yang belum tuntas (misal: merapikan branch Git atau meninjau ulang alur logika if-else).
2. **Pairing Buddy di Bulan 2:** Pasangkan murid tersebut dengan rekan squad yang memiliki pemahaman logika lebih kuat agar saling mendukung saat mulai menulis komponen React.
3. **Tujuan Utama:** Seluruh 18 murid melangkah bersama ke Bulan 2 dengan rasa percaya diri dan tanpa ada yang tertinggal di belakang.
