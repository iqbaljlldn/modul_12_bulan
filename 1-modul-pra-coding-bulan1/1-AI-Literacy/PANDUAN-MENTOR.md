# Panduan Mentor — Minggu 1: AI Literacy

**Fokus Minggu Ini:** Membangun pemahaman mendasar tentang kapabilitas dan batasan Artificial Intelligence (Generative AI), etika penggunaan di lingkungan belajar, teknik prompting terstruktur menggunakan kerangka R-C-I-C-O, dan bagaimana memanfaatkan AI sebagai mitra sparring berpikir dan belajar mandiri tanpa kehilangan kemandirian bernalar.

**Ritme:** 5 Sesi Materi & Workshop (`01a` s/d `01e`, Rabu–Senin). Karena kelas dimulai pada hari Rabu, sesi evaluasi khusus Minggu 1 (`01f`) ditiadakan dan digabung ke dalam **Sprint Review Sabtu Minggu 2 (`02f`)** agar siklus mingguan kembali terkunci di hari Sabtu. Alokasi per sesi: ±90-120 menit.

---

## 1. Peta Sesi Minggu 1

| Sesi | Hari | File Modul | Poin Mini-Lesson Mentor (20-30 Menit) | Output Sesi / Workshop Tim |
|---|---|---|---|---|
| 1 | Rabu | `01a-pengenalan-ai-dan-etika.md` | Non-teknis: cara kerja LLM memprediksi kata berikutnya, batas kapabilitas (halusinasi, bias), etika belajar & anti-plagiarisme. | **Piagam Etika AI Tribe** (kesepakatan bersama) |
| 2 | Kamis | `01b-problem-solving-dan-berpikir-terstruktur-dengan-ai.md` | Pengenalan ringan Computational Thinking; AI sebagai sparring partner berpikir, bukan pemikir utama. Pengingat: sentuhan kode mulai Minggu 2. | **Lembar Dekomposisi Awal** (komparasi AI vs manual) |
| 3 | Jumat | `01c-prompt-engineering-dasar.md` | Anatomi prompt profesional R-C-I-C-O: Role, Context (Latar Belakang), Instruction (Instruksi), Constraint (Batasan), Output (Format Hasil). Few-shot sederhana. | **Cheat Sheet Prompt Engineering** per squad |
| 4 | Sabtu | `01d-ai-untuk-aktivitas-harian.md` | AI untuk aktivitas operasional UMKM: copywriting, deskripsi produk, SOP layanan. Data fiktif ditandai sebagai asumsi. Sosialisasi rencana riset UMKM nyata. | **Draf Solusi Operasional UMKM (Asumsi)** |
| 5 | Senin | `01e-ai-untuk-belajar-mandiri.md` | AI sebagai tutor Socratic & Active Recall (bukan mesin pembuat kunci jawaban instan). | **Log Dialog Belajar Socratic** per individu |

---

## 2. Beban Tugas Mandiri Minggu 1 (Individual)

Setiap murid mengerjakan tugas mandiri setelah kelas dan menyimpannya di repositori squad dengan nama `tugas_<kode-sesi>.md`. Total estimasi waktu di luar kelas: **120 menit (2 jam)** sepanjang 5 sesi.

| Sesi | Kode File | Nama Tugas Mandiri | Estimasi Waktu |
|---|---|---|---|
| 01a | `tugas_01a.md` | Analisis Dilema Etika AI Pribadi | 20 menit |
| 01b | `tugas_01b.md` | Dekomposisi 1 Aktivitas Sehari-hari + Uji Sparing AI | 20 menit |
| 01c | `tugas_01c.md` | Menyusun 1 Prompt Formula R-C-I-C-O untuk Toko Sekitar | 25 menit |
| 01d | `tugas_01d.md` | Membuat 1 Deskripsi Produk UMKM Sekitar dengan AI + Kurasi Manual | 25 menit |
| 01e | `tugas_01e.md` | Log Sesi Dialog Socratic Mandiri (3 Putaran Tanya Jawab) | 30 menit |
| **Total** | | | **120 menit (2 jam)** |

---

## 3. Jebakan Mental Model Siswa Minggu Ini

1. **"AI selalu benar karena tahu segalanya":** Peserta pemula sering memperlakukan output LLM sebagai firman mutlak. Mentor harus mendemonstrasikan fenomena *hallucination* secara langsung di kelas (misal: minta AI mengarang biografi fiktif seorang tokoh lokal atau aturan diskon yang secara diam-diam merugikan toko).
2. **Copy-paste tanpa membaca ulang:** Siswa meng-copy jawaban AI lengkap dengan salam pembuka khas LLM (*"Tentu! Sebagai AI language model..."*). Tegur ini sejak dini sebagai pelanggaran etika dan standar profesionalisme.
3. **Prompt terlalu pendek dan ambigu:** Contoh: *"Bikinin rencana UMKM"*. Bimbing siswa untuk membedakan kedua 'C' dalam R-C-I-C-O: Context (latar belakang toko) dan Constraint (pantangan/batasan ketat).

---

## 4. Evaluasi Kapabilitas Minggu 1 (Asinkron & Terintegrasi ke `02f`)

Karena sesi Selasa langsung masuk ke Computational Thinking (`02a-02b`), pengecekan kapabilitas Minggu 1 dilakukan melalui **pemeriksaan asinkron artefak repo squad** oleh mentor dan dikonfirmasi saat **Sprint Review Gabungan di hari Sabtu (`02f`)** dengan 3 pilihan status: **Siap**, **Hampir Siap**, atau **Perlu Pendampingan**.

| # | Indikator Kapabilitas | Bukti Observasi | Status (Siap / Hampir Siap / Perlu Pendampingan) | Catatan Masukan Mentor |
|---|---|---|---|---|
| 1 | **Etika & Integritas AI** | Mampu menjelaskan kapan AI boleh dan dilarang dipakai, serta bertanggung jawab penuh atas hasil karya tim. | | |
| 2 | **Prompting Terstruktur (R-C-I-C-O)** | Menyusun prompt lengkap dengan membedakan Context (latar belakang) dan Constraint (batasan ketat). | | |
| 3 | **Validasi & Deteksi Halusinasi** | Mampu menunjukkan bukti kurasi manual, menandai data asumsi, dan tidak menelan mentah-mentah saran AI. | | |
| 4 | **Kelengkapan Tugas Mandiri** | Mengumpulkan draf tugas individual `tugas_01a.md` sampai `tugas_01e.md` tepat waktu. | | |

---

## 5. Panduan Mentor untuk Siswa "Perlu Pendampingan"

Jika seorang siswa mendapat status *Perlu Pendampingan* pada Sprint Review 1:
1. **Sesi Pairing 1-on-1 (15 Menit):** Dampingi siswa membuka aplikasi AI. Minta siswa mengetik satu prompt buruk, lalu bimbing langkah demi langkah memperbaikinya memakai kerangka R-C-I-C-O.
2. **Latihan Remedial Ringan:** Berikan satu teks deskripsi produk yang mengandung fakta mengada-ada (*hallucination*). Minta murid menandai kalimat mana yang tidak masuk akal.
3. **Target:** Memastikan murid paham bahwa AI adalah mitra diskusi yang harus selalu dikoreksi oleh akal sehat manusia, sebelum masuk ke perancangan logika di Minggu 2.
