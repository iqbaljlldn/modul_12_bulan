# 2.4c Audit Kualitas Kode & Persiapan Showcase Akhir Bulan 3

> **Tujuan sesi:** Melakukan audit menyeluruh kualitas kode, membersihkan technical debt, menyelaraskan kontrak API squad, dan mempersiapkan demo produk Mini Katalog UMKM v2 untuk **Sprint Review 4 / Showcase Akhir Bulan 3**.  
> **Format:** Blok 1 (Panduan Audit) → Blok 2 (Audit Pairing & Konsolidasi Squad) → Blok 3 (Tugas Mandiri + Gladi Resik).

---

## 1. Audit Kualitas Kode (*Engineering Standards Checklist* — Blok 1 & 2)

Sebelum melakukan showcase di hadapan seluruh tribe, setiap peserta bersama rekan satu squad wajib melakukan *code cleaning* dengan kacamata: *"Apakah kode ini mudah dibaca dan dilanjutkan oleh developer lain?"*.

### Langkah A: Jalankan Linter Cepat (`oxlint`)
```bash
npm run lint
```
Periksa dan selesaikan semua peringatan:
- Hapus import yang tidak terpakai (*unused imports*).
- Hapus variabel atau parameter fungsi yang tidak pernah dibaca.
- Pastikan tidak ada `any` yang tertinggal di tipe TypeScript.

### Langkah B: Jalankan Type-Check & Build Produksi
```bash
npm run build
```
Perintah ini menjalankan `tsc -b && vite build`.
Jika ada tipe data yang tidak cocok di salah satu komponen, proses build akan langsung gagal dan mencetak baris yang bermasalah. **Aplikasi dianggap belum selesai jika `npm run build` masih menghasilkan error!**

### Langkah C: Bersihkan Sisa "Kode Buru-buru"
- Hapus komentar `// TODO:` lama yang sudah selesai sejak Slice 5–7.
- Hapus `console.log()` debug yang tidak perlu.
- Pastikan penamaan komponen dan variabel konsisten (`PascalCase` untuk Komponen & Tipe, `camelCase` untuk fungsi/variabel/hooks, `snake_case` untuk field payload API).

---

## 2. Misi Squad Mingguan: Naskah Showcase Mini Katalog UMKM v2 (Sabtu)

Pada sesi **Sprint Review 4 / Showcase Akhir Bulan 3** hari Sabtu, ketiga squad bergiliran tampil selama **12-15 menit per squad** (termasuk **5 menit presentasi inti produk & Kontrak API** di depan mentor dan calon Chapter Backend + Tanya Jawab / Peer Feedback).

### Urutan Alur Presentasi Squad:
1. **Navigasi & Tampilan Responsif HP (Menit 1):**
   - Tunjukkan antarmuka baru Katalog yang rapi menggunakan Tailwind CSS v4.
   - Buka DevTools Device Toolbar (`iPhone SE 375px`), perlihatkan bahwa form, filter, dan kartu produk tertata mobile-first tanpa horizontal scroll.
2. **Eksplorasi Katalog: Cari, Filter, Sort & Pagination (Menit 2):**
   - Ketik nama produk di kotak pencarian: tunjukkan tab Network hanya mengirim 1 request setelah jeda debounce 400ms.
   - Pilih kategori, ubah pengurutan harga, dan pindah ke halaman 2.
   - **Momen Kunci:** Tekan tombol **F5 (Refresh)** di browser — buktikan bahwa seluruh filter dan halaman tetap utuh karena tersimpan di URL!
3. **Form, Validasi Cerdas & Notifikasi Toast (Menit 3):**
   - Coba submit Form Tambah Produk dengan harga `0` atau nama kosong: tunjukkan border merah & pesan error tanpa memicu HTTP `POST` di tab Network.
   - Isi data yang benar, lalu submit: tunjukkan toast notifikasi hijau muncul di bawah layar dan hilang otomatis.
4. **Presentasi Kontrak API Squad ke Chapter Backend (Menit 4-5):**
   - Buka dokumen `docs/kontrak-api.md` & `docs/decision-log.md`.
   - Jelaskan kepada rekan Chapter Backend: *"Ini daftar endpoint, method, format payload `CreateProductInput`, dan header `X-Total-Count` yang dibutuhkan frontend mulai bulan depan."*
   - Paparkan catatan perbedaan `json-server` vs NestJS (relasi `category`, validasi DTO server-side, format error JSON).
5. **Tanya Jawab, Sorotan Kode & Peer Feedback (Sisa Waktu):**
   - Rekan squad lain dan mentor memberikan masukan teknis, dilanjutkan pengisian **Survei Peminatan Chapter** (Frontend, Backend, Design, QA/DevOps) untuk persiapan Bulan 4–5.

---

## 3. Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan individual di kelas dan simpan hasilnya di repositori proyekmu pada:  
`tugas/tugas_04c.md`

1. Tuliskan identitas diri (Nama, Squad, Tanggal).
2. Tempelkan bukti output sukses terminal setelah menjalankan `npm run lint` dan `npm run build` (0 error, 0 warning).
3. Tuliskan refleksi pribadi akhir Fase 1 (3-5 kalimat):
   - Konsep Bulan 3 mana (*Custom Hook*, *Context API*, *URL Search Params*, *Debounce*, atau *Tailwind Mobile-First*) yang paling mengubah cara pandangmu dalam menyusun kode frontend?
   - Mengapa dokumen `docs/kontrak-api.md` penting sebelum tim berpindah ke Bulan 4 (NestJS & PostgreSQL)?

---

## 4. Retrospektif & Checkpoint Keluar Bulan 3

Bulan 3 menandai akhir dari **Phase 1 (Foundations & Frontend)**. Cek bersama squad sebelum masuk ke Bulan 4:

- [ ] **Membangun UI Multi-halaman Interaktif:** Mampu membuat form terkontrol, validasi murni, routing dinamis, layout mobile-first, dan konsumsi API REST.
- [ ] **State Architecture:** Mampu membedakan kapan menggunakan `useState` lokal, Custom Hook, React Context, dan URL Search Params.
- [ ] **Code Review & Kerjasama Tim:** Mampu me-review kode rekan squad dengan checklist dasar (*nama jelas, tipe benar, celah bug, lolos build/lint*) dan memberi umpan balik yang sopan di PR GitHub.
- [ ] **Dokumentasi Teknis:** Mampu menyusun Kontrak API tertulis & Decision Log yang akurat berdasarkan kode sungguhan.

---

Selamat menuntaskan **Mini Katalog UMKM v2!** Setelah Sprint Review & Retrospektif hari Sabtu, kalian siap melangkah ke **Bulan 4: Backend Full-stack Foundations (NestJS & PostgreSQL)**!
