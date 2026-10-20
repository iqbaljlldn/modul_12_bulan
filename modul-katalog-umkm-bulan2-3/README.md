# Modul Belajar — Platform Katalog UMKM

Modul ini adalah bahan ajar resmi untuk **12 Bulan Kurikulum Project-Based Learning** (Platform UMKM), mencakup **Bulan 2 (TypeScript + React Dasar)** dan **Bulan 3 (React Lanjutan & Kontrak API)**.

Setiap bab dirancang per topik spesifik (`.md`) dengan pendekatan **Product-Driven Learning**: konsep teori React dan TypeScript dijembatani langsung ke kebutuhan produk Katalog UMKM yang nyata, bukan sekadar tutorial abstrak.

---

## Cara Pakai

- **Mentor:** Baca `PANDUAN-MENTOR.md` di dalam folder masing-masing bulan (`1-TypeScript-React-Dasar` untuk Bulan 2 dan `2-React-Lanjutan` untuk Bulan 3) sebelum mengajar. Di dalamnya terdapat alokasi waktu per sesi, poin mini-lesson (20-30 menit), jebakan mental model siswa, dan kriteria checkpoint mingguan.
- **Peserta:** Baca bab sesuai urutan nomor. Sebelum masuk ke sesi implementasi slice, pelajari **Bacaan Wajib** yang dirujuk dari modul bootcamp React Programmer Pit.
- **Solusi & Pengujian:** Semua kode yang ada di modul ini sudah diuji secara nyata (build TypeScript, oxlint, dan endpoint API) di repo referensi mentor (`katalog-umkm-solusi-mentor-2`).

---

## Prasyarat Peserta

1. **Bulan 1 — Fondasi Pra-Coding** (`modul-pra-coding-bulan1`): Computational Thinking (Dekomposisi, Algoritma, Flowchart, ERD), AI Literacy, Wireframe & UX, Value Proposition Canvas, dan Git kolaborasi dokumen.
2. **Pre-class Programming** ([mhubaib/module-pre-class-programming](https://github.com/mhubaib/module-pre-class-programming)): HTML, CSS, Git workflow dasar, dan JavaScript modern (ES6+, array methods, async/await, fetch).
3. **Modul Bootcamp React** ([malfazakki/modul-react-programmer-pit](https://github.com/malfazakki/modul-react-programmer-pit)): Digunakan sebagai bahan bacaan wajib per bab, bukan diajarkan ulang dari nol.

---

## Struktur Lengkap Modul

```text
modul-katalog-umkm/
├── README.md                         # Kamu di sini
├── 0-Persiapan/                      # Orientasi sebelum Slice 0
│   ├── PANDUAN-MENTOR.md
│   ├── 01-tentang-modul-ini.md
│   ├── 02-setup-starter.md
│   ├── 03-alur-git-dan-pr.md
│   └── 04-format-minta-bantuan.md
│
├── 1-TypeScript-React-Dasar/         # Bulan 2: Slice 0-4 (Mini Katalog UMKM v1)
│   ├── PANDUAN-MENTOR.md
│   ├── 01a-orientasi-react.md               # SPA, Virtual DOM, Vite vs CRA (Bab 1.1)
│   ├── 01b-jsx-dan-komponen-bertipe.md      # JSX, Props, TS Types (Bab 1.2, 1.3, 4.1)
│   ├── 01c-styling-kartu-produk.md          # CSS Classes & Box Model (Bab 1.4)
│   ├── 01d-tipe-dasar-dan-list-rendering.md # SLICE 0: Kartu & List Produk
│   ├── 02a-state-dan-usestate.md            # useState & Immutability (Bab 1.5)
│   ├── 02b-useeffect-dan-lifecycle.md       # useEffect & Lifecycle (Bab 2.3)
│   ├── 02c-fetch-dan-loading-state.md       # SLICE 1: Fetch API json-server
│   ├── 02d-event-handling-dan-form.md       # Controlled Form & Events (Bab 2.1)
│   ├── 02e-form-tambah-produk.md            # SLICE 2: Form Tambah Produk
│   ├── 03a-http-methods-dan-api-patterns.md # PUT, PATCH, DELETE & Error (Bab 2.4)
│   ├── 03b-edit-hapus-dan-error.md          # SLICE 3: Edit & Hapus Produk
│   ├── 03c-state-management-patterns.md     # Lifting State & Optimistic UI (Bab 2.5)
│   ├── 04a-react-router-dasar.md            # BrowserRouter & Route Param (Bab 3.4)
│   ├── 04b-routing-dan-detail.md            # SLICE 4: Halaman Detail Produk
│   ├── 04c-konsolidasi-dan-refactor.md      # Review, Refactor, Showcase v1
│   ├── LATIHAN-TAMBAHAN.md
│   └── PANDUAN-MENTOR.md
│
└── 2-React-Lanjutan/                  # Bulan 3: Slice 5-8 (Mini Katalog UMKM v2)
    ├── PANDUAN-MENTOR.md
    ├── 01a-styling-tailwind-dan-komponen-ui.md # Tailwind v4 & Composition (Bab 1.4, 4.2)
    ├── 01b-custom-hooks-konsep-dan-pola.md     # Konsep Custom Hook & useCategories (Bab 3.2)
    ├── 01c-kategori-styling-custom-hook.md     # SLICE 5: Kategori, Tailwind & useProducts
    ├── 01d-latihan-dan-pemantapan-slice5.md    # Graceful degradation & Badge UI
    ├── 02a-validasi-form-dan-arsitektur-input.md # Validasi Murni & Aksesibilitas (Bab 2.1, 4.1)
    ├── 02b-context-api-dan-global-state.md     # Context API 3-File Architecture (Bab 3.1)
    ├── 02c-validasi-dan-context.md             # SLICE 6: Validasi Form & Notifikasi Toast
    ├── 02d-latihan-dan-pemantapan-slice6.md    # Multi-variant Toast & Realtime clearance
    ├── 03a-debounce-dan-optimasi-input.md      # Debounce 400ms & useDebouncedValue (Bab 2.3, 3.3)
    ├── 03b-url-search-params-dan-server-query.md # URL State & Server Query (Bab 3.5)
    ├── 03c-cari-filter-pagination.md           # SLICE 7: Search, Filter, Sort, Pagination
    ├── 03d-latihan-dan-pemantapan-slice7.md    # Empty State & Browser History Testing
    ├── 04a-desain-responsif-dan-layout-mobile.md # Mobile-First Layout HP UMKM (Bab 4.2)
    ├── 04b-konsolidasi-dan-kontrak-api.md      # SLICE 8: docs/kontrak-api.md & Decision Log
    ├── 04c-code-audit-dan-persiapan-showcase.md # Audit oxlint, build, Showcase v2
    ├── LATIHAN-TAMBAHAN.md
    └── PANDUAN-MENTOR.md
```

---

## Hasil Akhir Bulan 3 & Jembatan ke Bulan 4

Di akhir Bulan 3:
1. **Frontend:** Mini Katalog UMKM v2 beroperasi penuh dengan performa tinggi, UI responsif Tailwind, validasi input yang aman, notifikasi global, dan sinkronisasi state di URL.
2. **Spesifikasi:** Dokumen `docs/kontrak-api.md` tuntas disepakati bersama oleh tribe.
3. **Bulan 4 (Backend Full-stack Foundations):** Kita akan membangun server REST API sungguhan menggunakan **NestJS**, menghubungkannya ke database **PostgreSQL**, dan menggantikan `json-server` sepenuhnya mengikuti spesifikasi kontrak API yang sudah dibuat ini!
