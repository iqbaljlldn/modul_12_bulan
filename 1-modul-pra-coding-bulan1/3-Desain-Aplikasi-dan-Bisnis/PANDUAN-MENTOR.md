# Panduan Mentor — Minggu 3: Desain Aplikasi & Bisnis UMKM

**Fokus Minggu Ini:** Mengembangkan empati produk ganda: empati terhadap pengguna melalui prinsip User Experience (UX dasar) dan kerangka antarmuka (Wireframing mobile-first), serta empati terhadap model bisnis UMKM melalui wawancara langsung 1 UMKM nyata per squad, Value Proposition Canvas, perumusan persona, dan penerjemahan desain ke rencana backlog (Slice 0).

**Ritme:** 5 Sesi Materi & Workshop (Senin–Jumat) + 1 Sesi Review Mingguan (Sabtu). Alokasi per sesi: ±90-120 menit.

---

## 1. Peta Sesi Minggu 3

| Sesi | Hari | File Modul | Poin Mini-Lesson Mentor (20-30 Menit) | Output Sesi / Workshop Tim |
|---|---|---|---|---|
| 1 | Senin | `03a-prinsip-ux-dasar.md` | UI vs UX; Prinsip Kebiasaan Pengguna (analogi Jakob's Law) & Prinsip Tombol Jangkauan Jempol (analogi Fitts's Law); Umpan balik status sistem. | **Laporan "UX Review" Aplikasi Nyata** |
| 2 | Selasa | `03b-wireframe-dan-merancang-tampilan.md` | Wireframe (cetak biru hitam-putih, bukan estetika warna); Desain mobile-first; 3 Halaman Inti (Katalog, Detail, Dashboard). Jembatan kode HTML/CSS statis. | **Wireframe 3 Halaman Inti Platform UMKM** |
| 3 | Rabu | `03c-value-proposition-dan-model-bisnis.md` | Mencocokkan masalah pengguna dengan solusi aplikasi; Pasar dua sisi (Merchant & Buyer); Panduan Wawancara 1 UMKM Nyata (5-6 pertanyaan terarah). | **Value Proposition Canvas & Rencana Wawancara** |
| 4 | Kamis | `03d-sudut-pandang-pelanggan-umkm.md` | Persona pengguna wajib berbasis temuan wawancara UMKM nyata (Bu Sri sebagai ilustrasi modul); Prioritas fitur metode MoSCoW disederhanakan. | **Persona Nyata & Daftar Fitur Prioritas** |
| 5 | Jumat | `03e-dari-desain-ke-rencana-fitur.md` | Konsep Vertical Slicing kue lapis; Menulis User Story & Syarat Selesai (Acceptance Criteria); Rincian mendalam Slice 0, rangkuman Slice 1 & 2. | **Draf Backlog Fitur Platform UMKM (Slice 0-2)** |
| 6 | Sabtu | `03f-review-dan-evaluasi-minggu3.md` | Sprint Review 3: Presentasi squad (5m pitch + 3m Q&A); Simulasi Uji Kegunaan Silang (*Cross-Usability Walkthrough*); Retrospektif tim. | **Checklist Kapabilitas Minggu 3 & Refleksi** |

---

## 2. Beban Tugas Mandiri Minggu 3 (Individual)

Setiap murid mengerjakan tugas mandiri individual dan menyimpannya di folder masing-masing dalam repo squad (`tugas_<kode-sesi>.md`). Total estimasi waktu di luar kelas: **140 menit (±2,3 jam)**, terkontrol di bawah batas 2,5 jam.

| Sesi | Kode File | Nama Tugas Mandiri | Estimasi Waktu |
|---|---|---|---|
| 03a | `tugas_03a.md` | Observasi 1 Hambatan UX di Kehidupan Nyata Sekitar | 20 menit |
| 03b | `tugas_03b.md` | **Jembatan Kode 2:** Halaman HTML & CSS Statis Hitam-Putih untuk 1 Kartu Produk | 25 menit |
| 03c | `tugas_03c.md` | **Riset Pengguna Nyata:** Catatan Wawancara 1 Pelaku UMKM (3 temuan + 1 kutipan asli) | 30 menit |
| 03d | `tugas_03d.md` | Menyusun Mini Persona Pengguna Nyata Berdasarkan Temuan Wawancara | 25 menit |
| 03e | `tugas_03e.md` | Menulis 1 User Story + 2 Kriteria Penerimaan (*Acceptance Criteria*) Fitur Sederhana | 25 menit |
| 03f | `tugas_03f.md` | Refleksi Pribadi Sprint 3 (3-5 Kalimat) | 15 menit |
| **Total** | | | **140 menit (2 jam 20 menit)** |

---

## 3. Jebakan Mental Model Siswa Minggu Ini

1. **Terjebak membuat "UI Cantik" bukan "Wireframe":** Siswa menghabiskan waktu berjam-jam memilih warna gradasi, icon estetik, atau foto di Canva/Figma, padahal tata letak dan hierarki tombol utamanya belum jelas. Tegaskan: **Gunakan warna hitam, putih, dan abu-abu saja untuk wireframe!**
2. **Asumsi egosentris ("Menurut saya keren..."):** Siswa mendesain antarmuka yang hanya cocok untuk anak muda melek teknologi (font kecil-kecil, menu tersembunyi), melupakan bahwa user UMKM adalah bapak/ibu paruh baya yang butuh tombol besar dan teks kontras jelas.
3. **Mengabaikan hasil wawancara lapangan:** Siswa tergoda mengarang data keluhan pengguna. Wajibkan bahwa persona di 03d dan kutipan di slide pitching berasal dari wawancara nyata yang dilakukan squad di 03c.

---

## 4. Checklist Kapabilitas Sprint Review 3 (Sabtu)

Evaluasi dilakukan menggunakan checklist kapabilitas (status: **Siap**, **Hampir Siap**, atau **Perlu Pendampingan**) bersama catatan masukan konkret.

| # | Indikator Kapabilitas | Bukti Observasi | Status (Siap / Hampir Siap / Perlu Pendampingan) | Catatan Masukan Mentor |
|---|---|---|---|---|
| 1 | **Prinsip UX & Wireframing** | Tata letak mobile-first jelas, tombol aksi utama (*Call to Action*) mencolok, lulus uji coba simulasi silang antarsquad tanpa macet. | | |
| 2 | **Riset Pengguna Nyata** | Persona dan Value Proposition disusun berdasarkan data wawancara UMKM nyata, bukan karangan asumsi semata. | | |
| 3 | **Sentuhan Kode HTML/CSS** | Murid mampu menyusun kerangka statis HTML/CSS hitam-putih untuk komponen kartu produk sederhana. | | |
| 4 | **Perumusan Backlog (Slice 0)** | Mampu menuliskan User Story dan syarat selesai (*Acceptance Criteria*) yang dapat diuji secara biner. | | |
| 5 | **Kerjasama & Presentasi Tim** | Semua anggota berbicara aktif dalam batas waktu 5 menit presentasi (+3 menit tanya jawab). | | |

---

## 5. Panduan Mentor untuk Siswa "Perlu Pendampingan"

Jika seorang murid mendapat status *Perlu Pendampingan* pada Minggu 3:
1. **Bedah Wireframe Bersama:** Buka kertas wireframe murid. Tanyakan: *"Jika jempol tangan kananmu memegang HP, bisakah kamu menjangkau tombol Pesan ini tanpa meregangkan jari?"* Bantu murid menata ulang tata letak tombol.
2. **Klinik User Story Sederhana:** Bimbing murid mengisi template kalimat: *"Sebagai [siapa], saya ingin [apa], agar [kenapa]"* dengan studi kasus sederhana (misal: tombol filter kategori).
3. **Pendampingan HTML/CSS:** Pastikan murid tidak bingung antara tag HTML (`<div>`, `<h1>`, `<button>`) dan styling CSS dasar (`display: flex`, `border`).
