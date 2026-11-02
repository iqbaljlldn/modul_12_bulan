# Panduan Mentor — 1. TypeScript & React Dasar (Bulan 2)

**Peserta:** 18 orang, dibagi menjadi 6 squad rolling (masing-masing 3 orang).  
**Durasi:** 4 minggu (20 hari belajar efektif + 4 Sabtu Sprint Review).  
**Rasio Waktu:** 30% konsep/mini-lesson : 70% praktik langsung dan coding terbimbing.

---

## 1. Ritme Harian Belajar (Senin - Jumat)

Jadwal harian residensial berdurasi 250 menit dibagi menjadi 3 blok terstruktur:

| Blok | Waktu | Durasi | Format Aktivitas Mentor & Murid |
|---|---|---|---|
| **Blok 1** | 08.00 - 10.00 | 120 menit | **Standup Harian (10-15m):** Tiap murid menyampaikan progres kemarin, rencana hari ini, dan kendala/blocker.<br>**Guided Reading / Mini-lesson (maks 25m):** Mentor memandu membaca bagian penting bersama di kelas (jangan jadikan bacaan rumah syarat mutlak) atau menjelaskan konsep lewat analogi sehari-hari.<br>**Coding Terbimbing:** Mentor mendemokan langkah kecil secara live di layar proyektor, lalu murid mengetik dan memverifikasi di laptop masing-masing langkah demi langkah. |
| *Istirahat* | 10.00 - 10.30 | 30 menit | Istirahat penyegaran, camilan, dan rileksasi mata. |
| **Blok 2** | 10.30 - 11.20 | 50 menit | **Pairing & Debug Clinic (Tanpa Materi Baru):** Murid berpasangan (driver mengetik, navigator menyimak, tukar peran tiap 25m). Mentor berkeliling membantu murid yang mengalami error TypeScript/Vite/Git. Fokus menuntaskan rintangan teknis. |
| *Istirahat* | 11.20 - 13.00 | 100 menit | Istirahat siang, makan, ibadah, dan rehat. |
| **Blok 3** | 13.00 - 14.20 | 80 menit | **Tugas Mandiri (20-30m):** Dikerjakan individual di kelas dalam folder repo squad (`tugas_<kode>.md`), mentor siaga menjawab pertanyaan.<br>**PR Code Review & Lightning Demo (50m):** Murid membuka PR di repo squad, melakukan review silang antar rekan, dan 1-2 squad mendemokan hasil kodenya. |
| **Malam** | Fleksibel | Bebas | **Tidak ada tugas wajib.** Bootcamp residensial menjaga ritme istirahat murid. Hanya bahan bacaan pengantar santai atau latihan stretch opsional bagi yang berminat. |

### Sabtu: Sprint Review & Retrospektif Mingguan

- **Sprint Review (09.00 - 10.30):** Demo live tiap squad (6 squad @10-12 menit). Murid mendemokan fitur slice yang berjalan di browser, tab Network saat memanggil API, dan menjelaskan potongan kodenya.
- **Sprint Retrospektif (10.45 - 12.00):** Evaluasi ritme kerja tim menggunakan papan **Mad / Sad / Glad** atau **I Like / I Wish / What If**. Mentor memfasilitasi tanpa menghakimi, menyepakati perbaikan kerja sama untuk minggu berikutnya.

---

## 2. Peta Sesi 4 Minggu (5 Hari Belajar + Sabtu Review)

Setiap minggu dipetakan secara realistis untuk pemula (unit padat dipecah 2 hari, bukan dipadatkan):

```
Minggu 1: Orientasi React & Slice 0 (Tipe Dasar & List Rendering)
  Hari 1: 01a Orientasi React (Mental model SPA, Vite vs CRA, kenalan struktur folder)
  Hari 2: 01b JSX & Komponen Bertipe (Props bertipe TypeScript sederhana, ProductCard awal)
  Hari 3: 01c Styling Kartu Produk (CSS classes terisolasi, grid layout responsif)
  Hari 4: 01d Slice 0: List Rendering Data Statis (Interface Product, map, key)
  Hari 5: Konsolidasi Slice 0, Branching, PR Pertama & Code Review Bersama
  Sabtu:  Sprint Review 1 & Retrospektif (Target: Slice 0 jalan & PR dimerge)

Minggu 2: State, Lifecycle, Fetch & Form (Slice 1-2)
  Hari 6: 02a State & useState (Mental model whiteboard vs kertas tisu, immutability)
  Hari 7: 02b useEffect & Lifecycle (Side effect, pelayan restoran, dependency array, cleanup)
  Hari 8: 02c Slice 1: Fetch API, Loading & Error State (Komunikasi dengan mock API)
  Hari 9: 02d Event Handling & Controlled Form (Setir mobil vs autopilot, preventDefault)
  Hari 10: 02e Slice 2: Form Tambah Produk (POST ke json-server, state form terpisah)
  Sabtu:  Sprint Review 2 & Retrospektif (Target: Slice 1 & 2 jalan tanpa reload)

Minggu 3: CRUD Lengkap & Pola Data (Slice 3 Dipecah 2 Hari)
  Hari 11: 03a HTTP Methods & API Patterns (DELETE, PATCH, status codes, tiket tilang ApiError)
  Hari 12: 03b Bagian 1: Slice 3 - Hapus Produk, 204 No Content, & Penanganan Error
  Hari 13: 03b Bagian 2: Slice 3 - Edit Produk Inline (ProductEditForm, isEditing lokal, Partial)
  Hari 14: 03c State Management Patterns (Lifting state ke parent, papan kulkas, alur data searah)
  Hari 15: Konsolidasi Slice 3, Debug Clinic, & PR Review CRUD Lengkap
  Sabtu:  Sprint Review 3 & Retrospektif (Target: Slice 3 CRUD selesai & teruji)

Minggu 4: Routing, Konsolidasi & Showcase Akhir Bulan 2 (Slice 4)
  Hari 16: 04a React Router Dasar (Switchboard resepsionis, BrowserRouter, Link vs a, useParams)
  Hari 17: 04b Slice 4: Halaman Detail Produk & Navigasi Antar Halaman
  Hari 18: 04b Lanjutan: Penanganan Detail 404 & Loading State Halaman
  Hari 19: 04c Konsolidasi, Refactor, & Code Audit (Oxlint, hapus kode mati, konsistensi nama)
  Hari 20: Gladi Resik & Persiapan Showcase Akhir Bulan 2
  Sabtu:  Sprint Review 4 / Showcase Akhir Bulan 2 & Evaluasi Capaian
```

---

## 3. Strategi Mengajar Pemula & Mengurangi Beban Kognitif

1. **Kenalkan TypeScript Bertahap:**
   - **Minggu 1:** Tipe primitif (`string`, `number`, `boolean`), array (`Product[]`), dan `interface` sederhana. Hindari istilah teoritis berat.
   - **Minggu 2:** Tipe state (`useState<Product[]>`), event type (`ChangeEvent`, `FormEvent`). Jangan langsung memperkenalkan utility type yang rumit.
   - **Minggu 3:** Tulis tipe input secara eksplisit dulu (`CreateProductInput`, `UpdateProductInput`), baru kenalkan `Omit` atau `Partial` sebagai alternatif cerdas opsional.
   - **Minggu 3-4:** Class `ApiError` diperkenalkan dengan analogi kartu laporan/tiket tilang, bukan teori Object-Oriented yang rumit.

2. **Gunakan Analogi Sehari-hari:**
   - *State:* Papan tulis kecil di meja kasir yang bisa dihapus dan ditulis ulang tanpa membuang mejanya.
   - *Props:* Surat pengantar atau dokumen data yang dikirim dari kantor pusat (induk) ke kantor cabang (anak).
   - *Hook (`use...`):* Kotak perkakas khusus yang dipinjam komponen dari gudang React untuk menjalankan fungsi tertentu.
   - *useEffect:* Tugas tambahan pelayan restoran setelah meja ditata rapi ("setelah meja siap, tolong ambil pesanan dari dapur").
   - *Controlled Component:* Setir mobil di tangan sopir (React yang mengendalikan isi kotak input setiap ketikan).
   - *React Router:* Switchboard resepsionis lobi yang mengarahkan tamu ke kamar yang tepat tanpa membangun ulang gedung.
   - *`<Link>` vs `<a>`:* Tombol lift di dalam gedung vs keluar pintu pagar lalu masuk lagi dari depan.

3. **Cegah Copy-Paste Tanpa Paham:**
   - Bagian modul sengaja menyediakan kerangka kode bertanda `// TODO:` yang harus dilengkapi murid.
   - Mentor wajib memverifikasi bahwa murid memahami baris yang mereka tulis lewat pertanyaan prediksi output atau tebak bug.

4. **Kunci Versi Tooling:**
   - Pastikan starter repo mengunci `"json-server": "0.17.4"`.
   - Versi 1.x memecah fungsionalitas `_limit`, `_sort`, `_order`, dan header `X-Total-Count`.

---

## 4. Tabel Tugas Mandiri per Sesi

Semua tugas dikerjakan individual pada **Blok 3** (20-30 menit) di kelas, disimpan di `tugas/squad-<no>/<nama-murid>/tugas_<kode>.md`:

| Sesi | Kode Tugas | Judul Tugas Mandiri | Estimasi |
|---|---|---|---|
| **01a** | `tugas_01a.md` | Analisis Struktur Starter & Eksplorasi SPA | 20 menit |
| **01b** | `tugas_01b.md` | Pembuatan Komponen Bertipe Tambahan `ProductBadge` | 25 menit |
| **01c** | `tugas_01c.md` | Styling Status Kartu & Indikator Stok Kritis | 25 menit |
| **01d** | `tugas_01d.md` | Ekstensi Tipe `Product` & Pemetaan List Bersyarat | 25 menit |
| **02a** | `tugas_02a.md` | Logika Immutability Array & Counter Sederhana | 25 menit |
| **02b** | `tugas_02b.md` | Sinkronisasi Document Title & Cleanup Timer | 25 menit |
| **02c** | `tugas_02c.md` | Penanganan Error Network & Variabel Ignore Fetch | 30 menit |
| **02d** | `tugas_02d.md` | Form Multi-Input dengan Satu Handler Dinamis | 25 menit |
| **02e** | `tugas_02e.md` | Form Input Produk Baru dengan Validasi Tipe Data | 30 menit |
| **03a** | `tugas_03a.md` | Analisis Status Code & Fungsi API Client PATCH/DELETE | 20 menit |
| **03b** | `tugas_03b.md` | Isolasi State Edit Inline & Proteksi Hapus Data | 30 menit |
| **03c** | `tugas_03c.md` | Pemetaan Diagram Alur Data & Lifting State | 25 menit |
| **04a** | `tugas_04a.md` | Pembuatan Rute Statis & Navigasi SPA dengan Link | 25 menit |
| **04b** | `tugas_04b.md` | Penanganan Khusus Status 404 pada Halaman Detail | 25 menit |
| **04c** | `tugas_04c.md` | Audit Linter oxlint & Refactoring Kode Bersih | 30 menit |

---

## 5. Checklist Kapabilitas Mingguan & Strategi Pendampingan

Evaluasi dilakukan tanpa nilai angka melalui observasi berkala pada akhir tiap minggu:

### Minggu 1 (Orientasi & Slice 0)
- [ ] **Siap:** Mampu membuat komponen fungsional dengan props bertipe `interface`, melakukan list rendering dengan `.map()`, dan menyertakan `key` yang unik tanpa error linter.
- [ ] **Hampir Siap:** Mampu membuat komponen tapi masih sering lupa mengetik tipe props atau lupa menambahkan `key` pada list.
- [ ] **Perlu Pendampingan:** Belum paham alur JSX dan bingung membedakan sintaks HTML biasa dengan React.
  - *Aksi Pendampingan:* Pairing intensif 1-on-1 di Blok 2 Hari 5. Minta murid mendemokan pembuatan kartu sederhana dari nol dengan panduan mentor.

### Minggu 2 (State, Lifecycle, Fetch, Form — Slice 1 & 2)
- [ ] **Siap:** Menggunakan `useState` dengan update immutable, memanggil API dengan `useEffect` lengkap dengan state loading/error, dan membuat form controlled multi-input.
- [ ] **Hampir Siap:** Paham `useState` untuk nilai primitif, tapi masih melakukan mutasi langsung pada array/objek state, atau lupa menambahkan dependency array di `useEffect`.
- [ ] **Perlu Pendampingan:** Tidak memahami siklus render, fetch dilakukan berulang tanpa henti (*infinite loop*), form tidak bisa diketik karena state salah pasang.
  - *Aksi Pendampingan:* Berikan tugas remedial kecil di Blok 2: membuat tombol toggle sederhana dan counter array sebelum menyentuh API.

### Minggu 3 (CRUD Lengkap — Slice 3)
- [ ] **Siap:** Membedakan kapan state ditaruh di lokal (`isEditing`) vs di parent (`products`), mengimplementasikan update immutable (`map`/`filter`), dan menangani error status code via `ApiError`.
- [ ] **Hampir Siap:** Operasi edit/hapus berhasil di server tapi UI belum sinkron tanpa reload manual, atau form edit membuka di semua kartu sekaligus.
- [ ] **Perlu Pendampingan:** Kesulitan membaca error TypeScript pada utility type, alur data antar komponen membingungkan.
  - *Aksi Pendampingan:* Gambar alur data bersama di papan tulis pada Blok 2 Hari 14 dan lakukan live refactoring bersama pasangan pairing.

### Minggu 4 (Routing, Konsolidasi, & Showcase — Slice 4)
- [ ] **Siap:** Mengatur `BrowserRouter`, menggunakan `<Link>` untuk navigasi SPA, membaca parameter `:id` via `useParams`, dan menangani status 404 dengan pesan informatif.
- [ ] **Hampir Siap:** Routing berjalan, tapi masih menggunakan `<a href>` di beberapa tempat atau lupa mengonversi `id` dari string ke number.
- [ ] **Perlu Pendampingan:** Aplikasi error saat navigasi langsung lewat address bar, tidak paham kenapa halaman detail blank saat produk tidak ditemukan.
  - *Aksi Pendampingan:* Simulasi live debugging halaman detail bersama mentor di Blok 2 Hari 18.

---

## 6. Checkpoint Keluar Bulan 2 (Kesiapan Melangkah ke Bulan 3)

Sebelum melanjutkan ke Bulan 3 (`2-React-Lanjutan`), pastikan murid memiliki profil kapabilitas berikut:

| Kriteria Kapabilitas Utama | Bukti Nyata yang Diperiksa |
|---|---|
| **Alur Kolaborasi Git & PR** | Murid dapat membuat branch fitur, commit dengan pesan jelas, membuka PR, membaca komentar review, dan merge mandiri. |
| **Mental Model Komponen & Props** | Mampu menjelaskan perbedaan data yang datang dari luar (props) dengan data internal yang bisa berubah (state) dengan bahasa sendiri. |
| **Siklus Asinkron API & Feedback Pengguna** | Kode aplikasi selalu menangani minimal 3 fase data: loading, error (termasuk status 404), dan data berhasil tampil. |
| **Integritas CRUD di UI & Server** | Dapat mendemokan live: tambah produk baru, edit harga/stok inline, dan hapus produk tanpa memerlukan refresh halaman penuh. |
| **Navigasi Berbasis URL (SPA)** | Pengguna dapat membuka halaman detail produk tertentu via tautan atau reload URL langsung tanpa kehilangan konteks data. |

> Jika ada murid yang masih berstatus *Perlu Pendampingan* pada 2 atau lebih kriteria di atas saat showcase akhir Bulan 2, jadwalkan program pairing terarah pada 2 hari pertama Bulan 3 tanpa memberikan tekanan nilai akademik.
