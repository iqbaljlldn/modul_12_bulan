# Kurikulum Project-Based Learning 12 Bulan
### Platform Support UMKM — React, NestJS, PostgreSQL

**Versi 3.0** — upgrade dari v2.2. Perubahan utama: **Bulan 1 sepenuhnya pra-coding** (AI Literacy, Computational Thinking & Algoritma, Desain Aplikasi & Bisnis, Pitching) — materi coding (TypeScript + React) dimulai di Bulan 2. Materi coding lanjutan dan backend bergeser masing-masing 1 bulan. Phase 4 (Production Engineering) dikompres dari 3 bulan jadi 2 bulan supaya total tetap 12 bulan.

> **Product menjadi kendaraan belajar, bukan hadiah setelah peserta selesai belajar.**

---

## 1. Program Overview

| | |
|---|---|
| **Peserta** | 18 lulusan SMA/SMK, sudah belajar HTML, CSS, Git & JavaScript dasar selama 2 bulan (99% belum pernah ngoding sebelumnya) |
| **Durasi** | 12 bulan |
| **Tech stack** | React, TypeScript, NestJS, PostgreSQL, Git, Figma |
| **Tools kolaborasi** | simanajemen.my.id (board tugas, timeline, backlog) |
| **Model kerja** | Tribe-like (ala tim software development), diterapkan dari bulan 1 — bukan model kelas akademik |
| **Produk** | Satu Platform UMKM bersama (dibangun seluruh tribe) |
| **Ritme belajar** | 3-4 sesi/minggu (materi + praktik) + jam mandiri/pairing. Rasio **30% teori : 70% praktik** |
| **Materi yang sudah ada** | Pre-class 2 bulan (HTML, CSS, CLI/Git/GitHub, JavaScript) dan modul React bootcamp — dipakai sebagai referensi, tidak diulang (lihat Bulan 2-4) |

### Ringkasan 4 Fase

| Fase | Bulan | Fokus | Kondisi di akhir fase |
|---|---|---|---|
| **1. Pra-Coding & Team Foundations** | 1-3 | Bulan 1: bekal pra-coding (AI, CT & Algoritma, Design, Pitching). Bulan 2-3: **Mini Katalog UMKM** (React + TypeScript + API palsu `json-server`) dibangun slice demi slice; TypeScript, React, HTTP sisi client, Git workflow, pairing, code review dasar, debugging, task breakdown | Peserta punya fondasi berpikir komputasional, desain, dan komunikasi; lalu mulai mampu bekerja sebagai **anggota software team**; Katalog jalan di frontend dan kontrak API-nya tertulis |
| **2. Full-stack Foundations** | 4-5 | Bulan 4: API palsu diganti backend asli (NestJS, PostgreSQL) dengan slice & kontrak yang sama; Bulan 5: riset, desain, arsitektur, backlog, Sprint 0 | Bulan 4: Katalog full-stack end-to-end. Bulan 5: tribe siap bangun produk nyata & **sudah ada minimal satu vertical slice produk asli yang jalan** |
| **3. Product Development** | 6-10 | Sprint-based, feature per feature (Epic → Feature → Story → Vertical Slice) | MVP Platform UMKM (auth, produk, search/filter, checkout, dashboard) feature-complete |
| **4. Production Engineering** | 11-12 | Quality, production, release | Produk stabil, teruji, ter-deploy, terdokumentasi, didemokan ke publik |

> **Bulan = jendela indikatif, bukan deadline kaku.** Yang dijaga adalah *capability* dan *checkpoint* (lihat Bagian 15). Kalau progress peserta lebih lambat dari rencana, yang digeser/dipotong adalah **scope fitur**, bukan kualitas dan bukan pemahaman dasar.

---

## 2. Learner Profile

- 18 lulusan SMA/SMK, latar belakang beragam; sudah melewati pre-class 2 bulan (HTML 14 bab, CSS 21, CLI/Git/GitHub 10, JavaScript 21 bab termasuk async & Web API) plus modul React bootcamp, tapi hampir semuanya belum pernah ngoding proyek nyata.
- **Kemampuan awal tidak seragam.** Kurikulum ini tidak mengasumsikan semua peserta sama cepat. Konsekuensi desainnya:
  - Pairing & squad rolling di awal supaya peer-learning merata.
  - Tiap topik punya **jalur inti** (wajib semua) dan **jalur tambahan** (stretch untuk yang lebih cepat / dukungan ekstra untuk yang butuh).
  - Chapter dipakai buat memperdalam sesuai minat, bukan buat memisahkan "yang jago" dan "yang belum".
- Tiap topik baru butuh **porsi latihan lebih besar daripada teori**.
- Peserta belajar dari hampir nol, jadi program ini mengutamakan *rasa aman untuk salah, tanya, dan minta bantuan* — tanpa itu, pairing/review/demo gak akan jalan.

---

## 3. Learning Philosophy

### 3.1 Dari linear ke product-driven

Draft awal berbentuk linear:

```text
TypeScript → React → Backend → Database → Project → Deployment
```

Versi 3 memakai siklus, dengan **bulan pertama membangun fondasi berpikir sebelum ngoding**:

```text
Mindset & Skill Berpikir (Bulan 1)
  ↓
Product
  ↓
Capability yang dibutuhkan
  ↓
Concept
  ↓
Practice
  ↓
Feature / Vertical Slice
  ↓
Review
  ↓
Reflection
  ↓
Capability meningkat  ──► kembali ke Product
```

Peserta tetap belajar teknologi secara terstruktur, tapi tiap materi harus makin terhubung dengan kebutuhan membangun software. Pola yang dihindari: *"Bulan ini belajar teknologi X, lalu selesai."* Pola yang dipakai: *"Kita butuh capability X untuk menyelesaikan problem Y, jadi konsep X diajarkan dan langsung dipraktikkan."*

**Kenapa pra-coding dulu di Bulan 1?** Peserta belum pernah ngoding proyek nyata. Sebelum loncat ke kode, mereka butuh bekal berpikir: memecah masalah (computational thinking), merancang solusi (desain aplikasi & bisnis), menyampaikan ide (pitching), dan memakai AI sebagai teman belajar — bukan alat ajaib yang menggantikan pemahaman. Bekal ini membuat proses coding di Bulan 2 dan seterusnya jauh lebih bermakna: peserta tahu *kenapa* mereka ngoding, bukan cuma *bagaimana*.

### 3.1a Walking Skeleton — Ganti Mock Jadi Asli

Product-driven sejak hari pertama coding (Bulan 2) tidak berarti beginner langsung membangun full-stack. Caranya: bangun **slice tipis yang jalan dari awal**, dengan layer di bawahnya di-*mock*, lalu ganti mock dengan yang asli satu per satu.

```text
Bulan 2-3: React (asli) → json-server (mock)
Bulan 4  : React (asli) → NestJS (asli) → PostgreSQL (asli)   ← kontrak API tetap
```

Kenapa begini:
- Produk ada sejak minggu pertama coding, jadi tiap konsep punya alasan konkret.
- Beban kognitif dijaga: peserta hanya perlu paham satu layer baru pada satu waktu.
- Kontrak API (tabel endpoint) muncul secara alami dan jadi spesifikasi backend.
- Saat mock diganti asli, peserta *melihat* apa yang dikerjakan tiap layer.

Syaratnya: starter repo yang siap dari hari pertama coding (Bulan 2), konsep minimum tiap slice yang dijaga mentor (tulang punggung), dan mini-lesson 20-30 menit sebelum slice, bukan kuliah panjang.

### 3.2 Learning Loop per Topik

Sebisa mungkin setiap materi baru mengikuti pola:

```text
Why → Concept → Practice → Product application → Review → Reflection
```

Contoh (validation di API):

| Langkah | Isi |
|---|---|
| **Why** | Kenapa API perlu validation? Apa yang terjadi kalau user kirim data ngawur? |
| **Concept** | DTO + validation di NestJS |
| **Practice** | Latihan kecil: bikin DTO untuk `CreateProductDto`, coba kirim data salah |
| **Product application** | Implement validation di Product API |
| **Review** | Code review PR-nya (validasi udah lengkap? pesan error jelas?) |
| **Reflection** | Bug apa yang bisa terjadi tanpa validation? Ada yang ketinggalan di PR kita? |

Pola ini dipakai secara konsisten kalau relevan; gak semua topik butuh keenam langkah (topik kecil boleh diringkas).

### 3.3 Vertical Slice — Konsep Inti

**Vertical slice** = satu fitur kecil yang diselesaikan **end-to-end**, dari UI sampai database dan balik lagi, sampai bisa didemokan.

```text
Feature
  ↓
UI (React)
  ↓
API (NestJS controller + DTO)
  ↓
Business logic (service)
  ↓
Database (PostgreSQL)
  ↓
Testing / manual verification
  ↓
Demo
```

**Bukan begini:**

```text
Minggu 1 = frontend
Minggu 2 = backend
Minggu 3 = database
```

**Tapi begini** (progression slice yang dipakai dari Bulan 4 dan seterusnya):

```text
Create Product → List Product → Edit Product → Delete Product → Product Image
```

Kenapa penting: peserta belajar **delivery** (menyelesaikan sesuatu yang benar-benar jalan), bukan cuma syntax atau framework. Slice juga membuat squad & chapter alami saling bergantung: frontend, backend, dan data ketemu di satu fitur.

**Slice Checklist** (dipakai sebagai patokan "slice ini beres"):

- [ ] User bisa melakukan aksinya lewat UI
- [ ] UI memanggil API yang sesuai API contract
- [ ] Data divalidasi di API dan tersimpan/terbaca dari database
- [ ] Kasus error utama ditangani (input salah, data tidak ada, gagal jaringan)
- [ ] Sudah dicoba manual (happy path + minimal satu kasus gagal) dan hasilnya dicatat di PR
- [ ] PR sudah direview & di-merge
- [ ] Bisa didemokan

### 3.4 Prinsip Isi: "Teach what the product and learner capability currently require"

Mulai sederhana, naikkan kompleksitas bertahap sesuai kebutuhan produk dan kesiapan peserta. **Tidak dimasukkan** (kecuali ada kebutuhan produk yang jelas & peserta sudah siap):

- microservices, Kubernetes, distributed systems kompleks
- banyak design pattern & enterprise architecture
- tool/teknologi tambahan hanya supaya terlihat "seperti perusahaan"
- ceremony tambahan yang gak punya tujuan belajar/delivery yang jelas

**Filter keputusan** untuk setiap materi, aktivitas, ceremony, atau tool:

> *"Apakah ini membantu peserta menjadi lebih mampu membangun, memahami, menguji, mengirimkan, atau bekerja sama dalam sebuah software product?"*

Kalau jawabannya gak jelas, gak usah dimasukkan.

---

## 4. Graduate Capabilities

Setelah menyelesaikan program, peserta diharapkan mampu (dengan pendampingan minimal untuk masalah yang sudah dikenal, dan tahu cara mencari bantuan untuk yang belum dikenal):

### Technical
- memahami dan memakai TypeScript
- membangun UI dengan React
- membangun REST API dengan NestJS
- menggunakan PostgreSQL (SQL dasar, relasi, integrasi lewat ORM)
- menghubungkan frontend, backend, dan database dalam satu fitur
- memahami testing dasar (manual, unit, integration, E2E sederhana)
- memahami deployment dan production basics

### Software Engineering
- memakai Git workflow (branch, commit, PR, merge, resolve conflict)
- melakukan dan menerima code review
- debugging secara sistematis
- membuat task breakdown
- bekerja dengan API contract
- memahami basic architecture
- menulis dokumentasi teknis

### Team
- bekerja dalam squad, melakukan pairing
- memberi dan menerima feedback
- melakukan demo dan retrospective
- menyelesaikan task secara mandiri
- meminta bantuan dengan konteks yang jelas
- berkolaborasi lintas squad

### Product
- memahami problem user
- membuat requirement sederhana
- memahami trade-off
- menghubungkan technical work dengan product outcome
- melakukan iterative delivery

### Computational Thinking, Desain Produk/Bisnis & Komunikasi
- memecah masalah lewat computational thinking (dekomposisi, pengenalan pola, abstraksi, algoritma) dan menuangkannya ke flowchart sebelum ngoding
- membaca dan menggambar ERD sederhana untuk merancang struktur data
- memahami prinsip dasar desain aplikasi (UX, wireframe) dan desain bisnis (value proposition, model bisnis ringan, sudut pandang pelanggan)
- mempresentasikan/pitching hasil kerja secara ringkas dan meyakinkan (ala demo day/hackathon)
- memakai AI sebagai asisten secara bertanggung jawab: paham etika dasarnya, bisa menyusun prompt yang jelas, dan memakainya untuk bantu berpikir, riset, aktivitas harian, proyek kreatif, serta merancang alur/struktur aplikasi dan ide bisnis ringan — bukan untuk mengerjakan semuanya secara buta tanpa dipahami

### Production
- memahami testing dan CI/CD
- melakukan deployment
- memahami logging/monitoring
- memahami basic operational responsibility

> **Batasan klaim:** program ini memberi fondasi yang kuat dan pengalaman membangun produk nyata dalam tim. Hasilnya **bukan** "professional software engineer penuh" — peserta yang mulai dari nol dalam 12 bulan realistisnya siap lanjut belajar, magang, atau posisi entry-level *dengan pendampingan*, lengkap dengan portofolio nyata.

---

## 5. Product Context

**Platform UMKM** — marketplace/etalase yang membantu UMKM berjualan online dan pembeli menemukan produk UMKM. Satu produk bersama, dibangun seluruh tribe.

| Aktor | Kebutuhan utama |
|---|---|
| **UMKM (merchant)** | Daftar, kelola produk, terima & kelola order, lihat performa jualan |
| **Buyer** | Cari & filter produk, keranjang, checkout sederhana |

**Roadmap fitur (indikatif, bukan kontrak per bulan):**

| Epic | Isi | Kira-kira |
|---|---|---|
| Autentikasi & dasar dashboard | Register/login UMKM & buyer, role, dashboard shell | Bulan 6 |
| Manajemen produk | CRUD produk, upload gambar, kategori | Bulan 7 |
| Pencarian & filter | Kategori, lokasi/wilayah, harga | Bulan 8 |
| Keranjang & checkout | Keranjang, checkout sederhana, riwayat order | Bulan 9 |
| Dashboard UMKM | Statistik jualan, manajemen stok | Bulan 10 |
| Opsional (kalau kapasitas & kualitas memungkinkan) | Rating/review, notifikasi, pencarian lebih pintar | Bulan 10 |

**Di luar scope** (kecuali tribe sepakat dan kapasitas ada): payment gateway sungguhan, aplikasi mobile native, pemisahan jadi layanan-layanan terpisah (microservices).

**Product Owner:** di awal dipegang mentor/guru atau squad riset; mulai Bulan 9-10 peran ini dirotasi ke peserta, mentor jadi advisor.

---

## 6. Tribe / Squad / Chapter Model

Diterapkan dari hari pertama, bukan cuma pas project besar.

| | Tribe | Squad | Chapter |
|---|---|---|---|
| **Isi** | Seluruh 18 peserta | Tim kecil 3 orang (6 squad) | Lintas squad, minat/keahlian sama |
| **Tujuan** | Satu produk bersama | Menyelesaikan slice/fitur end-to-end | Menaikkan capability teknis anggotanya |
| **Ritme** | Showcase tiap 2 minggu | Update harian/async, pairing, code review, sprint | 1 sesi/minggu, 30-60 menit |
| **Output** | Produk & keputusan tribe (standar, tools) | Fitur yang jalan, PR | Konvensi, catatan bersama, kemampuan anggota |

### Squad
- **Bulan 1-4 (fondasi):** rolling/gonta-ganti tiap 1-2 minggu supaya semua saling kenal & saling ajarin. Mulai Bulan 3, pairing juga mempertimbangkan siapa yang lebih kuat di area tertentu biar saling mengisi.
- **Mulai Bulan 5:** direstruktur jadi **6 squad cross-functional @ 3 orang**, lebih stabil (gak rolling lagi). Komposisi ideal: tiap squad punya kombinasi minat backend, frontend, dan design/QA. Tetap **semua ngoding lintas layer** — spesialisasi bukan silo, siapa pun bisa (dan perlu) menyelesaikan slice end-to-end.
- **Sekitar Bulan 8:** rotasi peran/chapter singkat dipertimbangkan (misal yang biasa di frontend mencoba QA sebentar) supaya gak cuma jago di satu bidang.

### Chapter
- Mulai kebentuk di **Bulan 4**, berdasarkan minat yang keliatan selama fondasi. Ada 4: **Backend, Frontend, Design, QA & DevOps.**
- Anggota punya satu chapter utama dan boleh ikut chapter kedua (terutama setelah rotasi Bulan 8).
- **Chapter = capability accelerator**, bukan kelas tambahan dan bukan rapat mingguan biasa. Materinya muncul berdasarkan kebutuhan sprint (detail di Bagian 11).

---

## 7. Operating Principles

1. **Product-first.** Produk (Mini Katalog UMKM) hidup sejak minggu pertama coding (Bulan 2), dan materi ditarik oleh slice yang membutuhkannya, bukan diajarkan per bulan teknologi. Konsep yang belum dibutuhkan slice tidak diajarkan.
2. **Pra-coding foundations.** Bulan 1 membangun fondasi berpikir (computational thinking, desain, pitching, AI literacy) yang membuat proses coding di bulan-bulan selanjutnya lebih bermakna.
3. **Vertical slice.** Fitur diselesaikan end-to-end, bukan per layer.
4. **Small batches.** Task kecil, PR kecil, slice kecil — supaya cepat direview dan cepat belajar dari feedback.
5. **Setiap sprint = delivery unit + learning unit.** Ada dimensi *Product*, *Engineering*, dan *Team* (Bagian 10).
6. **Ceremony seminimal mungkin, dengan tujuan jelas.** Satu ceremony = satu tujuan belajar/delivery. Kalau gak jelas, dihapus.
7. **Ownership di peserta.** Keputusan teknis skala squad diambil squad; standar tribe diputuskan bersama; mentor menjaga guardrail dan bertindak sebagai coach (Bagian 13).
8. **Minta bantuan dengan konteks.** Format singkat: *"Aku mau ngapain, sudah coba apa, error/hasilnya apa, dugaanku apa."* Stuck lebih dari ±20 menit → tanya pasangan → squad → chapter → mentor.
9. **Tidak ada ujian akademik dan tidak ada ranking.** Yang dilihat adalah bukti capability (Bagian 12).
10. **Timeline fleksibel, kualitas tidak.** Kalau telat, potong scope, bukan potong review/testing/pemahaman.
11. **Keputusan penting dicatat.** Decision log ringan (tanggal, keputusan, alasan) — misal pilihan Tailwind vs CSS module, TypeORM vs Prisma, konvensi penamaan.

---

## 8. Capability Matrix

Capability seperti Git, debugging, code review, teamwork, dan product thinking **tidak pernah "selesai dipelajari"** — levelnya naik sepanjang 12 bulan.

**Legenda level:**

| Level | Arti |
|---|---|
| **Intro** | Diperkenalkan, dilakukan dengan bimbingan |
| **Core** | Fokus belajar bulan itu: diajarkan terstruktur + dilatih intensif |
| **Applied** | Dipakai membangun produk; belajar terjadi lewat pemakaian |
| **Developing** | Diperdalam sambil dipakai, menuju level lebih mandiri |
| **Continuous** | Dilatih terus di setiap sprint, gak ada titik "selesai" |

| Capability | M1 | M2 | M3 | M4 | M5 | M6-10 | M11-12 |
|---|---|---|---|---|---|---|---|
| Computational Thinking & Algoritma (flowchart) | Core | Applied | Applied | Applied | Applied | Applied | Applied |
| Desain Produk & Bisnis (UX ringan, value proposition) | Core | | Intro | | Core | Applied | |
| Pitching & komunikasi publik | Core | | | | Core | Continuous | Continuous |
| AI Literacy (etika, prompt engineering, AI sebagai asisten) | Core | Applied | Applied | Applied | Applied | Continuous | Continuous |
| Git & PR workflow | Intro | Core | Core | Core | Core | Continuous | Continuous |
| Debugging | | Core | Core | Core | Core | Continuous | Continuous |
| Code review | | Intro | Core | Core | Core | Continuous | Continuous |
| Pairing & teamwork | Core | Core | Core | Core | Core | Continuous | Continuous |
| Task breakdown & planning | Intro | Intro | Core | Core | Core | Continuous | Continuous |
| Komunikasi, demo & feedback | Intro | Core | Core | Core | Core | Continuous | Continuous |
| Ownership & delivery mandiri | | Intro | Intro | Core | Core | Continuous | Continuous |
| TypeScript | | Core | Core | Applied | Applied | Applied | Applied |
| React | | Core | Core | Applied | Applied | Applied | Applied |
| HTTP / REST API | | Intro | Core | Core | Core | Applied | Applied |
| Node.js & NestJS | | | | Core | Applied | Applied | Applied |
| PostgreSQL & data modeling | | | | Core | Core | Applied | Applied |
| Arsitektur & API contract | | | Intro | Intro | Core | Applied | Developing |
| ERD & data modeling (sebelum masuk DB asli) | Intro | | Intro | Applied | Core | Applied | Applied |
| Design & UX (Figma) | Intro | | | Intro | Core | Applied | Applied |
| Product thinking & requirement | Intro | Intro | Intro | Intro | Core | Continuous | Continuous |
| Testing & QA (manual → otomatis) | | | Intro | Intro | Intro | Developing | Core |
| Security awareness | | | | Intro | | Developing | Core |
| Deployment & CI/CD | | | | | Intro | Developing | Core |
| Logging, monitoring & operasi | | | | | | Intro | Core |
| Dokumentasi teknis | | Intro | Intro | Intro | Core | Applied | Core |

**Catatan:** Bulan 1 sepenuhnya pra-coding, sehingga React/TS/HTTP baru masuk di Bulan 2. CT, AI Literacy, dan Desain sudah Core di Bulan 1 karena itu fondasi berpikir yang dibangun sebelum ngoding. Class/OOP TypeScript sengaja baru ditarik di Bulan 4 saat NestJS membutuhkannya.

### Keterkaitan: Graduate Capability → Matrix → Bulan → Aktivitas → Bukti

Bagian ini memastikan tujuan akhir, capability matrix, isi bulanan, aktivitas squad/chapter, produk, dan bukti belajar **nyambung**, bukan berdiri sendiri.

| Graduate Capability | Baris matrix | Dilatih terutama di | Aktivitas squad / chapter | Bukti (Bagian 12) |
|---|---|---|---|---|
| CT, AI Literacy, Desain, Pitching | CT & Algo, AI Literacy, Desain Produk, Pitching | M1 (Core), dipakai terus | Workshop, output mingguan (flowchart, wireframe, pitch deck, ERD) | Output Bulan 1, kebiasaan di bulan-bulan selanjutnya |
| TypeScript, React | TypeScript, React | M2-3, dipakai terus | Slice Katalog + PR (Chapter Frontend mulai M4) | PR, showcase Katalog, penjelasan kode |
| REST API, NestJS, PostgreSQL, FE↔BE↔DB | HTTP/API, NestJS, PostgreSQL | HTTP sisi client M2-3; NestJS & PostgreSQL M4; dipakai M6-10 | Slice Katalog: json-server → NestJS → PostgreSQL; Chapter Backend | Katalog full-stack M4, trace request, PR slice |
| Testing dasar | Testing & QA | M11 (Intro sejak M3: test manual slice) | Test untuk slice sendiri, bug bash, Chapter QA & DevOps | Test di PR, bug report, partisipasi bug bash |
| Deployment & production basics | Deployment, Logging & operasi | M11-12 (Intro sejak M5, staging sejak M8) | Pipeline, deploy, game day, Chapter QA & DevOps | Deploy yang dilakukan sendiri, runbook, mini postmortem |
| Git workflow, code review, debugging | Git, Code review, Debugging | M2 dan seterusnya | PR kecil, review lintas squad, debug clinic | Riwayat PR & komentar review, kemampuan menjelaskan bug |
| Task breakdown, API contract, arsitektur, dokumentasi | Task breakdown, Arsitektur, Dokumentasi | M3-5, dipakai terus | Sprint planning, API contract, README/docs | Backlog buatan sendiri, dokumen teknis |
| Bekerja dalam squad, pairing, feedback, demo, retro | Teamwork, Komunikasi | M1 dan seterusnya | Pairing, sprint demo, retro, peer feedback | Peer feedback, catatan retro, demo |
| Memahami user, requirement, trade-off | Product thinking | M5 (Intro sejak M1) | Riset UMKM, persona, prioritisasi backlog | Problem statement, persona, keputusan scope |
| Ownership & mandiri | Ownership & delivery | M4 dan seterusnya | Slice dipegang sampai selesai | Slice yang selesai, kemampuan menjelaskan keputusan |

---

## 9. 12-Month Learning Roadmap

Format tiap bulan: **Tujuan → Fokus capability → Rencana mingguan → Aktivitas squad → Aktivitas chapter → Hasil produk → Bukti belajar → Checkpoint keluar.** Detail mingguan dari draft awal dipertahankan dan ditambah kolom *latihan & kaitan ke produk*.

---

# Phase 1 — Pra-Coding & Team Foundations (Bulan 1-3)

> **Tujuan fase:** Bulan 1 membangun fondasi berpikir dan soft-skill sebelum ngoding. Bulan 2-3 peserta mulai mampu bekerja sebagai anggota software team, dan **produknya sudah hidup sejak minggu pertama coding**. Bukan "bulan TypeScript, lalu bulan React", tapi satu produk kecil (Mini Katalog UMKM) yang tumbuh slice demi slice, dan teknologi ditarik saat slice membutuhkannya.

---

## Bulan 1 — Fondasi Pra-Coding: AI, Computational Thinking, Desain, & Pitching

**Tujuan:** Sebelum menulis satu baris kode pun, peserta punya bekal berpikir komputasional, kemampuan merancang solusi (desain aplikasi & bisnis), kemampuan menyampaikan ide (pitching), dan keterampilan memakai AI sebagai asisten belajar. Semua output Bulan 1 bersifat **project-based** — tiap minggu ada artefak nyata yang dihasilkan.

**Fokus capability:** Computational Thinking & Algoritma (Core), AI Literacy (Core), Desain Produk & Bisnis (Core), Pitching (Core), pairing & teamwork (Core), ERD (Intro), Git (Intro — untuk kolaborasi dokumen/artefak), task breakdown (Intro), product thinking (Intro).

**Squad:** 6 squad rolling @3 orang, ganti tiap 1-2 minggu. Meskipun belum ngoding, peserta sudah bekerja dalam tim kecil sejak hari pertama — membiasakan kolaborasi, pembagian peran, dan komunikasi.

### Minggu 1 — AI Literacy: Pengenalan, Etika, dan AI sebagai Teman Belajar

Peserta pertama kali berkenalan dengan AI secara mendalam: apa itu AI, apa yang bisa dan tidak bisa dilakukan, etika penggunaan, dan cara memakai AI sebagai asisten — bukan pengganti pemahaman.

| Sesi | Topik | Materi Inti | Output / Praktik |
|---|---|---|---|
| 1 | **Pengenalan AI & Etika** | Apa itu AI (ringkas, non-teknis), jenis AI yang relevan (generative AI, chatbot), apa yang AI bisa dan tidak bisa, bias & halusinasi, etika: kapan boleh pakai AI dan kapan harus pakai otak sendiri, plagiarisme vs bantuan | Diskusi kelompok: kasus-kasus etis (boleh/tidak boleh pakai AI untuk X?). Output: **"Piagam Etika AI Tribe"** — kesepakatan bersama tentang cara pakai AI yang bertanggung jawab selama program. |
| 2 | **Computational Thinking & Problem Solving dengan AI** | Pengenalan 4 pilar CT: dekomposisi, pengenalan pola, abstraksi, algoritma. Cara AI bisa membantu proses CT (brainstorming, memvalidasi logika), tapi tetap peserta yang berpikir | Latihan: ambil masalah sehari-hari (misal "merencanakan perjalanan" atau "mengelola stok toko"), pecah pakai 4 pilar CT. Coba minta bantuan AI untuk satu langkah, bandingkan dengan hasil berpikir sendiri. Output: **dokumen dekomposisi masalah** (tulis tangan/digital). |
| 3 | **Prompt Engineering Dasar: Cara Mengobrol dengan AI** | Anatomi prompt yang baik (konteks, instruksi, format output), teknik: zero-shot vs few-shot, iterasi prompt, cara memvalidasi jawaban AI, prompt untuk debugging dan penjelasan konsep | Workshop: peserta mencoba berbagai prompt untuk masalah yang sama, bandingkan hasilnya. Latihan: ubah prompt buruk jadi prompt baik. Output: **"Cheat Sheet Prompt Engineering"** per squad. |
| 4 | **AI untuk Aktivitas Harian & Proyek Kreatif** | Contoh penggunaan: AI untuk riset, merangkum informasi, brainstorming ide, membuat rencana, membuat konten sederhana. Batasan: selalu verifikasi output AI, jangan copy-paste tanpa paham | Mini-project: tiap squad pilih satu "masalah UMKM kecil" (misal: bikin deskripsi produk, rencana pemasaran sederhana, jadwal harian toko) dan selesaikan **dengan bantuan AI** — tapi harus bisa menjelaskan setiap langkah. Output: **presentasi mini** (5 menit per squad) tentang bagaimana mereka memakai AI dan apa yang mereka pelajari. |

### Minggu 2 — Computational Thinking & Algoritma

Minggu ini mendalami cara berpikir komputasional dan menuangkannya ke bentuk visual (flowchart, pseudocode) — skill yang akan sangat berguna saat mulai ngoding di Bulan 2.

| Sesi | Topik | Materi Inti | Output / Praktik |
|---|---|---|---|
| 1 | **Dekomposisi & Pengenalan Pola** | Memecah masalah besar jadi bagian kecil, mengenali pola yang berulang. Contoh: proses belanja online (cari produk → pilih → keranjang → bayar → kirim) | Latihan: ambil 3 proses bisnis UMKM nyata (menerima order, mengelola stok, melayani pelanggan), dekomposisi langkah-langkahnya. Output: **peta dekomposisi** (bisa pakai sticky notes, papan tulis, atau digital). |
| 2 | **Abstraksi & Algoritma** | Menyederhanakan masalah (abstraksi), menulis langkah-langkah solusi secara runtut (algoritma). Pengenalan pseudocode sederhana | Latihan: dari hasil dekomposisi sesi 1, tulis algoritma (dalam bahasa Indonesia/pseudocode) untuk satu proses. Misal: "Algoritma Menerima Order". Perbandingan: solusi berbeda untuk masalah yang sama. |
| 3 | **Flowchart** | Simbol-simbol flowchart (start/end, proses, decision, input/output), cara membaca dan menggambar flowchart, tools (draw.io, Mermaid, atau kertas) | Workshop menggambar flowchart: setiap squad mengambil satu fitur dari "Platform UMKM impian" dan menggambar flowchart alurnya. Misal: flowchart "User mendaftar sebagai UMKM" atau "Buyer checkout". Output: **flowchart per squad** (minimal 2 per squad). |
| 4 | **ERD Dasar (Pengenalan)** | Apa itu ERD, entitas, atribut, relasi (1-1, 1-N, N-N). Kenapa penting sebelum bikin database. Contoh: ERD sederhana toko online | Latihan: gambar ERD sederhana untuk "Mini Katalog UMKM" (entitas: Produk, Kategori, penjual). Belum harus sempurna — ini pengenalan. Output: **ERD draft pertama** per squad (akan direfined di bulan-bulan berikutnya). |

### Minggu 3 — Desain Aplikasi & Desain Bisnis

Peserta belajar berpikir dari sudut pandang pengguna (UX) dan dari sudut pandang bisnis — dua perspektif yang bikin coding jadi bermakna.

| Sesi | Topik | Materi Inti | Output / Praktik |
|---|---|---|---|
| 1 | **Desain Aplikasi — Prinsip UX Dasar** | Apa itu UX vs UI, prinsip: kemudahan pakai, konsistensi, feedback ke user, hierarki visual. Contoh baik vs buruk dari aplikasi nyata | Analisis: tiap squad pilih 2 aplikasi/website yang mereka pakai sehari-hari, identifikasi 3 hal bagus dan 3 hal buruk dari sisi UX. Output: **"UX Review"** singkat per squad (presentasi ke tribe 5 menit). |
| 2 | **Wireframe & Merancang Tampilan** | Apa itu wireframe (bukan desain cantik, tapi struktur), low-fi vs hi-fi, tools (kertas, Figma dasar), cara berpikir "halaman per halaman" | Workshop wireframe: setiap squad menggambar wireframe **3 halaman utama** Platform UMKM (misal: halaman daftar produk, detail produk, form tambah produk). Pakai kertas dulu, lalu pindah ke Figma (opsional). Output: **wireframe 3 halaman** per squad. |
| 3 | **Desain Bisnis — Value Proposition & Model Bisnis Ringan** | Apa itu value proposition, canvas sederhana (siapa pelanggannya, masalahnya apa, solusinya apa, keunggulannya apa). Model bisnis ringan: bagaimana platform UMKM bisa berguna (bukan cari untung, tapi dampak) | Workshop: tiap squad mengisi **Value Proposition Canvas** untuk Platform UMKM dari sudut pandang UMKM dan Buyer. Diskusi: kenapa UMKM mau pakai platform ini? Kenapa buyer mau beli di sini? Output: **Value Proposition Canvas** per squad. |
| 4 | **Sudut Pandang Pelanggan UMKM + AI untuk Merancang Ide Bisnis** | Empati pelanggan: persona sederhana (siapa UMKM-nya, apa masalahnya sehari-hari). Memakai AI untuk brainstorming fitur dan validasi ide bisnis | Latihan: buat **persona UMKM sederhana** (nama fiktif, jenis usaha, masalah utama, harapan dari platform). Pakai AI untuk brainstorming 10 fitur yang bisa membantu persona ini, lalu pilih 3 yang paling penting. Output: **persona + daftar fitur prioritas** per squad. |

### Minggu 4 — Pitching & Showcase Bulan 1

Bulan 1 ditutup dengan pitching — peserta belajar menyampaikan hasil kerja secara ringkas dan meyakinkan.

| Sesi | Topik | Materi Inti | Output / Praktik |
|---|---|---|---|
| 1 | **Pitching Dasar — Struktur & Teknik** | Struktur pitch: Problem → Solusi → Demo/Bukti → Hasil/Dampak → Call to Action. Teknik: storytelling sederhana, bahasa yang jelas, durasi (5-7 menit), tips nervousness | Latihan: tiap peserta menyampaikan pitch 2 menit tentang "kenapa Platform UMKM ini penting" (impromptu, belum pakai slide). Feedback dari pasangan. |
| 2 | **AI untuk Merancang Alur & Struktur Aplikasi** | Memakai AI untuk membantu merancang: user flow (alur pengguna), sitemap aplikasi, struktur fitur. Validasi hasil AI dengan flowchart & ERD yang sudah dibuat | Workshop: tiap squad memakai AI untuk merancang **user flow** Platform UMKM (dari landing page sampai checkout), lalu **memvalidasi** dengan menggambar flowchart manual. Output: **user flow + flowchart tervalidasi** per squad. |
| 3 | **Persiapan Pitch Deck & Gladi Resik** | Menyusun pitch deck sederhana (5-7 slide): cover, masalah, solusi (wireframe), alur (flowchart), data model (ERD), value proposition, rencana (apa yang akan dibangun di Bulan 2-12) | Tiap squad menyusun **pitch deck** menggunakan semua artefak yang sudah dibuat: wireframe, flowchart, ERD, value proposition, persona. Gladi resik presentasi. |
| 4 | **Showcase Bulan 1 — Pitch Day** | — | Tiap squad mempresentasikan pitch 7-10 menit + tanya jawab ke seluruh tribe. Format ala **demo day hackathon**: problem → solusi → bukti (wireframe, flowchart, ERD) → rencana. Peer feedback: tiap squad memberi apresiasi + saran ke squad lain. Output: **pitch deck final** + **rekaman/catatan feedback**. |

### Aktivitas Bulan 1
- **Squad:** update singkat harian (standup 10-15 menit atau tulis di board), pairing dalam workshop, retro di akhir minggu 2 dan 4.
- **Chapter:** belum ada (spesialisasi belum terlihat). Semua aktivitas tribe-level.
- **Git (Intro):** peserta diperkenalkan Git untuk mengelola artefak (dokumen, flowchart, wireframe) — bukan untuk kode, tapi membiasakan workflow (commit, push, kolaborasi).
- **Showcase akhir bulan:** lihat Minggu 4 Sesi 4 (Pitch Day).
- **Hasil:** Piagam Etika AI, cheat sheet prompt engineering, flowchart, ERD draft, wireframe, value proposition canvas, persona UMKM, user flow, pitch deck.
- **Bukti belajar:** artefak mingguan, showcase pitch, kemampuan menjelaskan hasil berpikir (CT, desain, bisnis) secara lisan, peer feedback.

**Checkpoint keluar Bulan 1:** tiap peserta bisa (1) memecah masalah menjadi langkah-langkah runtut menggunakan 4 pilar computational thinking; (2) menggambar flowchart alur fitur sederhana; (3) menggambar ERD dasar (entitas, atribut, relasi); (4) menggambar wireframe halaman sederhana; (5) menjelaskan value proposition Platform UMKM dari sudut pandang UMKM dan buyer; (6) memakai AI sebagai asisten dengan prompt yang jelas dan tetap memvalidasi hasilnya; (7) melakukan pitching 5-7 menit dengan struktur Problem → Solusi → Demo → Hasil.

---

## Cara Kerja Bulan 2-4: Walking Skeleton, "Ganti Mock Jadi Asli"

Setelah fondasi berpikir di Bulan 1, peserta mulai coding. Mereka tidak dilempar langsung ke full-stack. Produk dibangun dengan **layer palsu di bawahnya yang diganti asli bertahap** (Bagian 3.1a).

```text
Bulan 2-3:  React + TS (asli)  →  json-server (API palsu)
Bulan 4  :  React + TS (asli)  →  NestJS (asli)  →  PostgreSQL (asli)
                                   ↑ memenuhi kontrak API yang sama dengan json-server
```

**Produk:** *Mini Katalog UMKM* (daftar produk, tambah, edit, hapus, kategori, cari/filter). Ini sekaligus prototipe untuk Platform UMKM di Bulan 5.

**Aturan main:**
- **Repo per orang** (fork dari starter repo mentor). Squad rolling = grup pairing & review, bukan pemilik kode. Dengan begitu semua peserta membangun full-stack sendiri dan tidak ada yang cuma "kebagian satu layer".
- **Starter repo dari mentor:** Vite + React + TypeScript, oxlint + Prettier, `db.seed.json` berisi seed produk UMKM (field `snake_case`), `json-server` (**versi di-pin** ke 0.17.4; sintaks query pagination/filter mengikuti README starter karena bisa beda antar versi), PR template, satu perintah `npm run dev` yang menjalankan web + API palsu.
- **Loop tiap slice:** Mini-lesson 20-30 menit (konsep yang dibutuhkan slice ini) → kerja slice + pairing → PR & review → demo kecil → refleksi 5 menit (*apa yang hampir bikin bug?*).
- **Mini-lesson bukan kuliah.** Isinya Why → Concept → contoh kecil, sisanya praktik. Konsep yang belum dibutuhkan slice **tidak** diajarkan.
- **Tulang punggung konsep (urutan minimum).** Tiap slice punya konsep minimum yang wajib dikuasai sebelum lanjut (tabel di bawah). Slice boleh ditambah/dikurangi, tapi urutan konsep ini dijaga mentor supaya beginner tidak loncat terlalu jauh.
- **Flowchart sebelum ngoding.** Kebiasaan dari Bulan 1 diterapkan: sebelum memulai slice, peserta menggambar flowchart alur logika slice tersebut. Ini bukan formalitas — ini cara berpikir yang sudah dilatih.

### Tangga Slice Bulan 2-4

| # | Slice | Bulan | Konsep minimum yang ditarik | Layer |
|---|---|---|---|---|
| 0 | Katalog tampil (data hardcode) | 2 | Tipe dasar, `interface`, union/literal, komponen, props, `map` + `key`, conditional rendering | React |
| 1 | Katalog dari API (List) | 2 | `useEffect`, fetch, HTTP GET, status code, `Promise<T>`, loading/error state, generic `fetchJson<T>` | React ↔ json-server |
| 2 | Tambah Produk (Create) | 2 | Form terkontrol, `useState`, HTTP POST, `Omit`/`Partial`, kirim & tampilkan hasil | React ↔ json-server |
| 3 | Edit & Hapus | 2 | PATCH/PUT/DELETE, custom error class, `try/catch` bertipe, memecah module | React ↔ json-server |
| 4 | Detail Produk & navigasi | 2 | React Router, route param, lifting state | React |
| 5 | Kategori | 3 | Data relasi di `db.json`, component composition, styling standar tribe, custom hook `useProducts` | React ↔ json-server |
| 6 | Form yang layak | 3 | Validasi form, pesan error, context dasar | React |
| 7 | Cari, filter, halaman | 3 | Query params, debounce, state di URL, pagination, loading/error yang rapi | React ↔ json-server |
| 8 | Katalog siap tampil + **kontrak API tertulis** | 3 | Responsif dasar, README, merapikan kode, menulis tabel endpoint | React |
| 9 | List & Create — **mock diganti NestJS** | 4 | Node dasar, NestJS (module/controller/service/DTO), class TS, validation | React ↔ NestJS |
| 10 | Edit & Hapus + error konsisten | 4 | Exception NestJS, format error API, CORS | React ↔ NestJS |
| 11 | Data pindah ke PostgreSQL | 4 | SQL dasar, tabel, ORM (TypeORM/Prisma), `.env`, seed & migrasi | React ↔ NestJS ↔ PostgreSQL |
| 12 | Kategori & filter lewat JOIN | 4 | Relasi 1-N, `JOIN`, filter/search/pagination di server | React ↔ NestJS ↔ PostgreSQL |

### Bahan Belajar yang Sudah Ada (bacaan wajib sebelum slice, bukan sekadar rujukan)

| Sumber | Sudah menutup | Dipakai untuk |
|---|---|---|
| **Pre-class** (HTML 14 bab, CSS 21, CLI/Git/GitHub 10, JavaScript 21 bab termasuk async & Web API) | HTML/CSS, CLI, Git dasar, JS termasuk fetch/async | Slice 0-8: dirujuk saat peserta butuh menyegarkan JS/Git/CSS; **tidak** diajarkan ulang |
| **Modul React** (5 bab, 25 sub-bab — lihat pemetaan di bawah) | React dari dasar sampai routing & pola lanjutan | Tiap slice punya **bacaan wajib** dari bab tertentu yang harus dibaca peserta *sebelum* mini-lesson. Mini-lesson menjembatani konsep ke kasus Katalog UMKM, bukan mengulang isi bab. |

### Pemetaan Spesifik: Slice → Sub-bab Modul React

Pemetaan ini berdasarkan isi konkret tiap sub-bab (`modul-react-programmer-pit`), bukan hanya nama folder.

| Slice | Bacaan wajib (modul React) | Konsep kunci dari bacaan | Catatan |
|---|---|---|---|
| **Pra-Slice 0** (orientasi) | **1.1** Pengenalan React & Setup Environment | SPA vs MPA, Virtual DOM, Vite vs CRA, folder structure, JSX dasar | Peserta membaca di hari pertama coding (Bulan 2) sebelum mulai; bagian CRA bisa di-skip (kita pakai Vite) |
| **Slice 0** | **1.2** JSX & Rendering Elements, **1.3** Components & Props, **1.4** Styling dalam React, **4.1** Pengenalan TypeScript pada React | JSX lengkap, conditional rendering, list rendering, functional component, props (destructuring, default, children), CSS classes/modules, TS pada React | 4.1 dari Bab 4 ditarik ke sini karena kita pakai TS dari awal |
| **Slice 1** | **1.5** State & useState, **2.3** Component Lifecycle & useEffect, **2.4** API Integration & Async Operations | State vs props, useState, re-rendering, lifecycle phases, useEffect, dependency array, cleanup, fetch API, loading/error state | Bab 2.3 dan 2.4 adalah bacaan paling krusial sebelum slice ini |
| **Slice 2** | **2.1** Event Handling & Forms | SyntheticEvent, controlled components, form handling, multiple inputs, validasi input sederhana | |
| **Slice 3** | **2.2** Conditional Rendering & Lists (pendalaman), **2.5** State Management Lanjutan | Teknik conditional rendering lebih lanjut, key dan optimasi, useReducer (pengenalan), lifting state | 2.5 optional — cukup bagian lifting state |
| **Slice 4** | **3.4** React Router Routing Dasar | BrowserRouter, Route, Link, useParams, useNavigate | |
| **Slice 5** (Bulan 3) | **1.4** Styling dalam React, **4.2** Advanced Styling, **3.2** Custom Hooks | Utility-first CSS (Tailwind v4), component composition (`Button`, `Input`), Rules of Hooks, ekstraksi custom hook (`useCategories`, `useProducts`) | Standar styling tribe diputuskan di awal; memisahkan business logic dari komponen UI |
| **Slice 6** (Bulan 3) | **2.1** Event Handling & Forms (form validation), **4.1** TypeScript pada React, **3.1** useContext & Context API | Validasi murni (`validate.ts`), tipe `FormErrors` opsional, aksesibilitas (`aria-invalid`), Prop Drilling, arsitektur Context 3-file (`Context`, `Provider`, `Hook`), floating toast UI | Mengganti validasi HTML `required` dengan validasi client-side yang terstruktur dan feedback toast |
| **Slice 7** (Bulan 3) | **2.3** useEffect & Lifecycle (cleanup), **3.3** Performance Optimization, **3.5** React Router Advanced (Search Params) | Debounce pattern 400ms (`useDebouncedValue`), URL sebagai Single Source of Truth (`useSearchParams`), server query (`_sort`, `_order`, `_page`, `_limit`), pagination header `X-Total-Count` | Bab terpadat di Bulan 3: filter, pencarian, dan pagination tersimpan di URL, tahan refresh & shareable |
| **Slice 8** (Bulan 3) | **4.2** Advanced Styling (Responsive Design), Dokumentasi Teknis API & Code Review | Mobile-First breakpoints (`sm:`, `md:`, `lg:`), touch target 44px, penulisan spesifikasi endpoint di `docs/kontrak-api.md`, perbedaan mock vs NestJS | Hasil akhir: Mini Katalog UMKM v2 siap pakai + kontrak tertulis resmi untuk Chapter Backend di Bulan 4 |

> **Aturan pakai:** Peserta membaca bab yang dipetakan **sebelum** sesi mini-lesson slice itu. Mini-lesson hanya menjembatani konsep ke kasus Katalog UMKM (20-30 menit), bukan menjelaskan ulang seluruh isi bab. Kalau ada peserta yang belum baca, mentor tetap jalan — bacaan menjadi tanggungan peserta, bukan alasan memperlambat tribe.

### Peta Materi v1 → v3 (tidak ada yang hilang)

| Materi di draft awal | Sekarang muncul di |
|---|---|
| Setup TS/`tsconfig`, basic types, `any`/`unknown` | Slice 0 (starter sudah ter-setup; mentor jelaskan `tsconfig` seperlunya) |
| Type inference, union & intersection, object typing, `interface` vs `type` | Slice 0 |
| Function typing, optional/default param, enum & literal types | Slice 0-2 (fungsi bantu; `ProductStatus` sebagai literal union; enum dibahas singkat) |
| Generics & constraint | Slice 1 (`fetchJson<T>`), diperdalam di Slice 3 |
| Utility types (`Partial`, `Pick`, `Omit`, `Record`), modules | Slice 2-3 (`Omit<Product, 'id'>`, `Partial<Product>`, pecah `api/` & `types/`) |
| Error handling (custom error, `try/catch`), async/await + `Promise<T>` | Slice 1 & 3 |
| Class, access modifier, inheritance, abstract class, `implements` | **Bulan 4 minggu 1** (Slice 9): service/controller NestJS memakai class; ditarik saat dibutuhkan |
| Console app "Inventaris UMKM" + squad showcase | Diganti showcase Mini Katalog (akhir Bulan 2 dan 3) |
| React: component/JSX/props, state, form, conditional & list rendering, `useEffect`/fetch, Router | Slice 0-4 |
| React lanjutan: styling, composition, custom hooks, state kompleks/context, form validation, konsumsi API asli, pagination, mini-app lebih lengkap | Slice 5-8 |
| **Pra-coding (baru di v3)**: AI Literacy, CT & Algoritma, Desain Aplikasi & Bisnis, Pitching | **Bulan 1** (full 4 minggu, project-based) |

Tiap slice di atas memakai Learning Loop (Bagian 3.2) dan Slice Checklist (Bagian 3.3), disesuaikan skalanya untuk pemula.

---

## Bulan 2 — Katalog Produk Hidup: TypeScript + React lewat Slice 0-4

**Tujuan:** JS sudah dikuasai lewat pre-class, jadi Bulan 2 langsung membangun. TypeScript dan React masuk lewat Katalog, bukan sebagai bulan materi terpisah. Bersamaan itu peserta membangun kebiasaan tim: Git workflow, pairing, review, debugging, memecah tugas. Bekal berpikir dari Bulan 1 (CT, flowchart, ERD, AI) langsung diterapkan: **sebelum mulai slice, peserta gambar flowchart dulu**.

**Fokus capability:** TypeScript (Core), React (Core), Git & PR workflow (Core), pairing (Core), debugging (Core), HTTP dari sisi client (Intro), code review (Intro), task breakdown (Intro).

**Squad:** 6 squad rolling @3 orang, ganti tiap 1-2 minggu; pairing driver/navigator bergantian. Repo tetap milik masing-masing orang.

Sejak hari pertama coding, praktik teknis memakai versi mini dari engineering workflow:

```text
Flowchart → Learn → Practice → Implement → Commit → Review → Revise → Merge → Showcase
```

Artinya: tiap slice = flowchart dulu → branch kecil + PR + minimal satu reviewer (pasangan/squad lain) sebelum di-merge. PR template 3 pertanyaan: *Apa yang dibuat? Cara mencobanya? Bagian mana yang masih bikin bingung?*

### Minggu 1 — Orientasi React + Slice 0

Peserta pertama kali pakai React dan TypeScript. Minggu ini membangun pondasi konsep sebelum langsung ke slice. **Bacaan wajib modul React:** 1.1, 1.2, 1.3, 1.4, dan 4.1.

| Sesi | Unit Belajar | Mini-lesson | Kerja & kaitan ke produk |
|---|---|---|---|
| 1 | **Orientasi React** (→ modul `01a`) | Apa itu React, SPA vs MPA, Virtual DOM (ringkas bab 1.1); tur folder starter, Vite `npm run dev` | Peserta menjalankan starter repo pertama kali, eksplorasi folder structure, pahami apa yang sudah disiapkan. |
| 2 | **JSX & Komponen Bertipe** (→ modul `01b`) | JSX lengkap, functional component, props, destructuring, children (bab 1.2-1.3); TypeScript di React: props bertipe, `interface`, `type` (bab 4.1) | Peserta menulis `ProductCard` dan `ProductList` pertama, menerapkan tipe `Product`. **PR pertama** (memakai Git dari pre-class). |
| 3 | **Styling Kartu Produk** (→ modul `01c`) | CSS classes, `className`, inline style, responsive dasar (bab 1.4) | Kartu produk punya styling yang layak. Review lintas pasangan pertama. |
| 4 | **Slice 0 — Katalog Tampil** (→ modul `01d`) | `map` + `key`, conditional rendering, empty state, union/literal type | Menampilkan `Product[]` hardcode sebagai kartu produk yang sudah ter-style. Merapikan, commit, PR. |

**Evaluasi mini akhir minggu 1:** latihan mandiri ~2 jam — modifikasi `ProductCard` (tambah field, ubah styling, coba conditional rendering baru).

### Minggu 2 — State, Fetch, & Form + Slice 1-2

Ini minggu terpadat: peserta belajar state, useEffect, fetch, dan form sekaligus. **Bacaan wajib modul React:** 1.5, 2.3, 2.4, 2.1.

| Sesi | Unit Belajar | Mini-lesson | Kerja & kaitan ke produk |
|---|---|---|---|
| 1 | **State & useState** (→ modul `02a`) | Konsep state vs props, `useState`, re-rendering (bab 1.5); latihan kecil: counter, toggle | Peserta paham kapan pakai state vs props. Latihan mandiri di starter. |
| 2 | **useEffect & Lifecycle** (→ modul `02b`) | Lifecycle phases, `useEffect`, dependency array, cleanup function (bab 2.3) | Peserta latihan: komponen yang log mount/unmount, timer sederhana. |
| 3 | **Slice 1 — Katalog dari API** (→ modul `02c`) | HTTP method/status code, DevTools Network, `fetch`, `Promise<T>`, generic `fetchJson<T>`, loading/error state (bab 2.4) | Katalog ambil data dari `json-server`. **Debug clinic** 20 menit: baca error TS, cek tab Network, isolasi bug. |
| 4 | **Event Handling & Form** (→ modul `02d`) | SyntheticEvent, controlled components, `onChange`, multiple inputs (bab 2.1) | Peserta latihan form kecil terpisah (input nama + preview). Task breakdown pertama di board. |
| 5 | **Slice 2 — Tambah Produk** (→ modul `02e`) | `Omit`/`Partial`, HTTP POST, form terkontrol lengkap | Form tambah produk lewat POST ke `json-server`. PR + review. |

### Minggu 3 — CRUD Lengkap + Slice 3

Fokus: menyelesaikan CRUD dan mulai menangani error dengan lebih rapi. **Bacaan wajib modul React:** 2.2, 2.5 (bagian lifting state).

| Sesi | Unit Belajar | Mini-lesson | Kerja & kaitan ke produk |
|---|---|---|---|
| 1 | **HTTP Methods & API Patterns** (→ modul `03a`) | PATCH vs PUT, DELETE, REST convention, status code 204, custom error class (pendalaman bab 2.4) | Peserta menulis `updateProduct` dan `deleteProduct` di `api/products.ts`. |
| 2-3 | **Slice 3 — Edit & Hapus** (→ modul `03b`, 2 sesi) | `ApiError` class, `Partial<T>`, state lokal `isEditing`, pola update/filter di state (bab 2.2 pendalaman) | Edit inline dan hapus produk dengan konfirmasi. Sesi 1: edit. Sesi 2: hapus + error handling. PR + review. |
| 4 | **State Management Patterns** (→ modul `03c`) | Lifting state, kapan state di parent vs child, pola `setItems(current => ...)` (ringkasan bab 2.5) | Peserta merapikan alur data di `ProductsPage` → `ProductList` → `ProductCard`. **Retro pertama** di akhir sesi. |

### Minggu 4 — Routing, Konsolidasi + Slice 4

Penutup Bulan 2. **Bacaan wajib modul React:** 3.4.

| Sesi | Unit Belajar | Mini-lesson | Kerja & kaitan ke produk |
|---|---|---|---|
| 1 | **React Router Dasar** (→ modul `04a`) | `BrowserRouter`, `Routes`, `Route`, `Link`, `useParams` (bab 3.4); SPA navigation vs full reload | Peserta latihan routing minimal di sandbox kecil sebelum implementasi di Katalog. |
| 2 | **Slice 4 — Detail & Navigasi** (→ modul `04b`) | Route param bertipe, fetch satu produk, dependency array `[id]` | Halaman detail produk. Tiga halaman Katalog: list, detail, tambah. PR + review. |
| 3 | **Konsolidasi & Refactor** (→ modul `04c`) | Code smell sederhana, rapikan import, hapus kode mati, tulis README | Peserta merapikan seluruh kode, tulis README singkat. |
| 4 | **Showcase** | — | Tiap peserta/pasangan mendemokan "Mini Katalog UMKM v1" ke tribe, saling kasih peer feedback (bukan dinilai per individu). Pakai teknik pitching dari Bulan 1. |

### Aktivitas Bulan 2
- **Penerapan bekal Bulan 1:** flowchart sebelum slice, AI sebagai asisten debugging/belajar (dengan etika yang sudah disepakati), ERD sebagai referensi struktur data.
- **Squad:** update singkat harian (standup 10-15 menit atau tulis di board), pairing, PR + review, retro di akhir minggu 2 dan 4.
- **Chapter:** belum ada (spesialisasi belum terlihat). Diganti *debug clinic* tribe-level kalau dibutuhkan.
- **Showcase akhir bulan:** lihat minggu 4 sesi 4.
- **Hasil:** Katalog Produk (list, tambah, edit, hapus, detail) dengan API palsu.
- **Bukti belajar:** riwayat PR & komentar review, showcase, kemampuan menjelaskan kode sendiri saat pairing, catatan retro, latihan evaluasi mini, flowchart per slice.

**Checkpoint keluar Bulan 2:** tiap peserta bisa (1) branch → commit → PR → revisi sesuai review → merge, tanpa dibantu; (2) memakai tipe dasar TS di kode sendiri (tanpa `any` sembarangan); (3) membuat komponen React dengan state, list, dan fetch dari API; (4) menjelaskan apa yang terjadi di tab Network saat Katalog dibuka; (5) menjelaskan konsep SPA, component, props, state, dan useEffect dengan kata-kata sendiri; (6) menggambar flowchart alur logika slice sebelum ngoding.

---

## Bulan 3 — Katalog Lengkap: React Lanjutan lewat Slice 5-8

**Tujuan:** Katalog makin nyata (kategori, form layak, cari/filter, halaman). Peserta makin lancar bikin UI interaktif dan makin paham kontrak antara frontend dan API. Bulan 3 ditutup dengan **kontrak API tertulis** yang menjadi spesifikasi backend Bulan 4.

**Fokus capability:** React (Core), HTTP/REST dari sisi client (Core), code review (Core), task breakdown (Core), komunikasi & demo (Core), arsitektur & API contract (Intro), testing manual (Intro).

Squad rolling masih jalan; mulai dipasangkan berdasarkan siapa yang lebih kuat di area tertentu biar saling isi.

### Minggu 1 — Kategori, Tailwind CSS & Custom Hook (Slice 5)

Keputusan standar styling tribe diambil sebelum minggu ini dimulai. **Bacaan wajib modul React:** 1.4, 4.2, 3.2.

| Sesi | Unit Belajar | Mini-lesson | Kerja & kaitan ke produk |
|---|---|---|---|
| 1 | **Styling Tailwind & Komponen UI** (→ modul `01a`) | Utility-first CSS, setup `@tailwindcss/vite`, component composition (`Button`, `Input`, `Badge`), HTMLAttributes, varian bertipe TS | Migrasi `index.css` ke Tailwind v4; bangun komponen atomik UI dengan varian. |
| 2 | **Konsep & Pola Custom Hook** (→ modul `01b`) | Mengapa custom hook? Rules of Hooks, pemisahan logika stateful vs UI, contoh `useCategories` | Buat `src/types/category.ts`, `src/api/categories.ts`, dan `useCategories.ts` (dengan cleanup flag `ignore`). |
| 3 | **Slice 5 — Kategori & useProducts** (→ modul `01c`) | Ekstraksi `useProducts` dari `ProductsPage`, dropdown kategori di form, badge nama kategori di kartu produk | `ProductsPage` menjadi sangat ringkas; relasi `category_id` aktif secara dinamis. PR + review. |
| 4 | **Pemantapan & Ketahanan API** (→ modul `01d`) | Graceful degradation (penanganan error terisolasi saat `/categories` gagal), pembuatan `Badge.tsx` | Uji ketahanan aplikasi jika API kategori down; latihan mandiri & peer review. |

### Minggu 2 — Validasi Form & Notifikasi Global Context (Slice 6)

Fokus ke UX pengisian data dan umpan balik sistem. **Bacaan wajib modul React:** 2.1, 4.1, 3.1.

| Sesi | Unit Belajar | Mini-lesson | Kerja & kaitan ke produk |
|---|---|---|---|
| 1 | **Validasi Form & Arsitektur Input** (→ modul `02a`) | Kelemahan HTML `required`, pemisahan validasi murni (`validate.ts`), tipe `FormErrors` opsional, aksesibilitas (`aria-invalid`) | Peserta menulis fungsi validasi murni yang menolak harga <= 0, stok negatif, dan nama kosong. |
| 2 | **Context API & Notifikasi Global** (→ modul `02b`) | Prop Drilling problem, arsitektur Context 3-file (`Context`, `Provider`, `Hook`), auto-dismiss `setTimeout`, mount di `main.tsx` | Membangun `ToastContext`, `ToastProvider`, dan `useToast` dengan container floating toast di bawah layar. |
| 3 | **Slice 6 — Validasi & Context** (→ modul `02c`) | Pencegahan submit (`early return`), integrasi `validate()` di `ProductForm` & `ProductEditForm`, pemicu toast create/edit/delete | Form memblokir input salah dengan pesan visual merah; toast muncul otomatis saat aksi sukses. PR + review. |
| 4 | **Pemantapan & Multi-variant Toast** (→ modul `02d`) | Toast tipe `success`, `error`, `info`, real-time error clearance saat user mengetik | Menambah warna toast; membersihkan error seketika saat user memperbaiki input. **Retro sprint 2**. |

### Minggu 3 — Cari, Filter, Urutkan, Pagination & URL State (Slice 7)

Bab terpadat di Bulan 3: optimasi performa dan skalabilitas data. **Bacaan wajib modul React:** 2.3, 3.3, 3.5.

| Sesi | Unit Belajar | Mini-lesson | Kerja & kaitan ke produk |
|---|---|---|---|
| 1 | **Debounce & Optimasi Input** (→ modul `03a`) | Bahaya live search tanpa debounce, race conditions, timer `setTimeout` + cleanup di `useEffect`, hook `useDebouncedValue` | Membedakan `urlFilters.q` (instan di input) vs `activeFilters.q` (debounced 400ms ke API). |
| 2 | **URL State & Server Query** (→ modul `03b`) | URL sebagai Single Source of Truth (`useSearchParams`), shareable link, tahan refresh, membaca header `X-Total-Count`, `fetchPage` | Memperbarui `http.ts` dan `products.ts` dengan query string `URLSearchParams`. |
| 3 | **Slice 7 — Cari, Filter, Pagination** (→ modul `03c`) | Filter bar terkontrol (`ProductFilters`), tombol navigasi halaman (`Pagination`), `reloadToken` pada mutasi data di `useProducts` | Menggabungkan search, dropdown kategori, sorting harga, pagination 6 produk/halaman di `ProductsPage`. PR + review. |
| 4 | **Pemantapan & Edge Cases** (→ modul `03d`) | Aturan reset `page: 1` saat ganti filter, empty state pencarian kosong, uji tombol browser Back/Forward | Menangani skenario pencarian tanpa hasil; tombol reset filter; deep linking test. |

### Minggu 4 — Desain Responsif, Kontrak API Tertulis & Showcase (Slice 8)

Penutup Bulan 3 dan jembatan ke Backend Bulan 4. **Bacaan wajib modul React:** 4.2 & Dokumentasi API.

| Sesi | Unit Belajar | Mini-lesson | Kerja & kaitan ke produk |
|---|---|---|---|
| 1 | **Desain Responsif & Layout Mobile** (→ modul `04a`) | Pendekatan Mobile-First di Tailwind (`sm:`, `md:`, `lg:`), kenyamanan sentuhan jari 44px, grid adaptif kartu produk | Menguji dan merapikan layout katalog di Chrome DevTools Device Mode (iPhone SE 375px, Pixel, iPad). |
| 2 | **Slice 8 — Kontrak API Tertulis** (→ modul `04b`) | Mengapa kontrak API krusial bagi backend? Audit endpoint di `src/api/`, menulis `docs/kontrak-api.md`, perbedaan mock vs NestJS | Mengisi tabel spesifikasi endpoint (method, path, body, response, error). Mencatat keputusan di `docs/decision-log.md`. |
| 3 | **Audit Kualitas Kode** (→ modul `04c`) | Menjalankan `npm run lint` (`oxlint`) & `npm run build`, membersihkan dead code, persiapan skrip demo showcase 5 menit | Squad membersihkan seluruh warning, gladi resik presentasi alur produk dan presentasi kontrak API. |
| 4 | **Showcase Mini Katalog UMKM v2** | — | Tiap squad mendemokan aplikasi v2 dan mempresentasikan dokumen Kontrak API ke Chapter Backend. Survei peminatan peran. |

### Aktivitas Bulan 3
- **Penerapan bekal Bulan 1:** flowchart sebelum slice, wireframe sebagai referensi desain UI, AI sebagai asisten.
- **Squad:** update harian, pairing berbasis kekuatan, **code review dengan checklist dasar** (nama jelas? tipe benar? ada bug yang kelihatan? bisa dijalankan?), retro tiap akhir minggu 2 dan 4.
- **Chapter:** belum resmi. Di akhir bulan dilakukan *survei minat singkat* (backend / frontend / design / QA & DevOps) sebagai bahan pembentukan chapter di Bulan 4.
- **Persiapan Bulan 4:** mentor + calon Chapter Backend memutuskan **ORM (TypeORM atau Prisma) — pilih satu**, dicatat di decision log.
- **Hasil:** Mini Katalog UMKM v2 + kontrak API tertulis.
- **Bukti belajar:** PR + review yang lebih substansial, showcase, kemampuan menjelaskan alur state/data dan isi kontrak API.
- **Capability snapshot** pertama (akhir Bulan 3, Bagian 12.2).

**Checkpoint keluar Bulan 3:** tiap peserta bisa (1) membangun antarmuka web modern dengan component composition atomik, Tailwind CSS v4, dan custom hooks; (2) menerapkan arsitektur validasi form murni serta sistem notifikasi global menggunakan Context API (arsitektur 3 file); (3) mengimplementasikan pencarian ber-debounce 400ms, filter kategori dinamis, pengurutan, dan paginasi yang tersinkronisasi penuh ke URL search params (tahan refresh & shareable); (4) menyusun dan menjelaskan dokumen spesifikasi teknis Kontrak API (`docs/kontrak-api.md`) sebagai acuan resmi Chapter Backend di Bulan 4; (5) menjalankan audit kualitas kode (`oxlint` dan `npm run build` lulus 0 error), memberikan code review yang konstruktif di PR, dan mendemokan produk secara percaya diri pada showcase akhir bulan.

---

# Phase 2 — Full-stack Foundations (Bulan 4-5)

> Frontend, backend, dan database **tidak diajarkan sebagai tiga dunia terpisah.** Bulan 4 mengganti API palsu Katalog dengan backend asli, slice demi slice. Bulan 5 bukan cuma dokumentasi: di akhirnya sudah ada slice produk asli yang jalan.

---

## Bulan 4 — Ganti Mock Jadi Asli: Node.js, NestJS, PostgreSQL

**Tujuan:** paham cara kerja REST API dari sisi server, membangun backend yang memenuhi **kontrak API Bulan 3**, menghubungkannya ke PostgreSQL, dan menjalankan Katalog yang sama secara **end-to-end**.

```text
Sebelum:  React → HTTP → json-server (db.json)
Sesudah:  React → HTTP → NestJS → PostgreSQL → NestJS → HTTP → React
```

Frontend hampir tidak berubah (cukup ganti base URL via variabel environment). Justru itu buktinya bahwa kontrak API bekerja, dan peserta merasakan apa yang sebenarnya dilakukan tiap layer.

**Fokus capability:** HTTP/REST server side (Core), Node.js & NestJS (Core), PostgreSQL (Core), validation & error handling, debugging lintas layer, ownership (Core), testing manual (Intro), TypeScript class/OOP dasar (Applied, ditarik saat NestJS membutuhkannya).

Mulai bulan ini **Chapter** kebentuk berdasarkan minat yang keliatan selama fondasi (survei akhir Bulan 3 + pengamatan mentor). Selain squad harian ada sesi Chapter mingguan (30-60 menit). Squad tetap rolling; repo tetap milik masing-masing orang (backend di folder/repo terpisah dari frontend Katalog).

**ERD dari Bulan 1 diterapkan:** ERD draft yang digambar peserta di Bulan 1 sekarang menjadi acuan schema database asli. Peserta melihat langsung hubungan antara "gambar di papan" dan "tabel di PostgreSQL".

| Minggu | Slice | Mini-lesson (dipicu slice) | Kerja & kaitan ke produk |
|---|---|---|---|
| 1 | **Slice 9 — List & Create, mock diganti NestJS** | Client-server dari sisi server, Node dasar, npm; NestJS (module, controller, service, DTO, DI — konsepnya saja); **class TS** (property, constructor, access modifier, `implements`; inheritance/abstract secukupnya); DTO + validation | `GET /products` dan `POST /products` mengikuti kontrak Bulan 3, data masih di memori. Frontend cukup ganti base URL. |
| 2 | **Slice 10 — Edit & Hapus + error konsisten** | Exception NestJS (`NotFoundException`, dll.), format error konsisten, CORS, uji endpoint dengan REST client | `PATCH` dan `DELETE`, pesan error dari API tampil rapi di UI. |
| 3 | **Slice 11 — Data pindah ke PostgreSQL** | SQL dasar (SELECT, INSERT, UPDATE, DELETE), tabel & tipe data, ORM (TypeORM **atau** Prisma, sesuai keputusan Bulan 3), `.env`, seed & migrasi. **ERD lanjutan (reinforcement dari Bulan 1):** ERD yang digambar sekarang langsung jadi schema database asli | Repository in-memory diganti PostgreSQL; seed dari `db.json`. Slice 9-10 kini "naik ke database" tanpa mengubah kontrak. |
| 4 | **Slice 12 — Kategori & filter lewat JOIN**, showcase | Relasi 1-N, `JOIN` sederhana, filter/search/pagination di server (menggantikan fitur `json-server`) | Hasil: **Mini Katalog UMKM Full-stack**. Showcase ke tribe. |

Tiap slice mengikuti Learning Loop (Bagian 3.2) dan Slice Checklist (Bagian 3.3): ada PR, review, dan demo kecil.

### Aktivitas Bulan 4
- **Squad:** update harian, pairing (rolling 1-2 minggu), PR + review, retro tiap akhir minggu 2 dan 4.
- **Chapter (sesi mingguan, topik dipicu kebutuhan slice):**
  - *Backend:* DTO & validation, cara membaca error di NestJS, struktur module/service, kesalahan umum dari PR.
  - *Frontend:* base URL & environment, penanganan error API di UI, merapikan API client.
  - *Design:* pengenalan wireframe & dasar Figma (persiapan Bulan 5).
  - *QA & DevOps:* REST client, menulis test case manual & bug report, `.env` & environment variable.
- **Hasil:** Mini Katalog UMKM Full-stack (React ↔ NestJS ↔ PostgreSQL) yang memenuhi kontrak API yang sama dengan versi mock.
- **Bukti belajar:** PR tiap slice, showcase, kemampuan **menelusuri satu request** dari klik tombol sampai baris di database dan kembali ke UI, kemampuan memutuskan bug ada di layer mana (UI / API / DB), kemampuan menjelaskan apa yang berubah dan apa yang tetap saat mock diganti asli.

**Checkpoint penting (akhir Bulan 4):** pastikan mayoritas peserta paham alur data frontend ↔ backend ↔ database sebelum lanjut ke project UMKM yang sesungguhnya. Indikator konkret: peserta bisa menjelaskan (di papan tulis/verbal) perjalanan request "Create Product" dan bisa menemukan layer yang bermasalah saat ada bug. Kalau ada yang keteteran, kasih sesi pairing/mentoring tambahan di awal Bulan 5 — **bukan remedial formal**, cukup pairing sama yang lebih kuat di chapter-nya.

---

## Bulan 5 — Kickoff Product: Riset, Desain, Arsitektur + Sprint 0 (First Vertical Slice)

**Tujuan:** menyiapkan fondasi produk nyata *sambil* membangun sesuatu yang benar-benar jalan. Bulan ini **bukan** bulan dokumentasi saja. Mini Katalog UMKM dan kontrak API dari Bulan 2-4 dipakai sebagai referensi dan bahan mentah (misal untuk slice List Product di Sprint 0).

> **Target akhir Bulan 5:** tribe siap membangun produk nyata dan sudah memiliki setidaknya satu vertical slice dari produk asli yang berjalan.

**Fokus capability:** product thinking & requirement (Core), design & UX (Core), arsitektur & API contract (Core), dokumentasi (Core), dan latihan bekerja dalam satu repo bersama; deployment (Intro).

**Squad** direstruktur jadi **6 squad cross-functional @ 3 orang** (kombinasi backend, frontend, design/QA), mulai lebih stabil. Chapter tetap jalan lintas squad: Backend, Frontend, Design, QA & DevOps.

**Penerapan bekal Bulan 1:** Desain Aplikasi & Desain Bisnis yang dikenalkan di Bulan 1 sekarang **diterapkan penuh** di Minggu 1-2 (riset & desain) — bukan materi baru, tinggal dipraktikkan skala produk asli. Wireframe, value proposition canvas, persona dari Bulan 1 jadi starting point. Pitching direinforce di Minggu 4 sebelum demo Sprint 0, dan jadi standar tiap showcase besar berikutnya (M10, M12).

| Minggu | Materi (dari draft awal) | Yang dijalankan paralel / tambahan |
|---|---|---|
| 1 | **Riset** — wawancara/survei ke UMKM asli, analisis kompetitor, susun problem statement & user persona (dikerjain lintas squad, digabung jadi satu requirement tribe). Persona UMKM dari Bulan 1 di-update dengan data riset asli. | Pembentukan squad baru. Mentor + Chapter Backend & QA/DevOps menyiapkan **starter repo** (struktur folder, database via container/lokal, template `.env`). |
| 2 | **Desain** — wireframe → hi-fi mockup (Figma), design system dasar (warna, komponen, tipografi). Wireframe dari Bulan 1 jadi starting point. | Anggota yang berminat backend/frontend menyisihkan ±30-40% waktu buat *technical spike* & setup di repo asli, supaya gak menunggu desain selesai. |
| 3 | **Arsitektur** — database schema (berdasarkan ERD yang sudah di-iterasi sejak Bulan 1), API contract, struktur folder & coding convention (biar konsisten antar squad). | Mulai **Sprint 0**: tiap squad ambil satu slice kecil di repo produk asli (lihat di bawah). |
| 4 | Setup tools di simanajemen.my.id (board tugas, timeline), breakdown backlog jadi sprint 2 mingguan (Epic → Feature → Story/Task), sprint planning pertama. | Sprint 0 selesai & **didemokan** (pakai teknik pitching dari Bulan 1); disambung sprint planning untuk Sprint 1 (Bulan 6). |

### Sprint 0 — Slice Pertama di Repo Produk Asli
Tujuannya bukan fitur besar, tapi membuktikan bahwa 6 squad bisa bekerja bareng di satu repo dengan standar yang sama. Contoh pembagian (satu slice per squad, semuanya memakai schema & API contract asli):

1. Health check endpoint + halaman status (bukti FE ↔ BE tersambung di repo asli)
2. List kategori produk (seed data → API → UI)
3. List wilayah/lokasi (seed data → API → UI)
4. Halaman "Daftar UMKM" read-only (sesuai hi-fi)
5. Halaman "Daftar Produk" read-only (**List Product** produk asli, sesuai hi-fi)
6. Halaman contoh komponen design system + layout bersama

### Output Bulan 5 (dipertahankan dari draft awal + ditambah)
- problem statement, user persona (update dari Bulan 1)
- UI/design (Figma) + design system dasar
- architecture (diagram sederhana)
- database schema (evolusi dari ERD Bulan 1)
- API contract (boleh Swagger/OpenAPI dari NestJS atau dokumen tabel endpoint — standar diputuskan tribe)
- coding conventions (Bagian 14)
- backlog (Epic → Feature → Story) di simanajemen.my.id
- **Definition of Done v1** (Bagian 10)
- sprint structure
- **Sprint 0: minimal satu vertical slice produk asli berjalan & ter-merge**

**Bukti belajar:** kontribusi ke problem statement/persona/desain, PR Sprint 0, kemampuan menjelaskan peran schema/API contract/konvensi, kemampuan memecah fitur dari backlog.

**Checkpoint keluar Bulan 5 ("Ready to Build"):** (1) requirement & desain cukup untuk Epic pertama; (2) schema & API contract Epic Auth tersedia; (3) konvensi & DoD v1 disepakati; (4) semua squad pernah merge PR ke repo produk asli; (5) backlog dan Sprint 1 terencana; (6) sisa peserta yang keteteran dari Bulan 4 sudah dapat pairing tambahan.

---

# Phase 3 — Product Development (Bulan 6-10)

Tiap squad kerja end-to-end di slice yang jadi tanggung jawabnya: pairing internal squad + review lintas squad. Pendekatan feature-based dari draft awal dipertahankan.

```text
Epic → Feature → User Story / Task → Sprint → Vertical Slice → Review
```

**Roadmap indikatif (dari draft awal):**

| Bulan | Target Fitur (Epic) |
|---|---|
| 6 | Autentikasi (register/login UMKM & buyer) + setup dasar dashboard UMKM |
| 7 | Manajemen produk (CRUD produk, upload gambar) |
| 8 | Pencarian & filter produk (kategori, lokasi/wilayah, harga) |
| 9 | Keranjang & checkout sederhana |
| 10 | Dashboard UMKM (statistik jualan, manajemen stok) |

Ini contoh roadmap, **bukan deadline absolut**. Kalau sebuah epic belum selesai, scope-nya dipotong per slice (mana yang *must*, mana yang *nice to have*) dan sisanya digeser — lihat aturan "kalau telat" di Bagian 10.

**Setiap sprint punya tiga dimensi:**

| Dimensi | Pertanyaan |
|---|---|
| **A. Product capability** | Apa yang sekarang bisa dilakukan user? |
| **B. Engineering capability** | Teknik/konsep engineering apa yang dipelajari? |
| **C. Team capability** | Praktik teamwork apa yang sedang dilatih? |

Dengan begitu setiap sprint adalah sekaligus **delivery unit + learning unit**.

**Ritme (dari draft awal, disederhanakan):** sprint planning di awal sprint → update harian/async tiap squad → sprint demo = **tribe showcase** tiap 2 minggu (progress ditunjukkan ke "product owner") → retro singkat di akhir sprint → sesi Chapter mingguan.

**Peran mentor:** lebih intens di Bulan 6-7 (banyak konsep baru diterapkan real), lalu makin dilepas di Bulan 8-10 supaya peserta makin mandiri.

---

## Bulan 6 — Autentikasi & Dasar Dashboard

**Epic:** Autentikasi & Dashboard shell. **Mode mentor:** intens.

| Sprint | A. Product | B. Engineering | C. Team |
|---|---|---|---|
| **6.1 Register & Login** | UMKM & buyer bisa register dan login | Password hashing, JWT, DTO validation, auth guard, environment config; form & API client di React (simpan token, kirim di header) | PR kecil dan disiplin, review lintas squad pertama di repo asli, pertama kali memakai DoD v1 dan menangani merge conflict nyata |
| **6.2 Role & Dashboard Shell** | User diarahkan sesuai role (buyer vs UMKM); dashboard UMKM punya layout dasar & profil UMKM | Role-based access (guard), protected route, komposisi layout, alur migrasi database | Ketergantungan antar squad (shell dipakai semua), protokol perubahan API contract |

**Chapter (topik muncul sesuai kebutuhan sprint):**
- *Backend:* kenapa password harus di-hash, JWT, guard → diskusi kesalahan umum dari PR.
- *Frontend:* auth state, protected route, penanganan token.
- *Design:* implementasi design system & handoff Figma → kode.
- *QA & DevOps:* test case manual auth (happy path + kasus gagal), template bug report, kebersihan secret & `.env` (security awareness Intro).

**Bukti belajar:** PR auth, demo, peserta bisa menjelaskan "kenapa password di-hash", bug report auth.

---

## Bulan 7 — Manajemen Produk

**Epic:** Manajemen produk (CRUD, gambar, kategori). **Mode mentor:** intens → mulai dikurangi.

| Sprint | A. Product | B. Engineering | C. Team |
|---|---|---|---|
| **7.1 Product CRUD** | UMKM bisa **membuat, melihat, mengedit, dan menghapus** produknya | REST API, DTO validation, PostgreSQL, relasi merchant → product, otorisasi (UMKM hanya bisa ubah produk sendiri), pagination server-side, form React | Task breakdown per slice, PR, code review, pairing driver/navigator, demo, retro |
| **7.2 Gambar & Kategori** | Produk punya gambar & kategori; halaman detail produk | File upload, validasi tipe/ukuran file, penyimpanan file (sederhana untuk MVP), tampilan gambar & optimasi ukuran dasar | Handling perubahan requirement di tengah sprint, sesi tanya-jawab dengan product owner |

**Contoh pembagian slice Sprint 7.1 antar 6 squad** (kalau slice lebih sedikit dari squad, pecah per aktor/halaman, hindari dua squad mengerjakan slice yang sama): A: Create Product · B: List Product (halaman UMKM) · C: Edit Product · D: Delete + konfirmasi UI · E: Kategori (master data) · F: Listing & detail produk untuk buyer. Ketergantungan ditangani lewat seed data + API contract dari Bulan 5.

**Contoh alur Chapter → Squad (capability accelerator):**

```text
Sprint: Product CRUD
   ↓
Backend Chapter: DTO + validation
   ↓
Squad: Implement
   ↓
Code Review
   ↓
Chapter: Diskusi common mistakes dari PR yang masuk
```

**Bukti belajar:** fitur CRUD yang jalan, PR + review, peserta bisa menjelaskan kenapa validation dan otorisasi diperlukan, demo ke product owner.

---

## Bulan 8 — Pencarian & Filter

**Epic:** Pencarian & filter produk. **Mode mentor:** mulai dilepas.

| Sprint | A. Product | B. Engineering | C. Team |
|---|---|---|---|
| **8.1 Search & Filter Dasar** | Buyer bisa cari produk berdasarkan nama serta filter kategori & harga | Query parameter, `WHERE`/`LIKE`/`ORDER BY`, DTO untuk query, pagination; React: state di URL, debounce input; **CI dasar** (lint + build di PR) | Perubahan API contract lintas squad, review lintas squad untuk modul bersama |
| **8.2 Filter Wilayah & Performa** | Filter lokasi/wilayah, sorting | Index database (pengenalan), `EXPLAIN` sederhana, seed data volume lebih besar; **deploy staging pertama** (dipandu mentor + Chapter QA & DevOps) | **Mid-project reflection** (retro lebih dalam soal fase ini); **rotasi peran/chapter singkat** (misal yang di frontend coba QA) |

**Chapter:** Backend (query, index), Frontend (state di URL, performa render dasar), QA & DevOps (CI dasar, staging), Design (usability check hasil filter).

**Bukti belajar:** demo search/filter, penjelasan kenapa query lambat setelah data banyak, refleksi hasil rotasi.

---

## Bulan 9 — Keranjang & Checkout Sederhana

**Epic:** Keranjang & checkout. **Mode mentor:** advisor; peran product owner mulai dirotasi ke peserta.

| Sprint | A. Product | B. Engineering | C. Team |
|---|---|---|---|
| **9.1 Keranjang** | Buyer bisa tambah/ubah/hapus item di keranjang | State keranjang (context/state di React + persist di backend), relasi user–cart–item, validasi stok | Integrasi lintas squad (cart bergantung ke produk & auth), integration testing manual bersama |
| **9.2 Checkout & Order** | Buyer bisa checkout; UMKM melihat order masuk & mengubah statusnya; riwayat order | Database **transaction**, model order & order item, simpan harga saat order (snapshot), aturan bisnis (stok gak boleh minus), format error API yang konsisten | Negosiasi scope ("checkout sederhana": tanpa payment gateway sungguhan), keputusan trade-off dicatat |

**Chapter:** Backend (transaction, aturan bisnis di service), Frontend (form checkout, state global sederhana), QA & DevOps (skenario uji checkout end-to-end manual), Design (alur checkout).

**Bukti belajar:** demo alur buyer → UMKM, penjelasan kenapa perlu transaction & snapshot harga.

---

## Bulan 10 — Dashboard UMKM & Konsolidasi

**Epic:** Dashboard UMKM (statistik & stok). **Mode mentor:** advisor; squad menjalankan planning sendiri.

| Sprint | A. Product | B. Engineering | C. Team |
|---|---|---|---|
| **10.1 Statistik Jualan** | UMKM melihat ringkasan jualan (total, per produk, per periode) | Query agregasi (`GROUP BY`, filter tanggal), grafik sederhana di React (satu library, dipilih tribe) | Squad memimpin sprint planning sendiri; product owner dirotasi ke peserta |
| **10.2 Manajemen Stok & Konsolidasi** | UMKM mengelola stok, ada indikator stok menipis | Update stok konsisten dengan order, rapikan tech debt, perbaiki hasil review yang tertunda | Feature-complete review: cek scope MVP vs yang selesai; putuskan go/no-go fitur opsional |

**Checkpoint keluar Bulan 10 ("Feature Complete"):** semua fitur *must* MVP jalan end-to-end di staging; daftar bug/tech debt terdata; keputusan fitur opsional (rating/review, notifikasi, pencarian lebih pintar) diambil: dikerjakan di Bulan 11 hanya kalau kapasitas & kualitas memungkinkan.

**Bukti belajar (Fase 3 keseluruhan):** riwayat PR & review selama 5 bulan, demo tiap sprint, kemampuan menjelaskan keputusan desain/arsitektur pada slice sendiri, peer feedback, catatan retro.

---

# Phase 4 — Production Engineering (Bulan 11-12)

Fase ini bukan sekadar "fitur tambahan + QA → deployment → demo", tapi transisi ke cara berpikir produksi:

```text
Build → Test → Deploy → Observe → Fix → Improve → Release → Demo
```

**Catatan v3:** Phase 4 dikompres dari 3 bulan (v2.2) menjadi 2 bulan. Bulan Quality dan Production digabung jadi satu bulan intensif (Bulan 11), dan Release & Demo tetap 1 bulan (Bulan 12). Ini membutuhkan disiplin scope yang ketat — fokus ke testing dan deployment untuk alur kritis, bukan menguji segalanya.

---

## Bulan 11 — Quality + Production (Gabungan)

**Tujuan:** produk bisa dipercaya DAN berjalan di lingkungan nyata. Peserta belajar menguji apa yang mereka bangun sekaligus bertanggung jawab atas operasinya. **Definition of Done v2** (slice baru punya test untuk logika pentingnya) dan **DoD v3** (siap deploy) berlaku bersamaan.

**Fokus capability:** testing & QA (Core), security awareness (Core), deployment & CI/CD (Core), logging/monitoring & operasi (Core), performance awareness, debugging & code review (Continuous).

| Minggu | Fokus | Aktivitas |
|---|---|---|
| 1 | **Unit & integration testing** | Konsep test (kenapa & apa yang diuji), unit test service NestJS dan komponen React yang penting. Tiap squad menulis test untuk slice yang mereka bangun sendiri (*test what you built*). Test API + database (integration), E2E dasar untuk 2-3 alur kritis (misal login, buat produk, checkout). **Feature freeze** di akhir minggu ini. |
| 2 | **QA workflow, bug bash & security** | Bug reporting yang baik, triase (severity vs prioritas), **bug bash** lintas squad, siklus fix → verifikasi. Security awareness (validasi input, injection, XSS, secret, otorisasi) dan performance awareness (query lambat, pagination, ukuran gambar) sebagai checklist review. Perbaiki temuan bug bash. |
| 3 | **CI/CD & Deployment** | Environments (local / staging / production), konfigurasi & secret per environment, container dasar, pipeline CI (lint, test, build) di setiap PR. Deploy otomatis ke staging, deploy ke production (server sederhana/PaaS — dipilih tribe & mentor sesuai biaya), domain/HTTPS dasar, kesadaran rollback. |
| 4 | **Observe, incident & dokumentasi** | Logging, monitoring (uptime/health check, error log), kesadaran backup (backup & **uji restore**). **Incident simulation ("game day"):** mentor sengaja mengganggu staging (env var salah, DB mati, deploy bermasalah), squad mendeteksi, mendiagnosis, memperbaiki, lalu menulis mini postmortem tanpa menyalahkan orang. Dokumentasi teknis (README, arsitektur, API docs, runbook cara deploy/rollback), user manual. |

- **Fitur opsional** (rating/review, notifikasi, pencarian lebih pintar): hanya jika backlog Bulan 6-10 selesai dan kualitas oke; dikerjakan sebagai slice kecil dengan test sejak awal dan tidak melewati feature freeze.
- **Tanggung jawab operasional ringan:** tiap minggu ada satu squad yang bertugas memantau health check & log, supaya peserta merasakan tanggung jawab operasional dasar.
- **Tidak dipakai:** Kubernetes, orkestrasi kompleks, microservices.
- **Chapter:** QA & DevOps memimpin (pola test, bug triage, CI/CD); Backend (logging, konfigurasi produksi, testing); Frontend (build produksi, performa muat, testing & E2E); Design (usability review, aksesibilitas dasar, materi user manual).
- **Persiapan Demo Day:** squad riset mulai menyiapkan rencana (siapa diundang, format acara).
- **Bukti belajar:** test di PR, kualitas bug report, kontribusi bug bash, PR perbaikan bug, deploy yang dilakukan sendiri, runbook, mini postmortem, dokumentasi.

**Checkpoint keluar Bulan 11 ("Production Ready"):** alur kritis punya test otomatis; tidak ada bug severity tinggi yang terbuka; hasil bug bash tertangani; produk live, health check & log berfungsi, backup pernah diuji restore, dokumentasi teknis & pengguna tersedia.

---

## Bulan 12 — Release & Demo

**Tujuan:** stabil, dirilis, dan diperlihatkan ke publik; peserta merefleksikan perjalanan dan menyusun langkah belajar berikutnya.

| Minggu | Fokus | Aktivitas |
|---|---|---|
| 1 | **Stabilization** | Perbaiki temuan user testing, jalankan ulang alur E2E, release checklist, code freeze. **User testing bareng UMKM asli** kalau memungkinkan. |
| 2 | **Final release** | Tag/versi rilis, catatan rilis (changelog), verifikasi production, user testing putaran kedua kalau memungkinkan. Laporan akhir tribe. |
| 3 | **Persiapan Demo Day** | Latihan presentasi (pakai teknik pitching dari Bulan 1), skenario demo, cadangan (misal rekaman video kalau jaringan bermasalah), materi tiap squad. |
| 4 | **Demo Day & refleksi** | Showcase final ke sekolah/orang tua/komunitas, idealnya undang UMKM asli buat coba produknya langsung. Refleksi tribe: apa yang dipelajari, tantangan terbesar sepanjang 12 bulan. Peer feedback terakhir — antar squad saling kasih apresiasi & masukan. |

- **Individual learning roadmap:** tiap peserta menyusun rencana belajar lanjutan berdasarkan *capability snapshot* terakhir (Bagian 12), plus **portofolio** (pilihan PR/slice yang bisa dijelaskan sendiri).
- **Bukti belajar:** rilis final, demo, refleksi, peer feedback, portofolio.

---

## 10. Sprint & Delivery Workflow

### 10.1 Hierarki Kerja

```text
Epic → Feature → User Story / Task → Sprint → Vertical Slice → Review
```

### 10.2 Siklus Sprint (2 minggu)

```text
Planning → 2 minggu kerja → Demo (Tribe Showcase) → Retro
```

- **Planning (±60-90 menit):** squad memilih slice dari backlog, memecah jadi task, mengisi **Sprint Canvas** (Product / Engineering / Team — lihat Lampiran B).
- **Demo = Tribe Showcase (45-60 menit):** tiap squad menunjukkan slice yang jalan ke tribe & product owner. Ini satu-satunya "showcase" tribe (tiap 2 minggu), bukan dua acara terpisah.
- **Retro (±30 menit):** apa yang lancar, apa yang perlu dibenerin, satu perubahan konkret untuk sprint berikutnya.
- **Fase 1 (Bulan 1-3):** Bulan 1 memakai *mini-cycle* 1 minggu (satu topik per minggu). Bulan 2-3 memakai *mini-cycle* 1-2 minggu (mengikuti rolling squad) dengan bentuk yang sama tapi lebih ringan.
- **Fase 2 (Bulan 4-5):** transisi ke sprint 2 minggu penuh.

### 10.3 Ceremony — Semua Punya Tujuan

| Ceremony | Frekuensi | Tujuan (kenapa ada) |
|---|---|---|
| Update harian / async | Harian, 10-15 menit atau tulis di board | Tahu siapa macet & butuh bantuan; latihan komunikasi singkat |
| Pairing | Terus-menerus | Transfer skill, kurangi stuck, belajar menjelaskan |
| Code review | Setiap PR | Kualitas kode + belajar dari kode orang lain |
| Sesi Chapter | 1x/minggu, 30-60 menit | Menaikkan capability spesifik yang dibutuhkan sprint |
| Sprint planning | Tiap awal sprint | Memilih slice & latihan memecah tugas |
| Tribe showcase (sprint demo) | Tiap 2 minggu | Bukti delivery, feedback dari product owner & peer |
| Retro | Akhir sprint | Belajar dari cara kerja sendiri |
| Peer feedback | Akhir fase / tiap ±2 sprint | Feedback antar sesama, bukan hanya dari mentor |

**Sengaja tidak ditambahkan:** refinement meeting terpisah, PI planning, scrum of scrums, dan ceremony lain yang tujuannya belum jelas untuk konteks 18 peserta pemula.

### 10.4 Git Workflow (versi sederhana)

- `main` selalu dalam kondisi jalan; kerja di feature branch.
- PR kecil (ideal bisa direview dalam ±15 menit), dengan deskripsi 3 pertanyaan (lihat Lampiran B).
- Minimal 1 reviewer; modul bersama & perubahan API contract direview lintas squad.
- Author yang melakukan merge setelah approval; konflik diselesaikan dulu di branch sendiri.
- Pesan commit jelas dan singkat (misal `feat: add create product endpoint`).

### 10.5 Definition of Ready & Definition of Done (progresif)

**Definition of Ready** (story siap dikerjakan): tujuan user jelas, acceptance criteria singkat, endpoint/UI terkait ada di API contract/desain, ukuran cukup kecil untuk 1 sprint.

**Definition of Done** berkembang seiring kemampuan:

| Versi | Mulai | Isi |
|---|---|---|
| **DoD v1** | Bulan 5 | Slice Checklist (Bagian 3.3): jalan end-to-end, validasi & error dasar, dicoba manual, PR direview & di-merge, bisa didemokan, API contract diperbarui bila berubah |
| **DoD v2** | Bulan 11 minggu 1 | v1 + test otomatis untuk logika penting + tidak ada temuan security/performance yang jelas dari checklist review |
| **DoD v3** | Bulan 11 minggu 3 | v2 + siap deploy (konfigurasi aman, log berguna, pipeline tetap hijau) |

### 10.6 Aturan "Kalau Telat"

1. Potong **scope** (per slice: must vs nice to have), jangan potong review, testing, atau pemahaman.
2. Fitur yang belum selesai digeser ke sprint berikutnya atau dikeluarkan dari MVP, keputusannya dicatat.
3. Kalau satu squad tertinggal, bantu lewat pairing/chapter — bukan dengan menambah beban ceremony.
4. Bulan 10 (konsolidasi) dan Bulan 12 minggu 1 berfungsi sebagai penyangga alami.

---

## 11. Chapter Learning Model

**Chapter = capability accelerator.** Tugasnya membantu peserta di squad berbeda menaikkan capability yang *dibutuhkan produk saat ini*, bukan mengajarkan semua materi sekaligus.

### 11.1 Siklus Chapter (Just-in-Time)

```text
Sprint planning: ketahuan capability yang dibutuhkan
   ↓
Chapter session: konsep + latihan singkat
   ↓
Squad: implement di slice
   ↓
Code review: kumpulkan pola kesalahan yang muncul
   ↓
Chapter session berikutnya: bahas common mistakes dari PR nyata
```

### 11.2 Format Sesi (30-60 menit, 1x/minggu)

- 10-15 menit konsep/demo singkat (Why → Concept)
- 20-30 menit latihan langsung atau studi kasus dari kode tribe (Practice)
- 10 menit bahas kesalahan umum dari PR nyata (Review)
- Ditutup satu tindakan konkret yang dibawa ke squad (Product application)

### 11.3 Peta Topik Chapter (dipicu kebutuhan, bukan urutan kaku)

| Chapter | Topik | Biasanya muncul ketika... |
|---|---|---|
| **Backend** | HTTP/API, NestJS, SQL, validation, error handling, arsitektur, testing, performance | Bulan 4: slice pertama; M6: auth; M7: CRUD; M8: query lambat; M9: transaction; M11: testing |
| **Frontend** | React, component design, state management, integrasi API, form, aksesibilitas, testing | Bulan 4: integrasi API; M6: auth state; M7: form/upload; M8: state di URL; M11: testing & E2E |
| **Design** | UX research, wireframe, UI, design system, usability | Bulan 4 (intro); M5: desain produk; M6-7: handoff; M11: usability review |
| **QA & DevOps** | Testing, bug reporting, CI/CD, deployment, monitoring, quality practices | Bulan 4: test manual; M8: CI & staging; M11: testing & production |

### 11.4 Prinsip
- Chapter **bukan silo**: fitur tetap dimiliki squad, bukan chapter.
- Anggota chapter yang lebih kuat bergantian memandu sesi (mengajar = cara belajar terbaik); mentor mendampingi.
- Hasil sesi ditulis singkat (cheat sheet/konvensi) dan disimpan di wiki tribe supaya berguna untuk semua.
- Chapter kecil (Design, QA & DevOps) boleh diperkuat anggota chapter kedua, terutama setelah rotasi Bulan 8.

---

## 12. Assessment & Evidence of Learning

Tetap **tidak ada ujian akademik tradisional** dan **tidak ada ranking antar peserta**. Pertanyaannya:

> *"Capability apa yang sudah dimiliki peserta, dan capability apa yang masih perlu dikembangkan?"*

bukan *"Siapa ranking 1?"*

### 12.1 Bukti Capability

| Bukti | Menunjukkan capability | Dikumpulkan |
|---|---|---|
| Output pra-coding (flowchart, ERD, wireframe, pitch deck) | CT, desain, komunikasi, AI literacy | Bulan 1 |
| Hasil fitur / slice | Delivery, ownership, kemampuan teknis end-to-end | Tiap sprint (Fase 3) |
| Pull request | Git workflow, kualitas kode, task breakdown | Terus-menerus (mulai Bulan 2) |
| Code review (yang diberikan & diterima) | Kemampuan membaca kode, feedback, keterbukaan belajar | Terus-menerus |
| Contribution history | Konsistensi kontribusi (dilihat bersama penjelasan, karena pairing membuat commit gak selalu mewakili individu) | Terus-menerus |
| Demo | Komunikasi, memahami produk | Tiap 2 minggu |
| Penjelasan teknis lisan | Pemahaman nyata di balik kode ("coba jelasin alur slice-mu") | Checkpoint |
| Kemampuan debugging | Berpikir sistematis, menelusuri layer | Checkpoint, sesi pairing |
| Penjelasan keputusan desain/arsitektur | Memahami trade-off | Sprint review, checkpoint |
| Peer feedback | Kolaborasi, ownership, sikap kerja tim | Akhir fase / ±2 sprint |
| Retrospective | Refleksi diri & tim | Tiap sprint |
| Bug report, test, dokumen teknis | Kualitas, produksi, dokumentasi | Fase 4 |

### 12.2 Capability Snapshot
Satu halaman per peserta yang menandai tiap baris Capability Matrix dengan skala: **Belum terlihat → Dengan bantuan → Mandiri → Bisa membimbing orang lain**, ditambah bukti dan langkah berikutnya. Diperbarui di **checkpoint: akhir Bulan 1, 3, 5, 10, dan 12** (ringan, 15-20 menit percakapan 1:1 dengan mentor; peserta menilai diri dulu). Snapshot dipakai untuk merencanakan bantuan dan menyusun *individual learning roadmap* di Bulan 12 — bukan untuk dipajang atau dibandingkan.

### 12.3 Format Peer Feedback
Sederhana dan spesifik: *satu hal yang bikin tim lebih kuat karena orang ini* + *satu hal yang bisa dicoba*. Berbasis kejadian nyata (PR, pairing, demo), bukan sifat pribadi.

---

## 13. Mentor / Facilitator Role

Mentor bukan pusat semua keputusan. Perannya bergeser dari pengajar → coach → advisor.

| Fase | Mode | Fokus mentor |
|---|---|---|
| 1 (M1-3) | Instruktur + coach | M1: memfasilitasi workshop pra-coding, membangun kebiasaan tim & rasa aman. M2-3: mengajar konsep inti coding, membangun kebiasaan (PR, review, retro), menciptakan rasa aman |
| 2 (M4-5) | Teacher-coach | Mengajar slice pertama backend, memandu riset/desain/arsitektur, menyiapkan starter repo |
| 3 (M6-10) | Coach → advisor (intens M6-7, dilepas M8-10) | Unblock, review arsitektur, menjaga guardrail, mendorong peserta memimpin planning |
| 4 (M11-12) | Advisor + quality gate | Menjaga standar kualitas, memandu game day, mendampingi rilis & demo |

**Tanggung jawab utama:** menyiapkan starter/skeleton & materi latihan; membaca progress lewat PR, board, dan retro; mengenali peserta yang diam atau tertinggal dan mendampingi lebih awal; menjaga ceremony tetap ringan; menjaga motivasi.

**Siapa memutuskan apa:**

| Level | Keputusan |
|---|---|
| **Squad** | Pembagian task, cara implementasi di dalam konvensi, siapa mengerjakan apa |
| **Tribe** (mentor memfasilitasi) | Standar & tools (styling, ORM, konvensi, format API contract), prioritas produk |
| **Mentor** (guardrail) | Keamanan, biaya infrastruktur, scope yang membahayakan timeline/kualitas, kondisi pembelajaran (apakah peserta terlalu tertekan) |

> Kalau mentornya hanya 1-2 orang untuk 18 peserta, prioritaskan: (1) pairing & Chapter lead dari peserta yang lebih kuat, (2) review PR yang bertujuan mengajar, (3) mengurangi ceremony dibanding menambahnya.

---

## 14. Collaboration & Tooling

### 14.1 Tools dan Kapan Masuk

| Tool | Fungsi | Masuk |
|---|---|---|
| Git + repo hosting | Versi kode, PR, review | Bulan 1 (untuk artefak), Bulan 2 (untuk kode) |
| simanajemen.my.id | Board tugas, timeline, backlog | Board sederhana Bulan 1; setup penuh Bulan 5 |
| Editor + linter/formatter | Konsistensi kode | Bulan 2-3 |
| AI tools (ChatGPT, dll.) | Asisten belajar & debugging | Bulan 1 (dengan etika & batasan yang jelas) |
| Node.js/npm, `json-server` (API palsu), DevTools Network, REST client | Menjalankan starter, API palsu, uji API | Bulan 2 (npm, json-server, DevTools), Bulan 3-4 (REST client) |
| PostgreSQL + ORM (TypeORM **atau** Prisma) | Database | Bulan 4 |
| Figma | Desain | Intro Bulan 1 (wireframe), penuh Bulan 5 |
| Swagger/OpenAPI (opsional) | API contract | Bulan 5-6 |
| CI (pada platform repo yang dipakai) | Lint/build/test di PR | Bulan 8 (dasar), Bulan 11 (penuh) |
| Framework test (unit, integration, E2E) | Testing | Bulan 11 |
| Container, hosting sederhana, monitoring uptime | Deployment & observasi | Staging Bulan 8, production Bulan 11 |

Tool baru hanya masuk kalau lolos filter Bagian 3.4.

### 14.2 Konvensi (usulan awal, difinalkan di Bulan 5 minggu 3)

- Variabel & fungsi di kode: **camelCase** (`productName`, `calculateTotalPrice`)
- Tipe/class/komponen React: **PascalCase** (`Product`, `ProductCard`)
- Tabel & kolom database: **snake_case** (`order_items`, `created_at`)
- Field data di API/JSON: **snake_case**, mengikuti nama kolom (`category_id`, `created_at`); variabel di kode tetap camelCase
- Branch: `feat/nama-fitur`, `fix/nama-bug`
- Keputusan penting: dicatat di decision log

### 14.3 Kebiasaan Kolaborasi
- Board simanajemen.my.id adalah sumber kebenaran status kerja; update singkat harian bisa async di sini.
- Tanya dengan format bantuan (Bagian 7).
- Dokumentasi ditulis sambil jalan (README per modul, API contract), bukan di akhir.

---

## 15. Teaching Notes, Risks & Checkpoints

### 15.1 Catatan Pengajaran
- **Bulan 1 pra-coding punya tujuan jelas:** membangun fondasi berpikir yang membuat proses coding di Bulan 2 dan seterusnya jauh lebih bermakna. Bukan bulan "teori kosong" — tiap minggu ada output nyata (flowchart, wireframe, ERD, pitch deck). Peserta yang sudah bisa berpikir secara terstruktur (CT) dan punya gambaran produk (desain & bisnis) akan lebih cepat menyerap materi coding.
- **Kecepatan kurikulum ambisius** (dari nol ke React + NestJS + PostgreSQL dalam 4 bulan, dengan 1 bulan pra-coding), tapi feasible kalau porsi latihan jauh lebih besar dari teori — usahakan **30% teori : 70% praktik** dari awal. Produk hidup sejak Bulan 2 minggu 1 dan tiap konsep ditarik slice, jadi teori selalu punya konteks. **Kuncinya adalah scaffolding:** starter repo siap sebelum Bulan 2, mini-lesson 20-30 menit (bukan kuliah), dan tulang punggung konsep yang dijaga mentor.
- **Pre-class dan modul React adalah referensi, bukan materi yang diulang.** Kalau ada peserta yang belum kuat di JS/Git/React dasar, arahkan ke bab yang relevan dan pairing, bukan mengulang kelas.
- **Rolling squad di Bulan 1-4 penting** untuk peer-learning yang merata; jangan biarkan komposisi squad sama terus dari awal.
- **Checkpoint akhir Bulan 4 penting** — jangan maksa lanjut ke project besar kalau fondasi belum solid; cukup tambah sesi pairing/chapter ekstra bagi yang butuh.
- **Phase 4 dikompres menjadi 2 bulan** — ini bisa ketat. Kuncinya: fokus ke testing alur kritis (bukan semua), dan deployment ke platform sederhana (PaaS). Jangan buang waktu di setup infrastructure yang kompleks.
- **Rotasi peran** di tengah project (mulai Bulan 8) supaya peserta gak cuma jago di satu bidang.
- Jaga proporsi: peserta harus lebih banyak ngoding (atau membuat artefak di Bulan 1) daripada ikut ceremony.

### 15.2 Risiko & Mitigasi

| Risiko | Tanda-tanda | Mitigasi |
|---|---|---|
| Bulan 1 pra-coding terasa "belum ngoding" dan peserta tidak sabar | Peserta bertanya "kapan mulai ngoding?", motivasi turun | Jelaskan sejak awal kenapa fondasi berpikir penting. Output tiap minggu harus terasa nyata dan berguna. Tekankan bahwa flowchart, ERD, wireframe akan langsung dipakai saat mulai coding. |
| Kesenjangan kemampuan antar peserta | Beberapa selalu menunggu/tertinggal, yang cepat bosan | Pairing berbasis kekuatan, jalur inti + tambahan, Chapter, pairing ekstra tanpa label remedial |
| Beban kognitif Bulan 2 (produk langsung, banyak hal baru sekaligus) | Peserta terlihat kewalahan, PR mandek di slice awal | Starter repo siap, slice kecil, mini-lesson singkat, pairing, jalur inti vs tambahan; potong slice, bukan potong pemahaman |
| Konsep dasar terlewat karena kejar slice | Kode jalan tapi peserta gak bisa menjelaskan (tipe TS asal `any`, fetch gak paham) | Tulang punggung konsep, checkpoint penjelasan lisan tiap akhir bulan, refleksi 5 menit per slice |
| Mock vs asli tidak identik | Frontend rusak saat ganti json-server ke NestJS, format error/pagination beda | Kontrak API tertulis di Bulan 3, cek bareng sebelum Slice 9; bedanya dicatat sebagai bahan diskusi |
| Bulan 4 terlalu padat | Banyak yang gak bisa menjelaskan alur request | Slice kecil, kontrak API yang sudah jelas, checkpoint akhir Bulan 4, pairing tambahan di awal Bulan 5 |
| Phase 4 terlalu ketat (2 bulan) | Testing atau deployment terburu-buru, kualitas turun | Fokus ke alur kritis saja (3-5 alur utama), pilih PaaS sederhana, manfaatkan buffer Bulan 12 minggu 1 |
| Mentor jadi bottleneck | Banyak PR/pertanyaan menunggu mentor | Review lintas squad, Chapter lead peserta, format bantuan dengan konteks, keputusan level squad/tribe |
| Ceremony memakan waktu ngoding | Peserta kelelahan rapat, sprint demo panjang | Tinjau tabel 10.3; hapus yang tujuannya gak jelas |
| Konflik di satu repo | Banyak merge conflict, `main` sering rusak | PR kecil, ownership modul jelas, CI dasar, protokol perubahan API contract, review lintas squad |
| Scope creep | Backlog membengkak, fitur opsional mengalahkan kualitas | Must vs nice to have, feature freeze Bulan 11 minggu 1 |
| Motivasi/kepercayaan diri turun | Peserta diam, jarang push, absen | Rasa aman untuk salah, retro jujur, mentor cek personal secara ringan |
| Kesenjangan produk vs pembelajaran | Squad "sibuk kejar fitur", gak paham konsep | Dimensi Engineering di tiap sprint, Chapter membahas kesalahan umum, penjelasan lisan sebagai bukti |
| Demo Day berisiko | Produk rusak pas demo | Rehearsal, environment demo stabil, cadangan rekaman |

### 15.3 Checkpoint Program

| Checkpoint | Waktu | Pertanyaan kunci | Kalau belum tercapai |
|---|---|---|---|
| Pra-Coding Foundations | Akhir Bulan 1 | Bisa memecah masalah pakai CT, gambar flowchart/ERD/wireframe, pitch hasil kerja, pakai AI dengan etika? | Perpanjang latihan CT/desain di awal Bulan 2; integrasikan ke slice coding |
| Team Foundations | Akhir Bulan 3 | Bisa PR-review-merge, membangun Katalog multi-halaman yang ambil data dari API (json-server), memecah tugas, dan membaca/menulis kontrak endpoint? | Perpanjang pairing/latihan sebelum masuk backend; potong slice Bulan 3, bukan lompat ke NestJS |
| Full-stack | Akhir Bulan 4 | Bisa menjelaskan & men-debug alur FE ↔ BE ↔ DB? | Pairing/chapter tambahan di awal Bulan 5 |
| Ready to Build | Akhir Bulan 5 | Ada requirement, desain, schema, API contract, konvensi, backlog, dan ≥1 slice produk asli berjalan? | Tambah waktu Sprint 0 sebelum Sprint 1 |
| Feature Complete | Akhir Bulan 10 | Fitur *must* MVP jalan end-to-end di staging? | Potong scope, geser ke konsolidasi & awal Bulan 11 |
| Production Ready | Akhir Bulan 11 | Alur kritis teruji, bug besar tertangani, live, terpantau, ada backup teruji, dokumentasi tersedia? | Fokuskan Bulan 12 minggu 1-2 ke stabilisasi |
| Release & Demo | Bulan 12 | Rilis final, demo, refleksi & roadmap individu selesai? | — |

### 15.4 Definisi "Berhasil"
Bukan "semua peserta jadi expert", tapi: peserta bisa membangun, memahami, menguji, mengirimkan, dan bekerja sama dalam sebuah software product nyata — dan tahu langkah belajar berikutnya.

---

## Lampiran A — Ringkasan Perubahan dari Versi Sebelumnya

### v1 → v2

| Bagian | Versi 1 | Versi 2 | Alasan |
|---|---|---|---|
| Struktur | 8 fase per teknologi | 4 fase (Team Foundations, Full-stack Foundations, Product Development, Production Engineering) | Kemampuan tim berkembang bertahap; teknologi mengikuti kebutuhan produk |
| Bulan 1-2 | TS (2 minggu) lalu React, terpisah per topik | **Mini Katalog UMKM**: TS dan React ditarik lewat slice 0-8 dengan API palsu (`json-server`); Git workflow, PR/review, debugging, task breakdown dari hari 1; pre-class dan modul React jadi referensi | Produk hidup sejak minggu 1, bukan bulan teknologi. Console app "Inventaris UMKM" diganti Katalog |
| Bulan 3 | Backend, lalu database, lalu digabung di minggu 4 | **Ganti mock jadi asli**: slice yang sama diulang dengan NestJS lalu PostgreSQL, kontrak API dari Bulan 2 tetap; class TS ditarik saat NestJS membutuhkannya | Belajar delivery end-to-end; peserta melihat apa yang dikerjakan tiap layer |
| Bulan 4 | Riset, desain, arsitektur, backlog | Tetap + Sprint 0: minimal 1 slice produk asli jalan | Bulan 4 bukan cuma dokumentasi |
| Bulan 5-9 | Target fitur per bulan | Roadmap indikatif; sprint dengan 3 dimensi (Product/Engineering/Team) | Delivery unit + learning unit; fleksibel |
| Bulan 10-12 | Fitur+QA, deploy+dokumentasi, demo | Quality → Production → Release & Demo, dengan game day, backup, runbook | Transisi ke cara berpikir produksi |
| Chapter | Sharing teknis lintas squad | Capability accelerator berbasis kebutuhan sprint | Chapter tidak jadi kelas tambahan |
| Baru | — | Graduate Capabilities, Capability Matrix, jalur Assessment berbasis bukti, DoD progresif, Risiko & Checkpoint | Menghubungkan tujuan → aktivitas → bukti |
| Dipertahankan | Tribe/Squad/Chapter, pairing, review, showcase, retro, peer feedback, tabel harian TS & React, showcase tiap bulan, rasio 30:70, catatan rolling squad & checkpoint Bulan 3, rotasi peran | (sama, dengan penyempurnaan) | Versi 2 dari dokumen yang sama |

### v2.2 → v3

| Bagian | Versi 2.2 | Versi 3 | Alasan |
|---|---|---|---|
| **Bulan 1** | Slice 0-4 (TS + React), materi pra-coding sebagai jalur paralel | **Full pra-coding**: AI Literacy, CT & Algoritma, Desain Aplikasi & Bisnis, Pitching — 4 minggu penuh, project-based | Fondasi berpikir dulu sebelum ngoding; bekal ini membuat proses coding lebih bermakna |
| **Bulan 2** | Slice 5-8 (React Lanjutan) | Slice 0-4 (TS + React) — pindah dari Bulan 1 | Geser 1 bulan karena Bulan 1 sekarang pra-coding |
| **Bulan 3** | Backend (NestJS + PostgreSQL) | Slice 5-8 (React Lanjutan) — pindah dari Bulan 2 | Geser 1 bulan |
| **Bulan 4** | Kickoff Product + Sprint 0 | Backend (NestJS + PostgreSQL) — pindah dari Bulan 3 | Geser 1 bulan |
| **Bulan 5** | Auth & Dashboard (Sprint) | Kickoff Product + Sprint 0 — pindah dari Bulan 4 | Geser 1 bulan |
| **Bulan 6-10** | Bulan 5-9 lama | Product Development (Auth → CRUD → Search → Cart → Dashboard) — isi sama, geser 1 bulan | Mengisi slot yang bergeser |
| **Bulan 11** | Quality (1 bulan penuh) | **Quality + Production gabungan** (testing, bug bash, CI/CD, deploy, monitoring dalam 1 bulan) | Dikompres supaya total tetap 12 bulan |
| **Bulan 12** | Release & Demo (sama) | Release & Demo (sama) | Tidak berubah |
| **Jalur paralel** | Sesi paralel CT/desain/AI di samping slice | **Dihapus** — topik ini sekarang punya bulan sendiri (Bulan 1); di bulan coding tinggal *diterapkan* sebagai kebiasaan | Lebih fokus; tidak menambah beban ceremony di bulan coding |
| **Capability snapshot** | Akhir Bulan 2, 4, 9, 12 | Akhir Bulan 1, 3, 5, 10, 12 | Menyesuaikan checkpoint baru |

---

## Lampiran B — Template Ringan

**Sprint Canvas** (diisi saat planning, 5 menit):

```text
Sprint: <nama>            Squad: <nama>
Product capability   : User sekarang bisa ...
Engineering capability: Kita belajar/menerapkan ...
Team capability      : Kita melatih ...
Slice yang dikerjakan: ...
Bukti selesai (DoD)  : ...
```

**PR Template:**

```text
Apa yang dibuat?
Cara mencobanya?
Bagian mana yang masih bikin bingung / minta perhatian reviewer?
```

**Format Bantuan:**

```text
Aku mau ...
Sudah coba ...
Hasilnya / error-nya ...
Dugaanku ...
```

**Capability Snapshot** (per peserta):

```text
Nama: ____   Checkpoint: M__
Capability | Level (Belum terlihat / Dengan bantuan / Mandiri / Bisa membimbing) | Bukti | Langkah berikutnya
```
