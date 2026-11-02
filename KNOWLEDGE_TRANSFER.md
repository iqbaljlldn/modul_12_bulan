# DOKUMEN TRANSFER KNOWLEDGE & PANDUAN PENGEMBANGAN
## Kurikulum Project-Based Learning 12 Bulan (Platform Support UMKM)

> **Dokumen ini dibuat sebagai referensi serah terima (knowledge transfer) dan context primer bagi Mentor, Developer, dan AI Assistant** untuk memahami seluruh latar belakang keputusan desain, arsitektur kurikulum, struktur repositori, dan langkah kerja berikutnya.

---

## 1. Ringkasan Eksekutif & Konteks Program

Program ini adalah kurikulum **Project-Based Learning (PBL) intensif selama 12 Bulan** yang dirancang untuk membina **18 lulusan SMA/SMK** (usia ~18–20 tahun) dari hampir 0 hingga memiliki kapabilitas setara **Junior Full-Stack Software Engineer**.

### Karakteristik Utama Program:
1. **Target Peserta:**
   - 18 peserta lulusan SMA/SMK.
   - Sudah melalui program persiapan dasar 2 bulan (HTML, CSS, Git, JS dasar), tetapi **99% belum pernah membangun aplikasi atau ngoding proyek nyata**.
   - Memiliki kecepatan tangkap yang beragam; kurikulum dirancang dengan sistem *pairing*, *squad rolling*, dan jalur *core vs stretch*.
2. **Kultur Kerja Tim (Tribe / Squad / Chapter):**
   - Bukan kelas perkuliahan pasif. Sejak awal, peserta bekerja layaknya tim software engineer (ada daily standup, sprint backlog di `simanajemen.my.id`, pull request review, demo mingguan, dan retrospective).
   - Seluruh tribe bekerja sama membangun satu produk utama: **Platform Support UMKM** (ekosistem katalog produk, manajemen inventaris, order, dan pelaporan untuk UMKM lokal).
3. **Tech Stack Resmi:**
   - **Frontend:** React 19, TypeScript (strict mode, no `any`), Tailwind CSS v4, Vite 8, React Router v7.
   - **Mock API (Bulan 2–3):** `json-server` (port 3001) dengan seed database otomatis.
   - **Backend Asli (Bulan 4 ke atas):** NestJS, TypeScript, PostgreSQL, TypeORM/Prisma.
   - **Quality & Tools:** `oxlint`, `prettier`, Git & GitHub PR workflow.

---

## 2. Filosofi Pedagogi & Prinsip Desain Kurikulum

Kurikulum ini berevolusi dari kurikulum linear tradisional menjadi kurikulum berbasis produk modern (**Versi 3.0**) berdasarkan prinsip-prinsip krusial berikut:

### 2.1 Product-Driven Learning (Bukan Linear)
- **Pola Lama yang Dihindari:** Belajar teori TypeScript sebulan → Teori React sebulan → Backend sebulan → Baru bikin proyek di akhir. (Siswa lupa teori awal saat proyek dimulai).
- **Pola yang Digunakan:** *Produk menjadi kendaraan belajar sejak hari pertama, bukan hadiah di akhir.* Konsep teknis diajarkan tepat ketika produk membutuhkannya:
  $$\text{Problem Produk} \longrightarrow \text{Capability yang Dibutuhkan} \longrightarrow \text{Teori Minimum} \longrightarrow \text{Praktik} \longrightarrow \text{Vertical Slice} \longrightarrow \text{Review}$$

### 2.2 Prinsip Walking Skeleton ("Ganti Mock Jadi Asli")
- Pemula tidak mungkin langsung dibebani membangun full-stack (frontend + backend + database) sekaligus di minggu pertama.
- **Strategi Walking Skeleton:**
  - **Bulan 2–3:** Membangun antarmuka Mini Katalog UMKM secara bertahap (Slice 0–8) menggunakan React + TypeScript asli, sementara backend-nya di-*mock* menggunakan `json-server`.
  - **Bulan 4:** Mengganti `json-server` dengan server backend sungguhan (**NestJS + PostgreSQL**). Karena frontend sudah memiliki spesifikasi ketat di `docs/kontrak-api.md`, proses migrasi backend terasa nyata dan tidak membongkar ulang arsitektur UI.

### 2.3 Kenapa Bulan 1 Sepenuhnya Pra-Coding?
- Lulusan SMA/SMK sering mengalami *mental block* ketika langsung dijejali syntax kode tanpa memahami esensi pemecahan masalah.
- **Bulan 1 didedikasikan untuk Fondasi Berpikir:**
  - **AI Literacy:** Menjadikan AI (LLM) sebagai teman diskusi/tutor, bukan alat *copy-paste* tanpa berpikir.
  - **Computational Thinking & Algoritma:** Dekomposisi masalah, pattern recognition, flowchart alur sistem, dan Entity Relationship Diagram (ERD).
  - **Desain Aplikasi & Bisnis:** Merancang wireframe (Figma), memahami persona pemilik warung/UMKM, dan Value Proposition Canvas.
  - **Pitching:** Melatih kemampuan berbicara, demonstrasi ide, dan mental siap tampil.

### 2.4 Dekomposisi Granular (Kenapa 17 Unit Belajar per Bulan?)
- Pada iterasi awal, materi Bulan 2 dan 3 hanya berupa 4 file slice tebal. Bagi lulusan SMA, melompat dari kartu statis ke form validasi interaktif dalam 1 file menyebabkan *cognitive cliff* yang curam.
- Oleh karena itu, setiap bulan dipecah menjadi **17 unit belajar granular** (4 minggu $\times$ 3–4 sesi):
  - **Hari 1:** Teori konsep dasar & *mental model* (misal: pure function validation / Rules of Hooks).
  - **Hari 2:** Arsitektur & pola kode (misal: Context API 3-file pattern / Custom Hook extraction).
  - **Hari 3:** Eksekusi integrasi Vertical Slice ke aplikasi katalog.
  - **Hari 4:** Latihan pemantapan, *edge cases*, uji aksesibilitas, dan persiapan PR review.

---

## 3. Peta Navigasi & Struktur Direktori Repositori

```text
/home/iqbaal/modul_12_bulan/
│
├── KNOWLEDGE_TRANSFER.md                 # [Dokumen ini] Panduan serah terima & master prompt AI
├── kurikulum-pbl-12-bulan.md             # Dokumen Master Kurikulum v3.0 (Blueprint 12 Bulan)
│
├── 1-modul-pra-coding-bulan1/            # BUKU MATERI BULAN 1: Pra-Coding Foundations
│   ├── 0-Orientasi/                      # Panduan squad, jadwal belajar, panduan mentor
│   ├── 1-AI-Literacy/                    # Pengenalan LLM, prompt engineering dasar, etika AI
│   ├── 2-Computational-Thinking/         # Dekomposisi logika, algoritma, flowchart, ERD
│   ├── 3-Desain-Aplikasi-dan-Bisnis/     # User persona UMKM, Wireframing, Figma dasar, VPC
│   └── 4-Pitching-dan-Showcase/          # Storytelling, slide deck, demo produk, showcase M1
│
├── modul-katalog-umkm-bulan2-3/          # BUKU MATERI BULAN 2 & 3: React & TypeScript
│   ├── README.md                         # Peta belajar & silabus lengkap Bulan 2 & 3
│   ├── 0-Persiapan/                      # Setup repo starter, Git workflow, template bantuan
│   ├── 1-TypeScript-React-Dasar/         # BULAN 2: 17 unit materi (Slice 0 s/d Slice 4)
│   │   ├── 01a s/d 01d                   # M1: Orientasi, JSX, Styling, SLICE 0 (Kartu Produk)
│   │   ├── 02a s/d 02e                   # M2: useState, useEffect, SLICE 1 (Fetch), SLICE 2 (Form)
│   │   ├── 03a s/d 03c                   # M3: HTTP Methods, SLICE 3 (Edit/Delete, Error state)
│   │   ├── 04a s/d 04c                   # M4: React Router, SLICE 4 (Detail Produk), Showcase v1
│   │   ├── LATIHAN-TAMBAHAN.md           # Latihan pengayaan mandiri
│   │   └── PANDUAN-MENTOR.md             # Panduan instruktur & checkpoint kelulusan Bulan 2
│   └── 2-React-Lanjutan/                 # BULAN 3: 17 unit materi (Slice 5 s/d Slice 8)
│       ├── 01a s/d 01d                   # M1: Tailwind v4, Custom Hooks, SLICE 5 (Kategori)
│       ├── 02a s/d 02d                   # M2: Form Validation murni, Context API, SLICE 6 (Toast)
│       ├── 03a s/d 03d                   # M3: Debounce 400ms, URL Params, SLICE 7 (Filter/Page)
│       ├── 04a s/d 04c                   # M4: Responsive HP, SLICE 8 (Kontrak API & Showcase v2)
│       ├── LATIHAN-TAMBAHAN.md           # Latihan pengayaan mandiri
│       └── PANDUAN-MENTOR.md             # Panduan instruktur & checkpoint kelulusan Bulan 3
│
├── katalog-umkm-starter/                 # KODE TEMPLATE UNTUK SISWA (Starter Kit)
│   ├── package.json                      # Vite + React 19 + TypeScript + json-server
│   ├── scripts/ensure-db.mjs             # Inisialisasi db.json otomatis
│   ├── scripts/reset-db.mjs              # Reset database ke kondisi awal
│   └── src/                              # Kerangka awal untuk dikerjakan siswa
│
├── katalog-umkm-solusi-mentor/           # REPO SOLUSI RESMI BULAN 2 (Slice 0-4)
│   └── katalog-umkm-solusi/              # Implementasi lengkap Slice 0–4 untuk acuan mentor
│
├── katalog-umkm-solusi-mentor-2/         # REPO SOLUSI RESMI BULAN 3 (Slice 5-8)
│   └── katalog-umkm-solusi/
│       ├── docs/kontrak-api.md           # SPESIFIKASI RESMI API (Acuan Backend Bulan 4)
│       └── src/                          # Implementasi Tailwind v4, Context, Hooks, URL params
│
└── modul-react-programmer-pit-master/    # REPOSITORI RUJUKAN TEORI (Bootcamp Reference)
    ├── 0-Intro/                          # Ekosistem JavaScript & Node.js
    ├── 1-Pengenalan_React/               # SPA, JSX, Component, Props, State dasar
    ├── 2-State_Management_&_Hooks/       # Lifecycle, useEffect, Forms, HTTP requests
    ├── 3-Routing_&_Advanced_React_Patterns/ # Context, Custom Hooks, React Router, URL sync
    └── 4-Advanced_Topics/                # TypeScript di React, Tailwind CSS, Performance
```

---

## 4. Rincian Teknis Slices (Katalog UMKM)

| Slice | Bulan/Minggu | Fitur Utama | Konsep Kunci |
|---|---|---|---|
| **Slice 0** | B2 / M1 | Tampilan Daftar Kartu Produk Statis | JSX, TypeScript Interfaces (`Product`), Props passing, `.map()` rendering |
| **Slice 1** | B2 / M2 | Fetch Data dari `json-server` | `useState`, `useEffect`, fetch lifecycle (Loading, Error, Data states) |
| **Slice 2** | B2 / M2 | Form Tambah Produk Baru | Controlled Inputs, Form Submission, POST request, immutability update |
| **Slice 3** | B2 / M3 | Ubah Status & Hapus Produk | HTTP PATCH/DELETE, Modal Konfirmasi, Feedback handling |
| **Slice 4** | B2 / M4 | Halaman Detail Produk & Routing | React Router v7 (`BrowserRouter`, `useParams`, `Link`, 404 page) |
| **Slice 5** | B3 / M1 | Filter Kategori & Custom Hook | Tailwind CSS v4, Ekstraksi Custom Hook (`useProducts`, `useCategories`) |
| **Slice 6** | B3 / M2 | Validasi Form Murni & Global Toast | Arsitektur validasi `validate.ts`, Context API 3-File Pattern (`ToastContext`) |
| **Slice 7** | B3 / M3 | Search Debounce & Sinkronisasi URL | Debounce custom hook (400ms), `useSearchParams` URL as single source of truth, pagination |
| **Slice 8** | B3 / M4 | UI Responsif HP & Kontrak API | Mobile-first breakpoints (`sm:`, `md:`), touch target 44px, `docs/kontrak-api.md` |

---

## 5. Standar Kode & Aturan Teknis (Rules of Code)

1. **TypeScript Strict:**
   - Dilarang keras memakai tipe `any`. Gunakan interface eksplisit di folder `src/types/`.
2. **Context API 3-File Architecture:**
   - Pisahkan menjadi: `src/context/ToastContext.tsx` (interface & create context), `src/context/ToastProvider.tsx` (komponen provider & state), dan hook pengakses khusus `useToast()`.
3. **Pemisahan Logika & Tampilan (Custom Hooks):**
   - Komponen UI di `src/components/` tidak boleh melakukan `fetch()` langsung; logika request dibungkus di `src/api/` dan diakses melalui custom hook di `src/hooks/`.
4. **URL sebagai Single Source of Truth:**
   - Untuk pencarian, filter kategori, pengurutan, dan nomor halaman (Slice 7), state disimpan di URL query parameter (`?q=...&category_id=...&page=...`) agar halaman dapat di-*bookmark* dan mendukung riwayat navigasi browser (tombol Back/Forward).
5. **Validasi Form Murni:**
   - Fungsi validasi harus berupa *pure function* tanpa efek samping, mengembalikan objek error terstruktur `{ [field]: string }`.

---

## 6. Spesifikasi Kontrak API (`docs/kontrak-api.md`)

Kontrak ini adalah jembatan vital antara frontend Bulan 3 dan backend NestJS Bulan 4:

- **Entity Product:**
  ```ts
  interface Product {
    id: number
    name: string
    description: string
    price: number
    stock: number
    status: 'active' | 'draft'
    category_id: number
    merchant_name: string
    created_at: string // ISO 8601
  }
  ```
- **Endpoints:**
  - `GET /products`: Support query `q`, `category_id`, `_sort`, `_order`, `_page`, `_limit`. Respons header `X-Total-Count` wajib disertakan untuk keperluan pagination.
  - `GET /products/:id`: Mengembalikan 1 produk atau 404.
  - `POST /products`: Validasi body DTO (`CreateProductDto`), kembalikan 201.
  - `PATCH /products/:id`: Update parsial field produk, kembalikan 200.
  - `DELETE /products/:id`: Hapus produk, kembalikan 200/204.
  - `GET /categories`: Mengembalikan daftar `{ id: number, name: string }`.

---

## 7. Status Eksekusi & Roadmap Selanjutnya

### Yang Sudah Selesai (Completed ✅):
- [x] Master Kurikulum 12 Bulan Versi 3.0 (`kurikulum-pbl-12-bulan.md`).
- [x] Seluruh materi Bulan 1 Pra-Coding (5 folder modul lengkap).
- [x] Seluruh materi Bulan 2 TypeScript & React Dasar (17 unit file belajar granular + panduan mentor).
- [x] Seluruh materi Bulan 3 React Lanjutan (17 unit file belajar granular + panduan mentor).
- [x] Starter kit siswa (`katalog-umkm-starter`).
- [x] Solusi acuan mentor Bulan 2 (`katalog-umkm-solusi-mentor`).
- [x] Solusi acuan mentor Bulan 3 (`katalog-umkm-solusi-mentor-2`).
- [x] Pemetaan bab teori dari `modul-react-programmer-pit-master`.

### Langkah Kerja Berikutnya (Next Milestones 🚀):
1. **Penyusunan Modul Bulan 4 (Full-stack Foundations — NestJS & PostgreSQL):**
   - Membuat modul pembelajaran backend NestJS yang menggantikan `json-server`.
   - Mengajarkan struktur NestJS (Controller, Service, Module, DTO, Entity).
   - Mengajarkan koneksi database PostgreSQL via TypeORM / Prisma.
   - Mengimplementasikan filter, search, pagination, dan header `X-Total-Count` pada endpoint NestJS sesuai kontrak.
   - Menguji koneksi frontend Katalog UMKM v2 langsung ke server NestJS tanpa mengubah kode komponen.
2. **Pembuatan Starter & Solusi Mentor Backend Bulan 4:**
   - Template project NestJS + Docker Compose (PostgreSQL).
3. **Penyusunan Fase 2 Bulan 5 s/d Fase 4:**
   - Sprint 0, Scrum backlog, arsitektur Platform UMKM bersama, dan CI/CD deployment.

---

## 8. Master System Prompt (Siap Copy-Paste untuk Sesi AI Baru)

> **PETUNJUK:** Salin seluruh blok teks di bawah ini ke prompt pertama saat membuka sesi AI baru (Claude, ChatGPT, Gemini, dsb.) di repositori ini untuk menginisialisasi AI dengan pemahaman 100% tentang kurikulum ini.

```text
KAMU ADALAH LEAD MENTOR DAN SENIOR SOFTWARE CURRICULUM ARCHITECT UNTUK PROGRAM CODING BOOTCAMP 12 BULAN (PROJECT-BASED LEARNING).

### KONTEKS UTAMA REPOSITORI:
1. TARGET AUDIENCE:
   - 18 siswa lulusan SMA/SMK (usia ~18-20 tahun).
   - Latar belakang non-IT; 99% belum pernah ngoding proyek nyata sebelumnya.
   - Karakteristik: Rentan terhadap 'cognitive overload'. Membutuhkan analogi dunia nyata, penjelasan bertahap (scaffolding), porsi 30% konsep : 70% praktik, serta kultur belajar yang aman untuk berbuat salah dan bertanya.

2. MODEL OPERASIONAL & PEDAGOGI:
   - Pola Belajar: Tribe-like team (bukan kelas ceramah akademis). Menggunakan Sprint, Standup, PR Review di GitHub.
   - Prinsip 'Walking Skeleton' (Ganti Mock Jadi Asli):
     * Bulan 1: Pra-Coding Foundations (AI Literacy, Computational Thinking, Desain UX/Bisnis, Pitching).
     * Bulan 2: Katalog Produk Hidup (TypeScript + React Dasar, Slice 0-4) dengan mock API json-server.
     * Bulan 3: React Lanjutan (Slice 5-8: Tailwind v4, Form Validation, Context API, Debounce, URL State, Kontrak API).
     * Bulan 4: Backend NestJS + PostgreSQL menggantikan json-server sesuai kontrak API tanpa merusak frontend.
     * Bulan 5-10: Pembangunan Platform Support UMKM nyata secara kolaboratif (Sprint-based).
     * Bulan 11-12: Production Engineering, CI/CD, Deployment, dan Public Showcase.
   - Prinsip Dekomposisi: Setiap bulan coding dijabarkan menjadi 17 unit belajar granular (4 minggu x 3-4 sesi), bukan modul slice padat yang membingungkan pemula.

3. STRUKTUR DIREKTORI REPO:
   - kurikulum-pbl-12-bulan.md: Master kurikulum v3.0.
   - 1-modul-pra-coding-bulan1/: Modul Bulan 1 (AI Literacy, CT, Desain, Pitching).
   - modul-katalog-umkm-bulan2-3/: Modul belajar Bulan 2 (TS+React Dasar) & Bulan 3 (React Lanjutan).
   - katalog-umkm-starter/: Starter kit siswa (Vite, React 19, TS, json-server).
   - katalog-umkm-solusi-mentor/: Solusi resmi mentor Bulan 2.
   - katalog-umkm-solusi-mentor-2/: Solusi resmi mentor Bulan 3 (termasuk docs/kontrak-api.md).
   - modul-react-programmer-pit-master/: Sumber rujukan konsep teori.

4. PEDOMAN KUALITAS KODE (STANDAR TEKNIS):
   - Strict TypeScript: Hindari 'any'. Gunakan interface yang rapi dan terpusat di types/.
   - State & URL Synchronization: URLSearchParams digunakan sebagai sumber kebenaran untuk filter, cari, dan pagination.
   - React Architecture:
     * Custom hooks untuk memisahkan UI dan data fetching.
     * Context API menggunakan 3-file pattern (Context, Provider, custom Hook).
     * Validasi form menggunakan pure validation function (validate.ts) yang mengembalikan error map terstruktur.
   - Styling: Modern Tailwind CSS v4 dengan pendekatan Mobile-First (minimal touch target 44px).
   - Kontrak API: Mematuhi spesifikasi di katalog-umkm-solusi-mentor-2/katalog-umkm-solusi/docs/kontrak-api.md.

5. ATURAN DALAM MENJAWAB:
   - Komunikatif, berwawasan mentor ramah, sistematis, dan solutif (Bahasa Indonesia).
   - Saat membuat modul atau penjelasan materi baru, selalu ikuti Learning Loop: Why -> Concept -> Practice -> Product Application -> Review.
   - Pastikan setiap contoh kode siap pakai, memiliki type definition lengkap, dan tidak membingungkan pemula.
   - Siap melanjutkan milestone berikutnya: Pembuatan materi Bulan 4 (NestJS Backend & PostgreSQL) atau pengembangan materi lainnya.
```
