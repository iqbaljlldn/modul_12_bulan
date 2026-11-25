# Panduan Mentor — 2. React Lanjutan (Bulan 3)

**Peserta:** 12 orang, dibagi menjadi 3 squad rolling berbasis kekuatan (masing-masing 4 orang).  
**Durasi:** 4 minggu (20 hari belajar efektif + 4 Sabtu Sprint Review, mencakup Slice 5–8).  
**Rasio Waktu:** 30% konsep/mini-lesson : 70% praktik langsung dan coding terbimbing.  
**Tooling Utama:** **Node.js 26**, Vite + React + TypeScript, Tailwind CSS v4 (`@tailwindcss/vite`), `json-server@0.17.4` (dikunci, jangan upgrade ke `1.x`), dan `oxlint`.

---

## Keputusan Penting Sebelum Minggu 1

> **Standar Styling Tribe: Tailwind CSS v4 vs CSS Module?**  
> Modul ini disusun menggunakan **Tailwind CSS v4** dengan plugin `@tailwindcss/vite`.  
> Jika tribe kamu memutuskan memilih CSS Module, konsep arsitektur (*component composition*, *custom hook*, *context*, *url state*) tetap 100% sama — kamu hanya perlu menyesuaikan contoh kode styling di unit `01a`. Putuskan ini **sebelum hari pertama Minggu 1** dan catat di `docs/decision-log.md`.

> **Kepemilikan Repo vs Squad di Bulan 3:**  
> Kode proyek `katalog-umkm` tetap dikerjakan di **repositori pribadi masing-masing** agar seluruh ke-12 peserta menguasai semua lapisan (*custom hook*, *context*, *URL state*, *responsive layout*). **Squad (3 squad @ 4 orang)** mulai dirotasi berbasis kekuatan agar saling mengisi, berperan sebagai partner pairing harian, **PR code reviewer dengan checklist dasar** sebelum merge, penyusun konsensus `docs/kontrak-api.md` & `docs/decision-log.md`, serta tim presenter pada Sprint Review Sabtu.

---

## 1. Ritme Harian Belajar (Senin - Jumat)

Jadwal harian residensial berdurasi 250 menit dibagi menjadi 3 blok terstruktur:

| Blok | Waktu | Durasi | Format Aktivitas Mentor & Murid |
|---|---|---|---|
| **Blok 1** | 08.00 - 10.00 | 120 menit | **Standup Harian (10-15m):** Tiap murid menyampaikan progres kemarin, rencana hari ini, dan kendala/blocker.<br>**Guided Reading / Mini-lesson (maks 25m):** Mentor memandu membaca bagian inti unit hari ini di kelas atau membedah konsep via diagram.<br>**Coding Terbimbing:** Mentor mendemokan langkah arsitektur secara live di layar proyektor, murid mengetik dan memverifikasi di laptop masing-masing. |
| *Istirahat* | 10.00 - 10.30 | 30 menit | Istirahat penyegaran, camilan, dan rileksasi mata. |
| **Blok 2** | 10.30 - 11.20 | 50 menit | **Pairing & Debug Clinic (Tanpa Materi Baru):** Murid berpasangan (driver mengetik, navigator menyimak, tukar peran tiap 25m). Mentor berkeliling membantu debugging TypeScript, Tailwind, React Hooks, atau Git. |
| *Istirahat* | 11.20 - 13.00 | 100 menit | Istirahat siang, makan, ibadah, dan rehat. |
| **Blok 3** | 13.00 - 14.20 | 80 menit | **Tugas Mandiri (20-30m):** Dikerjakan individual di kelas dalam folder repo proyek (`tugas/tugas_<kode>.md`), mentor siaga menjawab pertanyaan.<br>**PR Code Review Checklist & Lightning Demo (50m):** Murid membuka PR ke branch `main` repo pribadinya. Minimal 1 rekan squad mereview dengan **Checklist Dasar** (nama jelas? tipe benar? ada bug? lolos `npm run lint` & `npm run build`?), dilanjutkan demo singkat 1-2 squad. |
| **Malam** | Fleksibel | Bebas | **Tidak ada tugas wajib.** Menjaga ritme istirahat murid. Hanya bahan bacaan santai atau tantangan opsional di `LATIHAN-TAMBAHAN.md` bagi yang selesai lebih cepat. |

### Sabtu: Sprint Review & Retrospektif Mingguan

- **Sprint Review (09.00 - 10.00):** Demo live tiap squad (**3 squad @ 12-15 menit**). Setiap akhir minggu (`01d`, `02d`, `03d`, `04c`) memuat **Misi Squad Mingguan**: keempat anggota memastikan PR repo masing-masing lolos review, membagi peran demo (Driver Demo, DevTools/Code Inspector, Storyteller Bug), dan mentor mengundi repo anggota yang ditampilkan di proyektor. Khusus Minggu 4, Sprint Review diperluas menjadi **Showcase Mini Katalog UMKM v2 + Presentasi Kontrak API ke calon Chapter Backend**.
- **Sprint Retrospektif (10.15 - 11.30):** Evaluasi ritme kerja tim pada akhir Minggu 2 (tengah bulan) dan Minggu 4 (akhir bulan) menggunakan papan **Mad / Sad / Glad** atau **I Like / I Wish / What If** *(Minggu 1 & 3 cukup retrospektif kilat 15 menit)*. Mentor memfasilitasi tanpa menghakimi. *(Sabtu bebas PR setelah kelas selesai.)*

---

## 2. Peta Sesi 4 Minggu (20 Hari Belajar + 4 Sabtu Review)

```text
Minggu 1: Kategori, Tailwind CSS v4 & Custom Hook (Slice 5)
  Hari 1:  01a Styling Standar Tribe: Tailwind CSS v4 & Komponen UI Atomik (Button, Input, Badge)
  Hari 2:  01b Custom Hooks: Konsep, Rules of Hooks & useCategories (Graceful Degradation)
  Hari 3:  01c Slice 5: Migrasi Styling Katalog, Pilihan Kategori & Custom Hook useProducts
  Hari 4:  01d Pemantapan Slice 5: Terapkan Badge di ProductCard & Uji Ketahanan API
  Hari 5:  Konsolidasi Slice 5, Debug Clinic & PR Cross-Review Squad (tanpa materi baru)
  Sabtu:   Sprint Review 1 (Target: UI Tailwind v4 rapi, relasi kategori & useProducts jalan)

Minggu 2: Validasi Form & Notifikasi Global Context (Slice 6)
  Hari 6:  02a Validasi Form Murni (validate, validateEdit, FormErrors, aria-invalid)
  Hari 7:  02b Context API & Global Toast Notification (Arsitektur 3 File & Vite Fast Refresh)
  Hari 8:  02c Slice 6: Integrasi Validasi ke ProductForm/ProductEditForm & Toast CRUD
  Hari 9:  02d Pemantapan Slice 6: Varian Warna Toast & Real-time Error Clearance
  Hari 10: Konsolidasi Slice 6, Debug Clinic & PR Cross-Review Squad (tanpa materi baru)
  Sabtu:   Sprint Review 2 & Retrospektif Tengah Bulan (Target: Validasi & Toast lengkap)

Minggu 3: Cari, Filter, Urutkan, Pagination & URL State (Slice 7)
  Hari 11: 03a Debounce 400ms & Optimasi Input Pencarian (useDebouncedValue + cleanup)
  Hari 12: 03b State di URL (useSearchParams) & Server-side Query + Header X-Total-Count
  Hari 13: 03c Bagian 1: Tipe ProductFilters, fetchPage, API Query Params & reloadToken useProducts
  Hari 14: 03c Bagian 2: Komponen ProductFilters, Pagination & Penggabungan ProductsPage
  Hari 15: 03d Pemantapan Slice 7: Empty State, Reset Filter, Uji Back/Forward & PR Review
  Sabtu:   Sprint Review 3 (Target: Search, Filter, Sort, Pagination tahan F5 & shareable)

Minggu 4: Desain Responsif, Kontrak API Tertulis & Showcase (Slice 8)
  Hari 16: 04a Desain Responsif Mobile-First dengan Tailwind CSS (uji DevTools 375px-768px)
  Hari 17: 04b Slice 8: Audit Endpoint src/api/* & Susun docs/kontrak-api.md + decision-log.md
  Hari 18: 04c Audit Kualitas Kode (oxlint, tsc -b, hapus kode mati) & Konsolidasi Kontrak API Squad
  Hari 19: Pemolesan Akhir, PR Final Repo Pribadi & Finalisasi Slide/Dokumen Kontrak Squad
  Hari 20: Gladi Resik Showcase 5 Menit per Squad & Survei Peminatan Chapter (tanpa materi baru)
  Sabtu:   Sprint Review 4 / Showcase Akhir Bulan 3 (Mini Katalog UMKM v2 + Presentasi Kontrak API)
```

---

## 3. Jebakan Mental Model & Solusi Mentor

| Topik | Kebingungan Peserta | Cara Mentor Meluruskan |
|---|---|---|
| **Custom Hook** | "Kenapa kita bikin file terpisah kalau kodenya cuma dipakai di satu halaman?" | Jelaskan bahwa custom hook bukan cuma soal *reusability* (bisa dipakai ulang), tapi soal **Separation of Concerns**: memisahkan logika data yang rumit agar komponen UI tetap bersih dan mudah dipahami. |
| **Context API** | "Kenapa harus dipisah jadi 3 file (`Context`, `Provider`, `Hook`)? Kenapa gak 1 file aja?" | Buka linter/Vite HMR: tunjukkan bahwa `oxlint` / Vite Fast Refresh akan memberi peringatan jika file komponen mengekspor fungsi biasa. Tunjukkan juga bahwa hook `useToast` memberi pesan error yang jauh lebih ramah pemula jika Provider lupa dipasang. |
| **State di URL** | "Kenapa gak pakai `useState` aja, kan lebih gampang?" | Minta peserta membuka filter tertentu, lalu suruh mereka menekan tombol **F5 (Refresh)**. Begitu filter mereka hilang, mereka akan langsung paham nilai mahal dari URL Search Params. |
| **Dependency Array `useProducts`** | "Kenapa harus `[filters.q, filters.page, ...]` satu-satu? Kenapa gak `[filters]` aja?" | Ajak peserta mengganti ke `[filters]`, lalu buka tab Network. Tunjukkan bagaimana request HTTP terpanggil berulang kali tanpa henti karena referensi objek selalu baru di tiap render. |
| **Kontrak API** | "Ngapain nulis dokumen kontrak API kalau kodenya udah jalan?" | Tegaskan: bulan depan API palsu ini akan diganti server NestJS buatan Chapter Backend sendiri. Jika tidak ada kontrak tertulis yang pasti, aplikasi mereka dijamin akan hancur berantakan saat integrasi. |

---

## 4. Tabel Tugas Mandiri per Sesi & Deliverable Squad

Tugas mandiri dikerjakan individual pada **Blok 3** (estimasi 20-30 menit) di kelas, disimpan di `tugas/tugas_<kode>.md` pada repositori masing-masing, lalu di-review lewat PR menggunakan **Checklist Code Review Dasar**:

| Sesi | Kode Tugas | Judul Tugas / Aktivitas | Estimasi / Jenis |
|---|---|---|---|
| **01a** | `tugas_01a.md` | Eksperimen Varian `Button`, `Input` & `Badge` | 20-30 menit (Individual) |
| **01b** | `tugas_01b.md` | Uji Isolasi Custom Hook `useCategories` & Cleanup `ignore` | 20-30 menit (Individual) |
| **01c** | `tugas_01c.md` | Pembandingan `ProductsPage` Sebelum vs Sesudah `useProducts` | 20-30 menit (Individual) |
| **01d** | `tugas_01d.md` | Terapkan `Badge` & Simulasi *Graceful Degradation* + Misi Squad 1 | 20-30 menit (Individual + Squad) |
| **02a** | `tugas_02a.md` | Pengujian Kasus Tepi Fungsi `validate` & `validateEdit` | 20-30 menit (Individual) |
| **02b** | `tugas_02b.md` | Uji Guard Clause `ToastProvider` & Alur Arsitektur 3 File | 20-30 menit (Individual) |
| **02c** | `tugas_02c.md` | Verifikasi Tab Network Validasi Client-Side & Toast CRUD | 20-30 menit (Individual) |
| **02d** | `tugas_02d.md` | Implementasi Varian Toast & *Real-time Error Clearance* + Misi Squad 2 | 20-30 menit (Individual + Squad) |
| **03a** | `tugas_03a.md` | Observasi Jeda Debounce 400ms vs 1000ms di Network Tab | 20-30 menit (Individual) |
| **03b** | `tugas_03b.md` | Inspeksi Header `X-Total-Count` & Query `URLSearchParams` | 20-30 menit (Individual) |
| **03c** | `tugas_03c.md` | Uji Ketahanan Refresh (F5), `reloadToken`, & Kombinasi Filter *(Hari 1-2)* | 20-30 menit (Individual) |
| **03d** | `tugas_03d.md` | *Empty State*, Tombol Reset Filter & Uji Back/Forward + Misi Squad 3 | 20-30 menit (Individual + Squad) |
| **04a** | `tugas_04a.md` | Audit Layout Mobile-First (320px, 375px, 768px) | 20-30 menit (Individual) |
| **04b** | `tugas_04b.md` | Audit Endpoint `src/api/*` + **Konsensus Squad** `docs/kontrak-api.md` & `decision-log.md` | 20-30 menit (Individual + Squad) |
| **04c** | `tugas_04c.md` | Bukti `oxlint` & `npm run build` + Persiapan Showcase v2 Squad | 20-30 menit (Individual + Squad) |

---

## 5. Checklist Kapabilitas Mingguan & Strategi Pendampingan

Evaluasi tetap tanpa nilai angka akademik, menggunakan observasi **Siap / Hampir Siap / Perlu Pendampingan**:

### Minggu 1 (Tailwind, Component Composition & Custom Hooks — Slice 5)
- [ ] **Siap:** Memahami props union/HTMLAttributes pada `Button`/`Input`/`Badge`, memisahkan fetching ke `useCategories`/`useProducts`, dan meneruskan `categories` ke kartu produk.
- [ ] **Hampir Siap:** Styling sudah rapi tapi masih sering memanggil `fetch` langsung di komponen halaman atau lupa meneruskan `...props`.
- [ ] **Perlu Pendampingan:** Bingung aturan *Top Level* Hooks atau masih menumpuk state `products` & `categories` tanpa pemisahan file.
  - *Aksi Pendampingan:* Pairing 1-on-1 di Blok 2 Hari 5 untuk membedah 1 file hook bersama.

### Minggu 2 (Validasi Form & Context API — Slice 6)
- [ ] **Siap:** Memisahkan validasi ke pure function (`validate`/`validateEdit`), memblokir submit invalid sebelum request API, dan memasang Context 3 file tanpa warning `oxlint`.
- [ ] **Hampir Siap:** Validasi jalan tapi error masih muncul setelah field diperbaiki, atau lupa membungkus `<App />` dengan `<ToastProvider>`.
- [ ] **Perlu Pendampingan:** Masih mengandalkan `required` HTML atau menyatukan Context + Provider dalam 1 file hingga Fast Refresh error.
  - *Aksi Pendampingan:* Simulasi langsung Prop Drilling vs Context di papan tulis pada Blok 2 Hari 10.

### Minggu 3 (Debounce, URL State & Server Query — Slice 7)
- [ ] **Siap:** Mengerti peran cleanup `clearTimeout`, membedakan `urlFilters.q` vs `activeFilters.q`, membaca header `X-Total-Count`, dan menjaga filter tetap utuh saat F5.
- [ ] **Hampir Siap:** Filter dan search jalan, tapi lupa mereset `page: 1` saat filter berganti atau terjadi loop fetch karena dependency array `[filters]`.
- [ ] **Perlu Pendampingan:** Bingung antara state lokal dengan `useSearchParams`, atau aplikasi error saat URL kosong.
  - *Aksi Pendampingan:* Buka tab Network bersama di Blok 2 Hari 14–15 untuk melacak parameter URL dan respons server langkah demi langkah.

### Minggu 4 (Mobile-First, Kontrak API & Showcase — Slice 8)
- [ ] **Siap:** Layout rapi di layar 375px tanpa horizontal scroll, dokumen `docs/kontrak-api.md` akurat sesuai kode `src/api/`, dan lolos `oxlint` + `npm run build` 0 error.
- [ ] **Hampir Siap:** Fitur lengkap di desktop tapi layout filter/pagination berantakan di HP, atau tabel kontrak API masih ada nama field yang salah ketik (`camelCase` vs `snake_case`).
- [ ] **Perlu Pendampingan:** Kesulitan menghubungkan kode frontend dengan dokumentasi endpoint untuk Chapter Backend.
  - *Aksi Pendampingan:* Review bersama per squad di Blok 2 Hari 18–19 sambil membuka `src/api/products.ts` dan `docs/kontrak-api.md` berdampingan.

---

## 6. Checkpoint Keluar Bulan 3

Sebelum meluluskan peserta ke **Bulan 4 (Backend Full-stack Foundations — NestJS & PostgreSQL)**, pastikan setiap peserta mampu:
1. Menjelaskan perbedaan peran `useState`, Custom Hook, Context API, dan URL Search Params dengan bahasa sendiri.
2. Membaca dan menjelaskan isi tabel `docs/kontrak-api.md` (mengapa `POST` butuh payload `CreateProductInput` lengkap, mengapa `GET /products` membaca header `X-Total-Count`).
3. Menjalankan `npm run lint` dan `npm run build` dengan hasil 0 error dan 0 warning.
4. Melakukan **PR Code Review dengan checklist dasar** pada kode rekan satu squad dengan umpan balik yang sopan dan terarah.
5. Mendemokan alur lengkap Mini Katalog UMKM v2 (Cari → Filter → Urutkan → Pagination → Validasi Form → Toast → Responsif HP).
