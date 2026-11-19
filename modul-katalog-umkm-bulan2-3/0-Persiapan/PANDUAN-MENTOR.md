# Panduan Mentor — 0. Persiapan

**Kapan:** Hari pertama Bulan 2 (setelah menyelesaikan Bulan 1 Fondasi Pra-Coding), sebelum Slice 0. Alokasi: 1 hari belajar (250 menit, terbagi dalam ritme harian 3 blok).

---

## Ritme Harian Belajar (Senin - Jumat)

Program berjalan dalam jadwal 250 menit/hari dengan model kerja tim software engineering (tribe/squad):

| Blok | Waktu | Durasi | Format Aktivitas |
|---|---|---|---|
| **Blok 1** | 08.00 - 10.00 | 120 menit | **Standup harian (10-15m):** 3 pertanyaan (apa yang selesai kemarin, kendala apa, apa target hari ini).<br>**Guided Reading / Mini-lesson (maks 25m):** Baca konsep bersama atau mentor jelaskan poin kunci.<br>**Coding Terbimbing:** Mentor live-code langkah kecil, murid langsung menirukan di laptop masing-masing. |
| *Istirahat* | 10.00 - 10.30 | 30 menit | Rehat santai, rileksasi mata dan pikiran. |
| **Blok 2** | 10.30 - 11.20 | 50 menit | **Pairing & Debug Clinic:** Praktik berpasangan (driver/navigator bergantian tiap 25m). **Tanpa materi baru.** Sesi khusus mengurai error instalasi, Git, atau environment. |
| *Istirahat* | 11.20 - 13.00 | 100 menit | Istirahat siang, makan, dan ibadah. |
| **Blok 3** | 13.00 - 14.20 | 80 menit | **Tugas Mandiri (20-30m):** Murid mengerjakan latihan individual di kelas dengan mentor siaga.<br>**PR Code Review & Lightning Demo (50m):** Review PR oleh rekan satu squad/pasangan, lalu demo singkat pencapaian hari ini.<br>*(Catatan Hari Persiapan: karena belum masuk Unit 01a, Blok 3 langsung diisi praktik PR pertama dari `03` dan simulasi format bantuan `04`).* |
| **Malam** | Fleksibel | Bebas | **Tidak ada tugas wajib.** Hanya bacaan santai atau eksplorasi opsional bagi yang berminat. |

### Sabtu: Sprint Review & Retrospektif

- **Sprint Review (09.00 - 10.00):** Demo live tiap squad (**3 squad @ 12-15 menit**: presentasi fitur slice di browser + tab Network API + tanya jawab/review kode singkat).
- **Sprint Retrospektif (10.15 - 11.30):** Evaluasi ritme kerja tim menggunakan papan Mad/Sad/Glad atau I Like/I Wish/What If, lalu susun action item untuk minggu berikutnya. *(Sabtu bebas PR setelah sesi selesai.)*

---

## Model Tim & Kolaborasi

- **Squad Rolling:** **12 murid** dibagi menjadi **3 squad** (masing-masing **4 orang**). Susunan squad diacak ulang secara berkala (tiap 1–2 minggu) agar murid terbiasa bekerja dengan berbagai rekan kerja.
- **Kepemilikan Repo vs Squad:** Pada Bulan 2–3, setiap murid bekerja di repositori latihan fork/clone miliknya sendiri agar semua berlatih end-to-end, sementara **squad** berfungsi sebagai grup pairing harian, review PR wajib, dan panggung demo Sprint Review.
- **Pairing (Driver & Navigator):** Saat Blok 2, satu orang mengetik (*driver*) dan rekan pasangannya membaca instruksi serta mengecek typo (*navigator*). Tukar peran setiap 25 menit.
- **Tanpa Nilai Angka:** Evaluasi sepenuhnya berbasis **Checklist Kapabilitas** (status: *Siap*, *Hampir Siap*, atau *Perlu Pendampingan*), kualitas PR/code review, dan keaktifan saat demo.

---

## Urutan Mengajar Bab Persiapan

1. **`01-tentang-modul-ini.md` (Blok 1 awal):** Jelaskan cara belajar *Product-Driven*: produk hidup lewat irisan kecil (*slice*), dan sambungkan dengan artefak **Bulan 1** (Wireframe Figma `03b` serta backlog `03e`). Tegaskan batas *scope* Bulan 2–3 fokus pada **Must-Have** (Katalog & Kelola Produk) sebelum fitur *Could-Have* (WAHA, Chatbot, Ekspedisi) masuk pasca-Bulan 4.
2. **`02-setup-starter.md` (Blok 1 sisa & Blok 2):** Pastikan **SEMUA 12 murid** sukses menjalankan `npm run dev` sebelum lanjut. Ini titik paling sering macet.
3. **`03-alur-git-dan-pr.md` (Blok 3 awal):** Praktikkan langsung alur branch → commit deskriptif (`feat:`/`docs:`) → push → buat PR di GitHub → cek manual `npm run lint` & `npm run build` → code review oleh rekan satu squad → merge oleh pembuat PR.
4. **`04-format-minta-bantuan.md` (Blok 3 akhir):** Simulasikan menulis format 4 poin minta bantuan dan tempel panduannya di papan pengumuman kelas.

---

## Catatan Kritis Lingkungan Kerja & Tooling

### 1. Kunci Versi `json-server` (0.17.x)
Starter repo menggunakan `"json-server": "0.17.4"`. **JANGAN di-upgrade ke versi 1.x.**
- Versi 1.x mengubah perilaku query parameter (`_limit`, `_sort`, `_order`) dan menghilangkan header pagination `X-Total-Count` yang menjadi fondasi materi di Bulan 2 dan 3.
- Pastikan murid tidak sengaja menjalankan `npm install json-server@latest`.

### 2. Versi Node.js (Kompatibel Vite 8)
- Starter teruji di **Node.js 22 LTS** dan menggunakan Vite 8 (`engines.node`: **`^20.19.0` atau `>=22.12.0`**).
- Jika ada murid dengan Node `< 20.19` atau versi ganjil yang gagal menjalankan Vite, segera bantu instalasi **Node 22 LTS** lewat `nvm`/`fnm` di Blok 2 (Debug Clinic).

### 3. Skrip Menjalankan Dev Server & Kualitas Kode
- Ingatkan murid untuk mengetik `npm run dev` (menjalankan web Vite di port `5173` dan mock API `json-server` di port `3001` secara bersamaan melalui `concurrently`).
- Jika murid hanya menjalankan `npm run dev:web`, API palsu tidak aktif dan `fetch` akan gagal.
- Kenalkan juga `npm run lint` (`oxlint`) dan `npm run build` (`tsc -b && vite build`) sejak Hari 0 karena starter belum memakai CI otomatis di GitHub.

---

## Checklist Kesiapan Masuk Slice 0

| Indikator Kapabilitas | Siap | Hampir Siap | Perlu Pendampingan |
|---|---|---|---|
| Starter repo jalan lancar di laptop (`http://localhost:5173` tampil). | Tampil tanpa kendala. | Perlu 1x bantuan restart terminal. | Node/npm error dan belum jalan mandiri. |
| Mock API aktif (`http://localhost:3001/products` mengembalikan data JSON). | Bisa cek mandiri di tab browser. | Perlu diingatkan port 3001. | Dev server API tidak nyala. |
| Mampu membuat branch baru dan membuka PR di GitHub. | Buat branch, cek lint/build, & buka PR mandiri. | Masih bingung memilih target branch atau lupa cek lint. | Masih push langsung ke branch `main`. |
| Mengetahui format 4 poin minta bantuan saat stuck. | Menulis format bantuan lengkap. | Menjelaskan secara lisan saja. | Langsung memanggil mentor tanpa info error. |

**Strategi Pendampingan:**
- Murid dengan status *Perlu Pendampingan* dipasangkan dengan rekan yang sudah *Siap* pada Blok 2 hari berikutnya.
- Mentor mendampingi langsung setup terminal dan Git environment sebelum memulai `01a`.
