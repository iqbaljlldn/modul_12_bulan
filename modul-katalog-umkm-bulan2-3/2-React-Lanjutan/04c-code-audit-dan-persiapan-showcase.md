# 2.4c Audit Kualitas Kode & Persiapan Showcase Akhir Bulan 3

> **Tujuan sesi:** Melakukan audit menyeluruh kualitas kode, membersihkan technical debt, dan mempersiapkan demo produk Mini Katalog UMKM v2 di hadapan tribe.  
> **Format:** Audit mandiri + simulasi demo berpasangan (pairing).

---

## 1. Audit Kualitas Kode (*Engineering Standards Checklist*)

Sebelum melakukan showcase di hadapan seluruh tribe, setiap squad wajib melakukan *code cleaning* dengan kacamata: *"Apakah kode ini mudah dibaca oleh developer lain?"*.

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
- Hapus komentar `// TODO: ganti kategori hardcode` yang sudah selesai sejak Slice 5.
- Hapus `console.log()` debug yang tidak perlu.
- Pastikan penamaan komponen dan variabel konsisten (PascalCase untuk Komponen, camelCase untuk fungsi/variabel).

---

## 2. Naskah Demo Showcase Mini Katalog UMKM v2 (5 Menit)

Saat sesi Showcase di hadapan mentor dan rekan-rekan tribe, jangan hanya membuka kode di VS Code. Bawakan demo produk seperti seorang Software Engineer profesional yang mempresentasikan hasil kerjanya ke Product Manager dan Client:

### Urutan Alur Demo:
1. **Navigasi & Tampilan Baru (Menit 1):**
   - Tunjukkan antarmuka baru Katalog yang rapi menggunakan Tailwind CSS.
   - Buka DevTools Device Toolbar, ubah ke mode layar HP: perlihatkan bahwa form dan kartu produk tertata responsif tanpa ada elemen yang terpotong.
2. **Eksplorasi Katalog: Filter, Cari & Paginasi (Menit 2):**
   - Ketik nama produk di kotak pencarian: perlihatkan request baru terkirim dengan jeda debounce mulus tanpa lag.
   - Pilih kategori dan ubah pengurutan harga: tunjukkan bagaimana kartu langsung menyesuaikan.
   - Pindah ke halaman 2 via tombol Pagination.
   - **Momen Kunci:** Tekan tombol **F5 (Refresh)** di browser: tunjukkan bahwa seluruh filter dan halaman tetap utuh karena tersimpan rapi di URL!
3. **Form & Validasi Cerdas (Menit 3):**
   - Buka Form Tambah Produk.
   - Coba submit dengan harga `0` dan nama kosong: perlihatkan garis merah dan pesan error yang ramah.
   - Isi data yang benar, lalu submit: perlihatkan notifikasi mengambang (Toast) hijau yang muncul di bawah layar dan hilang otomatis.
4. **Presentasi Kontrak API untuk Chapter Backend (Menit 4):**
   - Buka dokumen `docs/kontrak-api.md`.
   - Jelaskan kepada rekan Chapter Backend: *"Ini daftar endpoint, method, dan format data yang dibutuhkan oleh frontend mulai bulan depan"*.
   - Sebutkan catatan penting perbedaan `json-server` dengan rencana NestJS (relasi kategori, validasi DTO server-side).
5. **Tanya Jawab & Peer Feedback (Menit 5).**

---

## 3. Retrospektif & Evaluasi Kemampuan (Capability Snapshot 1)

Bulan 3 menandai akhir dari **Phase 1 (Foundations & Frontend)**. Cek apakah kamu sudah memenuhi **Checkpoint Keluar Bulan 3**:

- [ ] **Membangun UI Multi-halaman Interaktif:** Mampu membuat form terkontrol, validasi manual, routing dinamis, dan konsumsi API REST.
- [ ] **State Architecture:** Mampu membedakan kapan menggunakan `useState` lokal, Custom Hook, React Context, dan URL Search Params.
- [ ] **Code Review & Kerjasama Tim:** Mampu membaca kode rekan squad, menemukan celah bug, dan memberikan umpan balik yang sopan dan terarah di PR GitHub.
- [ ] **Dokumentasi Teknis:** Mampu menyusun Kontrak API tertulis yang akurat berdasarkan kode sungguhan.

---

## Selamat! 🎉

Kamu telah berhasil menyelesaikan **Mini Katalog UMKM v2**!  
Aplikasi frontend-mu sekarang sudah sangat matang, berkinerja tinggi, responsif, dan siap dihubungkan dengan backend asli.

Di **Bulan 4**, kita akan melangkah ke dunia backend: membangun server REST API sungguhan menggunakan **NestJS**, menghubungkannya ke basis data relasional **PostgreSQL**, dan menggantikan `json-server` sepenuhnya!
