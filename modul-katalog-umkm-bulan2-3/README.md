# Modul Belajar — Platform Katalog UMKM

Modul ini adalah bahan ajar resmi untuk **12 Bulan Kurikulum Project-Based Learning** (Platform UMKM), mencakup **Bulan 2 (TypeScript + React Dasar)** dan **Bulan 3 (React Lanjutan & Kontrak API)**.

Setiap bab dirancang per topik spesifik (`.md`) dengan pendekatan **Product-Driven Learning**: konsep teori React dan TypeScript dijembatani langsung ke kebutuhan produk nyata Mini Katalog UMKM, bukan sekadar tutorial atau teori abstrak.

---

## Model Belajar & Ritme Harian

Program berlangsung dalam setting bootcamp residensial 24/7 dengan jadwal belajar terstruktur (Senin - Jumat):
- **Blok 1 (08.00 - 10.00 / 120 menit):** Standup harian (10-15m), guided reading / mini-lesson (maks 25m), dan coding terbimbing bersama mentor.
- **Blok 2 (10.30 - 11.20 / 50 menit):** Pairing (driver/navigator rolling) dan debug clinic. Tanpa penambahan materi baru.
- **Blok 3 (13.00 - 14.20 / 80 menit):** Tugas mandiri individual (20-30m) dikerjakan di kelas dengan mentor siaga, dilanjutkan PR code review dan lightning demo singkat.
- **Malam:** Bebas tugas wajib. Hanya bacaan santai atau eksplorasi opsional.
- **Sabtu:** Sprint Review (demo live tiap squad) dan Sprint Retrospektif (Mad/Sad/Glad atau I Like/I Wish/What If).

Model evaluasi menggunakan **Checklist Kapabilitas** (*Siap / Hampir Siap / Perlu Pendampingan*) tanpa sistem penilaian angka akademik.

---

## Prasyarat Murid

1. **Bulan 1 — Fondasi Pra-Coding** (`modul-pra-coding-bulan1`): Computational Thinking (Dekomposisi, Algoritma, Flowchart, ERD), AI Literacy, Wireframe & UX, Value Proposition Canvas, dan kolaborasi Git.
2. **Pre-class Programming**: HTML, CSS, Git workflow dasar, dan JavaScript modern (ES6+, array methods, async/await, fetch).
3. **Modul Bootcamp React**: Digunakan sebagai bahan rujukan pengayaan terstruktur di kelas, bukan prasyarat hafalan sebelum masuk sesi.

---

## Struktur Lengkap Modul

```text
modul-katalog-umkm/
├── README.md                         # Kamu di sini
├── 0-Persiapan/                      # Orientasi sebelum Slice 0
│   ├── PANDUAN-MENTOR.md             # Ritme harian, setup env, kunci json-server 0.17.x
│   ├── 01-tentang-modul-ini.md       # Konsep slice & alur product-driven
│   ├── 02-setup-starter.md           # Setup repo starter, Node 22, dev server
│   ├── 03-alur-git-dan-pr.md         # Alur branch, commit, PR, review, merge
│   └── 04-format-minta-bantuan.md    # Format 4 poin minta bantuan saat stuck
│
├── 1-TypeScript-React-Dasar/         # Bulan 2: Slice 0-4 (Mini Katalog UMKM v1)
│   ├── PANDUAN-MENTOR.md             # Peta 4 minggu, ritme harian, tabel tugas, checklist
│   ├── 01a-orientasi-react.md               # SPA, Virtual DOM, Vite vs CRA
│   ├── 01b-jsx-dan-komponen-bertipe.md      # JSX, Props bertipe, ProductCard
│   ├── 01c-styling-kartu-produk.md          # CSS Classes & Grid responsif
│   ├── 01d-tipe-dasar-dan-list-rendering.md # SLICE 0: Kartu & List Rendering Statis
│   ├── 02a-state-dan-usestate.md            # useState & Immutability Array
│   ├── 02b-useeffect-dan-lifecycle.md       # useEffect & Lifecycle, Cleanup
│   ├── 02c-fetch-dan-loading-state.md       # SLICE 1: Fetch API json-server
│   ├── 02d-event-handling-dan-form.md       # Controlled Form & SyntheticEvent
│   ├── 02e-form-tambah-produk.md            # SLICE 2: Form Tambah Produk (POST)
│   ├── 03a-http-methods-dan-api-patterns.md # PATCH, DELETE, ApiError
│   ├── 03b-edit-hapus-dan-error.md          # SLICE 3: Edit Inline & Hapus Produk (2 hari)
│   ├── 03c-state-management-patterns.md     # Lifting State & Alur Data (One-Way)
│   ├── 04a-react-router-dasar.md            # BrowserRouter & Link vs <a>
│   ├── 04b-routing-dan-detail.md            # SLICE 4: Halaman Detail & Penanganan 404
│   ├── 04c-konsolidasi-dan-refactor.md      # Code Audit, oxlint, Showcase v1
│   └── LATIHAN-TAMBAHAN.md                  # Tantangan stretch opsional
│
└── 2-React-Lanjutan/                  # Bulan 3: Slice 5-8 (Mini Katalog UMKM v2)
    ├── PANDUAN-MENTOR.md
    ├── 01a-styling-tailwind-dan-komponen-ui.md # Tailwind v4 & Composition
    ├── 01b-custom-hooks-konsep-dan-pola.md     # Konsep Custom Hook & useCategories
    ├── 01c-kategori-styling-custom-hook.md     # SLICE 5: Kategori, Tailwind & useProducts
    ├── 01d-latihan-dan-pemantapan-slice5.md    # Graceful degradation & Badge UI
    ├── 02a-validasi-form-dan-arsitektur-input.md # Validasi Murni & Aksesibilitas
    ├── 02b-context-api-dan-global-state.md     # Context API 3-File Architecture
    ├── 02c-validasi-dan-context.md             # SLICE 6: Validasi Form & Notifikasi Toast
    ├── 02d-latihan-dan-pemantapan-slice6.md    # Multi-variant Toast & Realtime clearance
    ├── 03a-debounce-dan-optimasi-input.md      # Debounce 400ms & useDebouncedValue
    ├── 03b-url-search-params-dan-server-query.md # URL State & Server Query
    ├── 03c-cari-filter-pagination.md           # SLICE 7: Search, Filter, Sort, Pagination
    ├── 03d-latihan-dan-pemantapan-slice7.md    # Empty State & Browser History Testing
    ├── 04a-desain-responsif-dan-layout-mobile.md # Mobile-First Layout HP UMKM
    ├── 04b-konsolidasi-dan-kontrak-api.md      # SLICE 8: docs/kontrak-api.md & Decision Log
    ├── 04c-code-audit-dan-persiapan-showcase.md # Audit oxlint, build, Showcase v2
    ├── LATIHAN-TAMBAHAN.md
    └── PANDUAN-MENTOR.md
```

---

## Catatan Teknis Tooling Kunci

- **`json-server` (0.17.x):** Dependensi ini sengaja dikunci pada versi 0.17.4 dan **tidak boleh di-upgrade ke versi 1.x**. Versi 1.x memodifikasi perilaku parameter URL (`_limit`, `_sort`, `_order`) dan menghilangkan header pagination `X-Total-Count` yang menjadi acuan kontrak belajar kita.
- **Node.js:** Versi yang direkomendasikan adalah Node.js 22 LTS (minimal Node 20+).
- **Linter & Type Checking:** Menggunakan `oxlint` untuk audit kecepatan tinggi dan `tsc -b` untuk pengecekan tipe statis yang ketat.

---

## Hasil Akhir & Jembatan ke Bulan 4

Di akhir Bulan 3:
1. **Frontend:** Mini Katalog UMKM v2 beroperasi penuh dengan performa tinggi, UI responsif Tailwind v4, validasi input yang aman, notifikasi global, dan sinkronisasi state di URL.
2. **Spesifikasi:** Dokumen `docs/kontrak-api.md` tuntas disepakati bersama oleh tribe.
3. **Bulan 4 (Backend Full-stack Foundations):** Kita akan membangun server REST API sungguhan menggunakan **NestJS**, menghubungkannya ke database **PostgreSQL**, dan menggantikan `json-server` sepenuhnya mengikuti spesifikasi kontrak API yang sudah dibuat ini!
