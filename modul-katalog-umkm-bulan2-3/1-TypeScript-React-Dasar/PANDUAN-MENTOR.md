# Panduan Mentor — 1. TypeScript & React Dasar (Bulan 2)

**Peserta:** 18 orang, 6 squad rolling @3. **Durasi:** 4 minggu (~15 unit belajar, ±16 sesi). Rasio 30% teori : 70% praktik — mini-lesson tidak lebih dari 20-30 menit per sesi.

## Perubahan dari versi sebelumnya

Modul Bulan 2 diperluas dari 5 file (1 per slice) menjadi **15 unit belajar**. Materi baru bukan isi baru — melainkan **pengantar konsep** dari modul React bootcamp yang ditarik dan diringkas sebelum tiap slice, supaya peserta tidak "loncat" langsung ke slice tanpa pondasi.

**Aturan bacaan wajib:** tiap unit punya referensi ke bab spesifik di modul React bootcamp. Peserta diminta membaca **sebelum** sesi. Mini-lesson menjembatani ke kasus Katalog, bukan mengulang seluruh bab.

## Ritme mingguan

| Minggu | Sesi | Unit | Aktivitas |
|---|---|---|---|
| 1 | 4 sesi | 01a → 01d | Orientasi React + Slice 0. PR pertama, review pertama. Evaluasi mini di akhir minggu. |
| 2 | 5 sesi | 02a → 02e | State/useEffect/fetch/form + Slice 1-2. Debug clinic di tengah minggu. Task breakdown pertama di board. |
| 3 | 4 sesi | 03a → 03c | CRUD lengkap + Slice 3 (bisa 2 sesi). Retro pertama di akhir minggu. |
| 4 | 4 sesi | 04a → 04c + showcase | Routing + konsolidasi + showcase akhir bulan. |

## Sebelum mengajar tiap unit

1. Jalankan sendiri langkahnya di starter (`katalog-umkm-starter`), pastikan versi Node/dependency di laptopmu sama dengan starter.
2. Simpan kode solusi (`katalog-umkm-solusi` — kunci jawaban, JANGAN dibagikan ke peserta) untuk kalau ada yang macet parah.
3. Cek **bacaan wajib** di unit itu — pastikan kamu sudah baca bab yang sama di modul React bootcamp.
4. Mini-lesson: buka dengan **Why**, tunjukkan **Concept** singkat, sisanya biarkan peserta praktik sendiri/berpasangan.

## Jebakan spesifik per unit

### Minggu 1
- **01a (Orientasi):** sesi ini jangan terlalu lama — 30-45 menit cukup. Tujuannya peserta bisa jalankan starter dan paham folder structure, bukan kuliah teori React.
- **01b (JSX & Komponen):** peserta sering bingung `interface` vs `type` — jangan dijadikan drama, cukup bilang "di modul ini begini" dan lanjut.
- **01c (Styling):** jangan habiskan waktu di CSS yang sempurna. Cukup supaya kartu layak dilihat. Keputusan standar styling tribe baru di Bulan 3.
- **01d (Slice 0):** kalau peserta sudah solid di 01a-01c, slice ini bisa cepat. Kalau belum, ini sesi konsolidasi.

### Minggu 2
- **02a (useState):** latihan counter/toggle WAJIB dilakukan dulu sebelum lanjut. Kalau `useState` belum klik, semua slice setelahnya akan berat.
- **02b (useEffect):** ini bab paling "loncatan" buat yang pre-class-nya kurang lancar di `async/await`. Siapkan sesi tambahan kecil kalau perlu.
- **02c (Slice 1):** pastikan peserta buka DevTools Network saat fetch — ini kebiasaan yang harus terbentuk di sini.
- **02d (Event & Form):** latihan form kecil (input + preview) sebelum masuk Slice 2 sangat membantu.
- **02e (Slice 2):** form controlled dengan satu `handleChange` sering butuh dijelaskan 2 kali. Gambar di papan tulis: `event.target.name` → key di objek state.

### Minggu 3
- **03a (HTTP Methods):** sesi ini lebih "teori" — peserta menulis fungsi API tapi belum pakai di UI. Cukup singkat.
- **03b (Slice 3):** ini unit terpadat (custom error class + PATCH + DELETE + state lokal edit). **Pertimbangkan dipecah 2 sesi** kalau squad terasa kewalahan.
- **03c (State Patterns):** ini sesi refleksi, bukan materi baru. Ajak peserta gambar alur data di papan tulis.

### Minggu 4
- **04a (Router):** latihan mini app routing sebelum implementasi di Katalog sangat membantu.
- **04b (Slice 4):** dependency array `[id]` di `useEffect` adalah titik paling gampang salah — siapkan contoh "kalau [id] dihapus, apa yang terjadi" secara live.
- **04c (Konsolidasi):** pastikan peserta beneran rapikan kode, bukan skip ke showcase.

## Checkpoint akhir Bulan 2

Sebelum lanjut ke folder `2-React-Lanjutan` (Bulan 3), pastikan tiap peserta bisa:
1. branch → commit → PR → revisi → merge, tanpa dibantu;
2. menjelaskan alur `fetch` (kenapa perlu loading/error state);
3. menunjukkan salah satu PR miliknya dan menjelaskan isinya sendiri;
4. menjelaskan konsep SPA, component, props, state, dan useEffect dengan kata-kata sendiri.

Kalau ada yang belum, jangan tunda ke Bulan 3 — tambah sesi pairing di minggu pertama Bulan 3, bukan skip begitu saja.
