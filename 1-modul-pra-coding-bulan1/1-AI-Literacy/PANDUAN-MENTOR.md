# Panduan Mentor — Minggu 1: AI Literacy

**Fokus Minggu Ini:** Membangun pemahaman mendasar tentang kapabilitas dan batasan Artificial Intelligence (Generative AI), etika penggunaan di lingkungan belajar, teknik prompting terstruktur menggunakan kerangka R-C-I-C-O, dan bagaimana memanfaatkan AI sebagai mitra sparring berpikir dan belajar mandiri tanpa kehilangan kemandirian bernalar.

**Ritme:** 5 Sesi Materi & Workshop (Senin–Jumat) + 1 Sesi Review Mingguan (Sabtu). Alokasi per sesi: ±90-120 menit.

---

## 1. Peta Sesi Minggu 1

| Sesi | Hari | File Modul | Poin Mini-Lesson Mentor (20-30 Menit) | Output Sesi / Workshop Tim |
|---|---|---|---|---|
| 1 | Senin | `01a-pengenalan-ai-dan-etika.md` | Non-teknis: cara kerja LLM memprediksi kata berikutnya, batas kapabilitas (halusinasi, bias), etika belajar & anti-plagiarisme. | **Piagam Etika AI Tribe** (kesepakatan bersama) |
| 2 | Selasa | `01b-ct-dan-problem-solving-dengan-ai.md` | Pengenalan ringan Computational Thinking; AI sebagai sparring partner berpikir, bukan pemikir utama. Pengingat: sentuhan kode mulai Minggu 2. | **Lembar Dekomposisi Awal** (komparasi AI vs manual) |
| 3 | Rabu | `01c-prompt-engineering-dasar.md` | Anatomi prompt profesional R-C-I-C-O: Role, Context (Latar Belakang), Instruction (Instruksi), Constraint (Batasan), Output (Format Hasil). Few-shot sederhana. | **Cheat Sheet Prompt Engineering** per squad |
| 4 | Kamis | `01d-ai-untuk-aktivitas-harian.md` | AI untuk aktivitas operasional UMKM: copywriting, deskripsi produk, SOP layanan. Data fiktif ditandai sebagai asumsi. Sosialisasi rencana riset UMKM nyata. | **Draf Solusi Operasional UMKM (Asumsi)** |
| 5 | Jumat | `01e-ai-untuk-belajar-mandiri.md` | AI sebagai tutor Socratic & Active Recall (bukan mesin pembuat kunci jawaban instan). | **Log Dialog Belajar Socratic** per individu |
| 6 | Sabtu | `01f-review-dan-evaluasi-minggu1.md` | Sprint Review 1: Presentasi tiap squad (5m pitch + 3m Q&A), tantangan prompt debugging live, dan retrospektif tim. | **Checklist Kapabilitas Minggu 1 & Refleksi** |

---

## 2. Beban Tugas Mandiri Minggu 1 (Individual)

Setiap murid mengerjakan tugas mandiri setelah kelas dan menyimpannya di repositori squad dengan nama `tugas_<kode-sesi>.md`. Total estimasi waktu di luar kelas: **135 menit (±2,25 jam)** sepanjang minggu (aman di bawah batas 2,5 jam).

| Sesi | Kode File | Nama Tugas Mandiri | Estimasi Waktu |
|---|---|---|---|
| 01a | `tugas_01a.md` | Analisis Dilema Etika AI Pribadi | 20 menit |
| 01b | `tugas_01b.md` | Dekomposisi 1 Aktivitas Sehari-hari + Uji Sparing AI | 20 menit |
| 01c | `tugas_01c.md` | Menyusun 1 Prompt Formula R-C-I-C-O untuk Toko Sekitar | 25 menit |
| 01d | `tugas_01d.md` | Membuat 1 Deskripsi Produk UMKM Sekitar dengan AI + Kurasi Manual | 25 menit |
| 01e | `tugas_01e.md` | Log Sesi Dialog Socratic Mandiri (3 Putaran Tanya Jawab) | 30 menit |
| 01f | `tugas_01f.md` | Refleksi Pribadi Sprint 1 (3-5 Kalimat) | 15 menit |
| **Total** | | | **135 menit (2 jam 15 menit)** |

---

## 3. Jebakan Mental Model Siswa Minggu Ini

1. **"AI selalu benar karena tahu segalanya":** Peserta pemula sering memperlakukan output LLM sebagai firman mutlak. Mentor harus mendemonstrasikan fenomena *hallucination* secara langsung di kelas (misal: minta AI mengarang biografi fiktif seorang tokoh lokal atau aturan diskon yang secara diam-diam merugikan toko).
2. **Copy-paste tanpa membaca ulang:** Siswa meng-copy jawaban AI lengkap dengan salam pembuka khas LLM (*"Tentu! Sebagai AI language model..."*). Tegur ini sejak dini sebagai pelanggaran etika dan standar profesionalisme.
3. **Prompt terlalu pendek dan ambigu:** Contoh: *"Bikinin rencana UMKM"*. Bimbing siswa untuk membedakan kedua 'C' dalam R-C-I-C-O: Context (latar belakang toko) dan Constraint (pantangan/batasan ketat).

---

## 4. Checklist Kapabilitas Sprint Review 1 (Sabtu)

Evaluasi dilakukan menggunakan checklist kapabilitas dengan 3 pilihan status: **Siap**, **Hampir Siap**, atau **Perlu Pendampingan**. Tidak ada angka nilai atau skor berbobot.

| # | Indikator Kapabilitas | Bukti Observasi | Status (Siap / Hampir Siap / Perlu Pendampingan) | Catatan Masukan Mentor |
|---|---|---|---|---|
| 1 | **Etika & Integritas AI** | Mampu menjelaskan kapan AI boleh dan dilarang dipakai, serta bertanggung jawab penuh atas hasil karya tim. | | |
| 2 | **Prompting Terstruktur (R-C-I-C-O)** | Menyusun prompt lengkap dengan membedakan Context (latar belakang) dan Constraint (batasan ketat). | | |
| 3 | **Validasi & Deteksi Halusinasi** | Mampu menunjukkan bukti kurasi manual, menandai data asumsi, dan tidak menelan mentah-mentah saran AI. | | |
| 4 | **Dinamika Squad & Presentasi** | Ketiga anggota squad berbicara dalam batas waktu presentasi 5 menit (+3 menit Q&A), saling melengkapi saat ditanya. | | |
| 5 | **Kelengkapan Tugas Mandiri** | Mengumpulkan draf tugas individual `tugas_01a.md` sampai `tugas_01f.md` tepat waktu. | | |

---

## 5. Panduan Mentor untuk Siswa "Perlu Pendampingan"

Jika seorang siswa mendapat status *Perlu Pendampingan* pada Sprint Review 1:
1. **Sesi Pairing 1-on-1 (15 Menit):** Dampingi siswa membuka aplikasi AI. Minta siswa mengetik satu prompt buruk, lalu bimbing langkah demi langkah memperbaikinya memakai kerangka R-C-I-C-O.
2. **Latihan Remedial Ringan:** Berikan satu teks deskripsi produk yang mengandung fakta mengada-ada (*hallucination*). Minta murid menandai kalimat mana yang tidak masuk akal.
3. **Target:** Memastikan murid paham bahwa AI adalah mitra diskusi yang harus selalu dikoreksi oleh akal sehat manusia, sebelum masuk ke perancangan logika di Minggu 2.
