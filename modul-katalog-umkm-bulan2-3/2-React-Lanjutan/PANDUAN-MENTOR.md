# Panduan Mentor — 2. React Lanjutan (Bulan 3)

**Durasi:** 4 minggu (Slice 5-8).  
**Struktur Pembelajaran:** 4 minggu, 3-4 unit belajar per minggu (total 15 unit terstruktur).  
**Tujuan Utama:** Membawa peserta dari membuat komponen dasar ke arsitektur frontend profesional: styling utility-first (Tailwind v4), component composition, custom hooks, validasi form murni, Context API, state di URL via search params, debounce, dan penulisan kontrak API teknis tertulis untuk Chapter Backend di Bulan 4.

---

## Keputusan Penting Sebelum Minggu 1

> **Standar Styling Tribe: Tailwind CSS v4 vs CSS Module?**  
> Modul ini disusun menggunakan **Tailwind CSS v4** dengan plugin `@tailwindcss/vite`.  
> Jika tribe kamu memutuskan memilih CSS Module, konsep arsitektur (*component composition*, *custom hook*, *context*, *url state*) tetap 100% sama — kamu hanya perlu menyesuaikan contoh kode styling di unit `01a`. Putuskan ini **sebelum hari pertama Minggu 1** dan catat di `docs/decision-log.md`.

---

## Peta Sesi Mingguan & Alokasi Waktu

### Minggu 1 — Kategori, Tailwind CSS & Custom Hook (Slice 5)
*Target Capaian: Katalog UMKM berganti styling ke Tailwind, memiliki komponen reusable atomik, relasi data kategori, dan logika produk diekstrak ke `useProducts`.*

- **Sesi 1 (Unit `01a`):** *Styling Standar Tribe & Komponen UI Atomik*
  - **Mini-lesson (25 menit):** Mengapa utility-first? Menyiapkan `@tailwindcss/vite` dan reset `src/index.css`. Bedah pola `Button.tsx` (`HTMLAttributes`, variants, rest/spread `...props`).
  - **Kerja Mandiri / Pairing:** Peserta membuat `Button.tsx`, `Input.tsx`, dan `Badge.tsx`.
  - **Jebakan:** Peserta pemula sering syok melihat deretan class Tailwind yang panjang di JSX. Tenangkan mereka: jelaskan bahwa dengan membungkusnya di komponen atomik (`Button`), class panjang tersebut hanya ditulis satu kali.
- **Sesi 2 (Unit `01b`):** *Konsep, Aturan, dan Pola Custom Hook*
  - **Mini-lesson (20 menit):** Apa itu custom hook? Mengapa bukan fungsi biasa? Rules of hooks (top-level only). Menulis `useCategories.ts` dengan pola flag `ignore` untuk mencegah memory leak.
  - **Kerja Mandiri / Pairing:** Membuat `src/types/category.ts`, `src/api/categories.ts`, dan `src/hooks/useCategories.ts`.
- **Sesi 3 (Unit `01c`):** *Slice 5 — Implementasi Penuh Kategori & useProducts*
  - **Mini-lesson (20 menit):** Membedah ekstraksi `useProducts.ts`. Menunjukkan kontras `ProductsPage.tsx` sebelum vs sesudah refaktor (file menjadi sangat ramping!). Menghubungkan dropdown kategori di form dan badge di kartu.
  - **Kerja Mandiri / Pairing:** Menerapkan `useProducts`, memperbarui `ProductForm` & `ProductCard`. PR + Code Review Slice 5.
- **Sesi 4 (Unit `01d`):** *Latihan Pemantapan Slice 5 & Uji Ketahanan API*
  - **Aktivitas:** Uji graceful degradation (matikan endpoint `/categories`, pastikan halaman produk tidak crash). Saling review PR pasangan.

---

### Minggu 2 — Validasi Form & Notifikasi Global Context (Slice 6)
*Target Capaian: Form memiliki validasi murni yang memblokir submit jika data salah, menampilkan error visual yang rapi dan aksesibel, serta memiliki sistem notifikasi mengambang (toast) berbasis Context API.*

- **Sesi 1 (Unit `02a`):** *Validasi Form & Arsitektur Input Terkendali*
  - **Mini-lesson (25 menit):** Mengapa validasi bawaan HTML `required` tidak memadai? Membuat fungsi murni `validate(values)` di `src/utils/validate.ts`. Membedah tipe `FormErrors` opsional (`?`) dan integrasi `aria-invalid` di `Input.tsx`.
  - **Kerja Mandiri / Pairing:** Peserta menulis `validate.ts` dan menguji berbagai kondisi input.
- **Sesi 2 (Unit `02b`):** *Context API & Global Toast Notification*
  - **Mini-lesson (30 menit):** Masalah Prop Drilling. Menjelaskan konsep Provider-Consumer. **Mengapa dipecah 3 file?** Jelaskan aturan Vite Fast Refresh (HMR tidak boleh mencampur komponen JSX dengan fungsi biasa). Memasang Provider di `main.tsx`.
  - **Kerja Mandiri / Pairing:** Membuat `ToastContext.ts`, `ToastProvider.tsx`, dan `useToast.ts`.
- **Sesi 3 (Unit `02c`):** *Slice 6 — Implementasi Penuh Validasi & Context*
  - **Mini-lesson (15 menit):** Menghubungkan `validate()` sebelum `onSubmit`. Memanggil `showToast()` saat produk berhasil ditambah, diedit, atau dihapus.
  - **Kerja Mandiri / Pairing:** Menghubungkan ke `ProductForm.tsx`, `ProductEditForm.tsx`, dan `ProductsPage.tsx`. PR + Code Review Slice 6.
- **Sesi 4 (Unit `02d`):** *Latihan Pemantapan Slice 6 & Retro Sprint*
  - **Aktivitas:** Menambahkan varian warna toast (`success`, `error`, `info`) dan real-time error clearance saat user mulai mengetik. **Retro sprint tengah bulan**.

---

### Minggu 3 — Cari, Filter, Urutkan, Pagination & URL State (Slice 7)
*Target Capaian: Pengguna dapat mencari nama produk, memilih kategori, mengurutkan harga/tanggal, dan berpindah halaman secara efisien lewat query API server-side, dengan seluruh kondisi tersimpan di URL via `useSearchParams`.*

- **Sesi 1 (Unit `03a`):** *Debounce & Optimasi Input Pencarian*
  - **Mini-lesson (25 menit):** Bahaya live search tanpa debounce: pemborosan request dan race condition latensi jaringan. Membedah siklus `setTimeout` + `clearTimeout` di dalam cleanup `useEffect`. Membedakan `urlFilters.q` (instan di UI) vs `activeFilters.q` (debounced ke API).
  - **Kerja Mandiri / Pairing:** Membangun `src/hooks/useDebouncedValue.ts`.
- **Sesi 2 (Unit `03b`):** *State di URL (`useSearchParams`) & Server Query*
  - **Mini-lesson (25 menit):** Mengapa URL adalah Single Source of Truth? Keunggulan shareable links, refresh safety, dan navigasi browser. Membaca header `X-Total-Count` via `fetchPage<T>`. Menghitung `totalPages`.
  - **Kerja Mandiri / Pairing:** Memperbarui `src/api/http.ts` dan `src/api/products.ts` dengan `URLSearchParams`.
- **Sesi 3 (Unit `03c`):** *Slice 7 — Implementasi Penuh Cari, Filter, Urutkan & Pagination*
  - **Mini-lesson (25 menit):** Membedah `reloadToken` di `useProducts`. Mengapa dependency array `useEffect` harus field per field (`filters.q`, `filters.categoryId`, dst) dan **bukan** objek `filters` utuh. Membangun `ProductFilters.tsx` dan `Pagination.tsx`.
  - **Kerja Mandiri / Pairing:** Menggabungkan seluruh alur di `ProductsPage.tsx`. PR + Code Review Slice 7.
- **Sesi 4 (Unit `03d`):** *Latihan Pemantapan Slice 7 & Penanganan Edge Cases*
  - **Aktivitas:** Menguji tombol back/forward browser. Membuat tampilan hasil pencarian kosong (*empty state*) dan tombol "Reset Semua Filter".

---

### Minggu 4 — Desain Responsif, Kontrak API Tertulis & Showcase (Slice 8)
*Target Capaian: Aplikasi teruji responsif di layar smartphone UMKM, dokumentasi teknis `docs/kontrak-api.md` tuntas ditulis sebagai spesifikasi untuk backend NestJS, kode bersih dari warning, dan showcase Mini Katalog UMKM v2 berhasil didemokan.*

- **Sesi 1 (Unit `04a`):** *Desain Responsif & Layout Mobile dengan Tailwind*
  - **Mini-lesson (20 menit):** Realitas pelaku UMKM Indonesia (85%+ smartphone). Pendekatan Mobile-First di Tailwind (`sm:`, `md:`, `lg:`). Menyesuaikan grid kartu produk, tata letak filter, dan ukuran touch target tombol.
  - **Kerja Mandiri / Pairing:** Menguji dan merapikan layout menggunakan DevTools Device Mode (iPhone SE 375px, Pixel 7, iPad).
- **Sesi 2 (Unit `04b`):** *Slice 8 — Konsolidasi & Kontrak API Tertulis*
  - **Mini-lesson (30 menit):** Mengapa Kontrak API adalah dokumen terpenting penghubung Frontend dan Backend? Mengaudit seluruh endpoint di `src/api/`. Mengisi `docs/kontrak-api.md`. Mendokumentasikan perbedaan krusial `json-server` vs NestJS (relasi kategori, validasi DTO server-side, header pagination).
  - **Kerja Mandiri / Pairing:** Melengkapi `docs/kontrak-api.md` dan `docs/decision-log.md`.
- **Sesi 3 (Unit `04c`):** *Audit Kualitas Kode (Linting & Build Verification)*
  - **Aktivitas:** Menjalankan `npm run lint` (`oxlint`) dan `npm run build` (`tsc -b && vite build`). Membersihkan kode mati, console log, dan import yang tidak terpakai. Gladi resik demo 5 menit.
- **Sesi 4:** *Showcase Mini Katalog UMKM v2 & Survei Minat Chapter*
  - **Aktivitas:** Presentasi produk 5 menit per squad di depan seluruh tribe. Menunjukkan fitur lengkap dan dokumen Kontrak API ke calon Chapter Backend. Pengisian survei peminatan peran (Frontend, Backend, DevOps/QA).

---

## Jebakan Mental Model & Solusi Mentor

| Topik | Kebingungan Peserta | Cara Mentor Meluruskan |
|---|---|---|
| **Custom Hook** | "Kenapa kita bikin file terpisah kalau kodenya cuma dipakai di satu halaman?" | Jelaskan bahwa custom hook bukan cuma soal *reusability* (bisa dipakai ulang), tapi soal **Separation of Concerns**: memisahkan logika data yang rumit agar komponen UI tetap bersih dan mudah dipahami. |
| **Context API** | "Kenapa harus dipisah jadi 3 file (`Context`, `Provider`, `Hook`)? Kenapa gak 1 file aja?" | Buka linter/Vite HMR: tunjukkan bahwa Vite Fast Refresh akan kehilangan state jika file komponen mengekspor fungsi biasa. Tunjukkan juga bahwa hook `useToast` memberi pesan error yang jauh lebih ramah pemula jika Provider lupa dipasang. |
| **State di URL** | "Kenapa gak pakai `useState` aja, kan lebih gampang?" | Minta peserta membuka filter tertentu, lalu suruh mereka menekan tombol **F5 (Refresh)**. Begitu filter mereka hilang, mereka akan langsung paham nilai mahal dari URL Search Params. |
| **Dependency Array `useProducts`** | "Kenapa harus `[filters.q, filters.page, ...]` satu-satu? Kenapa gak `[filters]` aja?" | Ajak peserta mengganti ke `[filters]`, lalu buka tab Network. Tunjukkan bagaimana request HTTP terpanggil berulang kali tanpa henti karena referensi objek selalu baru di tiap render. |
| **Kontrak API** | "Ngapain nulis dokumen kontrak API kalau kodenya udah jalan?" | Tegaskan: bulan depan API palsu ini akan diganti server NestJS buatan temanmu sendiri. Jika tidak ada kontrak tertulis yang pasti, aplikasi mereka dijamin akan hancur berantakan saat integrasi. |

---

## Checkpoint Keluar Bulan 3

Sebelum meluluskan peserta ke Bulan 4 (Backend Full-stack Foundations), pastikan setiap peserta mampu:
1. Menjelaskan perbedaan peran `useState`, Custom Hook, Context API, dan URL Search Params dengan kata-kata sendiri.
2. Membaca dan menjelaskan isi tabel `docs/kontrak-api.md` (mengapa method POST membutuhkan body, mengapa GET /products membaca header `X-Total-Count`).
3. Menjalankan `npm run lint` dan `npm run build` dengan hasil 0 error.
4. Mendemokan alur lengkap Katalog UMKM v2 (Cari → Filter → Urutkan → Pagination → Validasi Form → Toast → Responsif HP).
