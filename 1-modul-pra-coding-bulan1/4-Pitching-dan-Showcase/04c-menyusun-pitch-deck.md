# 04c. Menyusun Pitch Deck: 7 Slide Esensial Berbasis Bukti Nyata

**Minggu 4: Pitching & Showcase | Sesi 3 (Rabu)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Draf Pitch Deck Lengkap per Squad (7 Slide Visual) *(di-push link/PDF-nya ke repo squad untuk dipresentasikan saat Daily Standup besok pagi)*

---

## 1. Mengapa Ini Penting?

Banyak presentasi teknologi gagal karena penyakit **"Death by PowerPoint"**:
- Slide dipenuhi paragraf tulisan kecil-kecil yang tidak terbaca penonton.
- Presenter hanya berdiri membaca slide kata demi kata tanpa menatap penonton.
- Tidak ada bukti konkret (*proof of work*), hanya klaim abstrak dan janji manis.

Slide presentasi bukanlah makalah skripsi. **Slide adalah alat bantu visual untuk memperkuat kata-katamu**.

Hari ini, setiap squad merakit seluruh artefak yang telah diproduksi selama 3 minggu terakhir menjadi **Pitch Deck 7 Slide** yang padat, memukau, dan sarat bukti visual nyata.

---

## 2. Struktur Standar 7 Slide Pitch Deck

| Slide | Fokus Konten Pitch Deck |
|---|---|
| **Slide 1** | **Cover:** Nama produk/platform, tagline singkat, & daftar anggota squad |
| **Slide 2** | **Masalah Nyata:** Cerita singkat & *persona* hasil wawancara UMKM nyata |
| **Slide 3** | **Nilai Solusi:** *Value Proposition Statement* yang menjawab masalah |
| **Slide 4** | **Bukti Desain Antarmuka:** Ekspor Wireframe Figma 3 halaman utama katalog |
| **Slide 5** | **Bukti Alur Logika:** *Flowchart* & *User Flow* pemesanan hingga ke WhatsApp |
| **Slide 6** | **Bukti Struktur Data:** Diagram ERD model data produk & pesanan |
| **Slide 7** | **Roadmap & Penutup:** Rencana eksekusi Slice 0–4 di Bulan 2 & ajakan diskusi |

### Rincian Konten Tiap Slide:

#### Slide 1: Cover & Judul Menarik
- Nama Platform (contoh: *"KatalogLokal — Etalase Digital Ringan untuk Pedagang Rumahan"*).
- Logo / ikon sederhana.
- Nama Squad dan daftar nama anggotanya.

#### Slide 2: Masalah Nyata & Persona Pengguna
- Profil pedagang **hasil wawancara nyata squad** di Sesi `03c`/`03d` (`catatan-wawancara-squad.md` & `persona-dan-prioritas-fitur.md`). Patuhi izin narasumber: jika tidak mengizinkan nama/foto asli, gunakan nama samaran atau ikon ilustrasi.
- 3 Penderitaan utama yang benar-benar terbukti dari wawancara (bukan karangan atau salinan contoh modul!).
- **Kutipan langsung (*quote*) keluhan asli** dari pedagang yang diwawancarai.

#### Slide 3: Solusi & Nilai Manfaat (*Value Proposition*)
- Pernyataan *Value Proposition* 1 kalimat dari `value-proposition-squad.md` (`03c`).
- Alasan praktis mengapa katalog web ini cocok untuk pedagang kecil yang diwawancarai (cepat dibuka lewat HP kelas pemula, tanpa alur checkout rumit, langsung terhubung ke WhatsApp).

#### Slide 4: Bukti Desain Antarmuka (*The Interface*)
- Tampilkan gambar ekspor PNG **Wireframe Figma 3 halaman** dari `03b` (`Katalog Utama`, `Detail Produk`, dan `Dashboard Kelola Produk`).
- Sorot minimal **1 keputusan UX terbaik** dari `03a`/`03b` (misal: tombol *"Pesan via WhatsApp"* besar di zona jempol bawah layar atau kartu nonaktif otomatis saat `Stok = 0`).

#### Slide 5: Bukti Alur Sistem (*The Logic Flow*)
- Cuplikan diagram *Flowchart* (`02c`) & *User Flow* (`04b`) alur pemesanan via WhatsApp.
- Tunjukkan bagaimana sistem menangani kondisi gagal (misal: stok habis atau validasi nomor WA / 404).

#### Slide 6: Bukti Model Data (*The Data Model*)
- Cuplikan diagram ERD dari `02d` (Entitas `Merchant`, `Kategori`, `Produk`, `Pesanan`, dan entitas penghubung `ItemPesanan`).
- Jelaskan singkat dalam bahasa manusia mengapa data ditata demikian: 1 pesanan bisa mencatat banyak barang sekaligus, dan pembeli tidak perlu membuat akun login yang merepotkan.

#### Slide 7: Roadmap Eksekusi Bulan 2 & Penutup
- Tampilkan cuplikan backlog dari `rencana-fitur-backlog.md` (`03e`): fokus membangun **Slice 0–2** lebih dulu hingga selesai **Slice 0–4** (*Walking Skeleton* dengan React & TypeScript di Bulan 2).
- Kalimat penutup yang percaya diri dan membuka sesi tanya jawab panelis.

---

## 3. Tiga Aturan Emas Desain Slide

1. **Prinsip Satu Pesan per Slide:** Jangan menumpuk masalah, flowchart, dan tabel data dalam satu slide yang sesak.
2. **Ukuran Font Minimal 24pt:** Jika teks harus dikecilkan di bawah 20pt agar muat, berarti teks tersebut terlalu panjang dan wajib dipangkas!
3. **Biar Gambar dan Diagram yang Bicara:** Gambar ekspor Figma dan diagram alurmu jauh lebih meyakinkan daripada 5 paragraf teks panjang.

---

## 4. Workshop Praktik Squad (60 Menit)

Gunakan Google Slides, Canva, atau Figma Slides sesuai pilihan squad:
1. **Langkah 1 — Bagi Tugas Slide (10 Menit):**
   - Pembagian adil antar anggota squad (misal untuk 3 orang: Anggota 1 menyiapkan Slide 1–3, Anggota 2 menyiapkan Slide 4–5, Anggota 3 menyiapkan Slide 6–7).
2. **Langkah 2 — Rakit Slide dari Artefak Repo (35 Menit):**
   Ambil kutipan wawancara asli (`03c`), persona (`03d`), ekspor PNG Figma (`03b`), diagram Mermaid (`02c`/`02d`/`04b`), dan cuplikan backlog (`03e`) lalu tata secara bersih.
3. **Langkah 3 — Harmonisasi Gaya (15 Menit):**
   Pastikan gaya font, palet warna, dan ukuran teks konsisten dari Slide 1 sampai Slide 7.

---

## 5. Output Sesi

*Push* tautan (*link* view terbuka) atau file PDF **Draf Pitch Deck Final Squad (7 Slide)** ke repositori squad (siap digunakan dan dievaluasi saat Gladi Resik / Daily Standup besok).

---

## 6. Tugas Mandiri (Individual)

- **Sifat:** Pribadi. Ini **catatan latihan untuk dirimu sendiri** mengecek kesiapan slide bagianmu (bukan bahan wajib dokumen tim).
- **Target Waktu:** 25 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_04c.md` *(di-push untuk dibahas saat Daily Standup besok pagi)*

### Instruksi:
1. Buka 2 atau 3 slide yang menjadi bagian giliran bicaramu untuk Gladi Resik besok.
2. Lakukan audit mandiri menggunakan checklist 3 pertanyaan:
   - Apakah ukuran font di slidemu minimal 24pt?
   - Apakah slidemu didominasi oleh gambar diagram/artefak (bukan paragraf teks panjang)?
   - Apakah kamu bisa menjelaskan slide tersebut dalam waktu maksimal 2 menit tanpa membaca tulisan di slide?
3. Tuliskan catatan perbaikan slide pribadimu di `tugas_04c.md`.

### Contoh Hasil yang Diharapkan:
```markdown
# Tugas Mandiri 04c — Audit Slide Bagian Pribadi
> [ILUSTRASI CONTOH — isi sesuai slide bagianmu sendiri]

Nama: [Nama Kamu]
Bagian Slide Saya: Slide 4 (Wireframe Figma) dan Slide 5 (Flowchart & User Flow)

## 1. Hasil Pengecekan Checklist:
- Ukuran Font: Awalnya 18pt karena banyak kalimat penjelasan. Sudah saya hapus paragrafnya, diganti 3 poin singkat berukuran 28pt.
- Dominasi Visual: 80% area slide sekarang berisi gambar ekspor Wireframe Figma 3 halaman dan diagram alur yang jelas.
- Durasi Bicara: Saya mencoba latihan dengan stopwatch: butuh 1 menit 45 detik untuk menjelaskan kedua slide ini.

## 2. Poin Utama yang Akan Saya Ucapkan Secara Lisan:
"Kami tidak sekadar berasumsi soal tampilan; di Slide 4 ini teman-teman bisa melihat wireframe 3 halaman yang kami rancang di Figma agar tombol WhatsApp mudah dijangkau jempol pembeli..."
```

---

## 7. Cek Pemahaman Diri

1. Mengapa panelis lebih terkesan melihat gambar ekspor Figma, flowchart, dan ERD nyata daripada teks janji manis di slide presentasi?
2. Mengapa Slide 2 wajib memakai data dan kutipan asli wawancara squad, tidak boleh memakai contoh modul?

---

Lanjut ke: **[04d-gladi-resik-dan-peer-feedback.md](04d-gladi-resik-dan-peer-feedback.md)**
