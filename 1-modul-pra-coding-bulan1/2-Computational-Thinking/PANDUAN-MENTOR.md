# Panduan Mentor — Minggu 2: Computational Thinking & Algoritma

**Fokus Minggu Ini:** Mengonversi alur masalah UMKM ke dalam logika terstruktur yang dapat dipahami sistem: dekomposisi langkah operasional, penulisan pseudocode bahasa Indonesia baku, visualisasi alur dengan Flowchart (pemesanan via WhatsApp & kelola produk), pemodelan relasi data (ERD dasar dengan entitas penghubung `ItemPesanan`), serta menjaga memori otot ngoding lewat 1 latihan kode JavaScript sederhana.

**Ritme:** 5 Sesi Materi & Workshop (Senin–Jumat) + 1 Sesi Review Mingguan (Sabtu). Alokasi per sesi: ±90-120 menit.

---

## 1. Peta Sesi Minggu 2

| Sesi | Hari | File Modul | Poin Mini-Lesson Mentor (20-30 Menit) | Output Sesi / Workshop Tim |
|---|---|---|---|---|
| 1 | Senin | `02a-dekomposisi-dan-pengenalan-pola.md` | Membedah proses bisnis UMKM menjadi 2 alur kunci (Pemesanan WhatsApp & Restok/Kelola Produk, 6-8 langkah); mencari pola logika berulang. | **Peta Dekomposisi & Pola Logika (2 Alur)** |
| 2 | Selasa | `02b-abstraksi-dan-algoritma.md` | Abstraksi data (buang noise); struktur pseudocode baku (`JIKA ... MAKA ... LAINNYA ... AKHIR-JIKA`); dry run table. Jembatan kode JS fungsi diskon/ongkir. | **Dokumen Pseudocode Logika Bisnis** |
| 3 | Rabu | `02c-flowchart.md` | Simbol baku industri (Terminator, Proses, Decision, Data I/O); Flowchart 1: Tambah Produk, Flowchart 2: Pemesanan via WhatsApp (bukan checkout COD/transfer). | **Minimal 2 Flowchart Fitur Platform UMKM** |
| 4 | Kamis | `02d-erd-dasar.md` | Model data ERD: Entitas, Atribut, PK, Relasi 1:N dan N:N; Entitas penghubung `ItemPesanan`; penjelasan data Pembeli (tanpa login); Status alur WA. | **Draft ERD Platform Katalog UMKM** |
| 5 | Jumat | `02e-latihan-terpadu-ct.md` | Menghubungkan 1 fitur pilihan: Dekomposisi → Pseudocode → 1 Flowchart → Potongan ERD (3-5 atribut). Penjelasan atomic transaction pada flash sale. | **Portofolio Terpadu 1 Fitur Pilihan** |
| 6 | Sabtu | `02f-review-dan-evaluasi-minggu2.md` | Sprint Review 2: Presentasi tiap squad (5m pitch + 3m Q&A); Ujian "Bug Hunt" melacak diagram cacat; Retrospektif tim rolling. | **Checklist Kapabilitas Minggu 2 & Refleksi** |

---

## 2. Beban Tugas Mandiri Minggu 2 (Individual)

Setiap murid mengerjakan tugas mandiri individual dan menyimpannya di folder masing-masing dalam repo squad (`tugas_<kode-sesi>.md`). Total estimasi waktu di luar kelas: **135 menit (±2,25 jam)**, terukur dan tidak membebani.

| Sesi | Kode File | Nama Tugas Mandiri | Estimasi Waktu |
|---|---|---|---|
| 02a | `tugas_02a.md` | Dekomposisi 1 Proses Warung Sekitar (6-8 langkah) | 20 menit |
| 02b | `tugas_02b.md` | **Jembatan Kode 1:** Terjemahkan Pseudocode ke Fungsi JavaScript Sederhana + Dry Run Table | 25 menit |
| 02c | `tugas_02c.md` | Flowchart Sederhana Validasi Form Tambah Produk | 25 menit |
| 02d | `tugas_02d.md` | Menentukan Entitas, Atribut, & Relasi Fitur Ulasan Ringkas | 25 menit |
| 02e | `tugas_02e.md` | Uji Konsistensi Mandiri: Menghubungkan Variabel Pseudocode dengan Kolom ERD | 25 menit |
| 02f | `tugas_02f.md` | Refleksi Pribadi Sprint 2 (3-5 Kalimat) | 15 menit |
| **Total** | | | **135 menit (2 jam 15 menit)** |

---

## 3. Jebakan Mental Model Siswa Minggu Ini

1. **Flowchart "menggantung" tanpa Terminator:** Siswa sering membuat percabangan decision (*Ya/Tidak*), tapi salah satu cabang tidak berujung ke mana-mana (*dead end*) atau lupa diberi panah `Selesai`. Ingatkan bahwa komputer tidak boleh berhenti di kondisi buntu tanpa instruksi penutup.
2. **Kondisi decision tidak jelas label Ya/Tidak-nya:** Siswa menulis pertanyaan di diamond, tapi garis keluar tidak diberi keterangan.
3. **Bingung membedakan Entitas vs Atribut pada ERD:** Siswa sering membuat "Harga" atau "Nama Produk" sebagai kotak entitas tersendiri, padahal itu adalah atribut dari entitas `Produk`. Gunakan analogi formulir fisik (Entitas = Kertas Formulir, Atribut = Kolom Isian pada formulir).
4. **Relasi Pesanan ke Produk (N:N):** Siswa sering bingung bagaimana 1 pesanan bisa membeli banyak produk sekaligus. Jelaskan mengapa kita membutuhkan tabel penghubung `ItemPesanan` (*Junction Table*).

---

## 4. Checklist Kapabilitas Sprint Review 2 (Sabtu)

Evaluasi dilakukan melalui checklist kapabilitas (status: **Siap**, **Hampir Siap**, atau **Perlu Pendampingan**) bersama catatan masukan konkret.

| # | Indikator Kapabilitas | Bukti Observasi | Status (Siap / Hampir Siap / Perlu Pendampingan) | Catatan Masukan Mentor |
|---|---|---|---|---|
| 1 | **Dekomposisi & Algoritma** | Menulis langkah runtut dengan format baku `JIKA ... MAKA ... LAINNYA ... AKHIR-JIKA`, tidak bermakna ganda. | | |
| 2 | **Kebenaran Flowchart** | Menggunakan simbol standar, percabangan Ya/Tidak lengkap, tidak ada panah buntu, alur pemesanan WA jelas. | | |
| 3 | **Model Data ERD Dasar** | Membedakan entitas dan atribut; relasi 1:N terhubung jelas; memahami fungsi entitas `ItemPesanan`. | | |
| 4 | **Sentuhan Kode JavaScript** | Murid mampu menuliskan fungsi JS sederhana untuk logika diskon/ongkir dan mencocokkan dengan dry run table. | | |
| 5 | **Analisis Bug Hunt** | Mampu menemukan minimal 3 dari 4 celah kesalahan pada diagram uji Sabtu. | | |

---

## 5. Panduan Mentor untuk Siswa "Perlu Pendampingan"

Jika seorang murid mendapat status *Perlu Pendampingan* pada Minggu 2:
1. **Latihan Tracing Menggunakan Jari (15 Menit):** Cetak atau tampilkan satu diagram flowchart sederhana. Minta murid menggerakkan jari telunjuknya menelusuri alur langkah demi langkah untuk satu kasus input konkret. Hal ini langsung memperjelas konsep percabangan logika.
2. **Klinik ERD Benda Nyata:** Ambil secarik kertas kwitansi belanja warung. Bimbing murid melingkari mana yang merupakan Toko, mana Pesanan, mana Barang, dan mana rincian per baris barang (`ItemPesanan`).
3. **Pendampingan Kode JS:** Bantu murid mengecek kembali penulisan tanda kurung kurawal `{}` dan sintaks `if / else` pada tugas 02b agar tidak trauma dengan error syntax.
