# 01f. Review Mingguan: Sprint Review 1 & Retrospektif

**Minggu 1: AI Literacy | Sesi 6 (Sabtu)**  
**Target Waktu:** 120 Menit  
**Output Sesi:** Checklist Kapabilitas Minggu 1, Piagam Etika Final Tribe, dan Catatan Retrospektif

---

## 1. Format Sesi Hari Sabtu

Hari Sabtu adalah momen akuntabilitas, pembuktian artefak tim, dan refleksi hasil belajar seluruh squad selama seminggu penuh. Tidak ada nilai angka atau ujian kertas; evaluasi dilakukan lewat showcase langsung, tanya jawab, dan checklist kesiapan kapabilitas.

```text
┌─────────────────────────────────────────────────────────────┐
│                 AGENDA SPRINT REVIEW SABTU                  │
├─────────────────┬───────────────────────────────────────────┤
│ 1. Showcase     │ Presentasi artefak mingguan tiap squad    │
│    (50 Menit)   │ (6 squad x 8 menit: 5m presentasi + 3m QA)│
├─────────────────┼───────────────────────────────────────────┤
│ 2. Uji Praktik  │ Tantangan live prompt debugging & skenario│
│    (35 Menit)   │ etis dari mentor                          │
├─────────────────┼───────────────────────────────────────────┤
│ 3. Retrospektif │ Refleksi squad (apa yang lancar, apa yang │
│    (35 Menit)   │ macet) & persiapan Minggu 2               │
└─────────────────┴───────────────────────────────────────────┘
```

---

## 2. Bagian 1: Showcase Artefak Mingguan (50 Menit)

Setiap squad memiliki waktu **5 menit presentasi + 3 menit tanya jawab** dari mentor dan rekan tribe.

### Hal yang Dipresentasikan Tiap Squad:
1. **Piagam Etika Squad:** 1 poin etika paling krusial yang disepakati bersama.
2. **Cheat Sheet Prompt Engineering:** 1 template prompt terbaik buatan squad dan bukti perbedaannya dibanding prompt pemula.
3. **Mini-Proyek UMKM (Sesi 01d):** Solusi operasional untuk UMKM percontohan, termasuk demonstrasi bagian mana yang merupakan output AI dan bagaimana squad melakukan kurasi manual.

---

## 3. Bagian 2: Tantangan Praktik Spontan (35 Menit)

Mentor menampilkan satu skenario masalah di layar proyektor untuk dipecahkan bersama oleh squad dalam waktu 15 menit:

### Contoh Kasus: "Audit AI Kasir Warung Pintar"
> **Skenario:** Seorang rekan membuat prompt berikut ke AI untuk menentukan harga grosir telur di aplikasi warung:  
> *"Buatin rumus harga grosir telur kalau beli banyak biar untung."*  
> AI menjawab: *"Berikan diskon 50% untuk pembelian di atas 5 kg agar pelanggan senang dan loyal."*  
> Rekanmu langsung memasukkan saran ini ke sistem tanpa verifikasi.
>
> **Tugas Squad (Tulis dalam lembar kerja singkat):**
> 1. Analisis apa kelemahan fatal dari prompt rekanmu menggunakan kerangka R-C-I-C-O?
> 2. Mengapa diskon 50% adalah malapetaka bagi warung kelontong (margin sembako biasanya hanya 8–12%)?
> 3. Tulis ulang prompt tersebut agar AI memberikan rekomendasi diskon yang realistis!

---

## 4. Bagian 3: Sprint Retrospective (35 Menit)

Setiap squad berkumpul selama 15 menit untuk mengisi papan refleksi tim (*Mad, Sad, Glad*):

| Kolom | Pertanyaan Pemantik |
|---|---|
| **Mad (Bikin Kesal/Hambat)** | Apa kendala teknis atau koordinasi yang bikin kerja tim lambat minggu ini? |
| **Sad (Kurang Maksimal)** | Materi atau bagian apa yang squad rasa masih belum terlalu mantap? |
| **Glad (Berhasil Bagus)** | Keberhasilan apa yang dirayakan bersama? Hal positif apa dari teman satu squad? |

Tutup dengan menentukan **1 komitmen konkret perbaikan** untuk Minggu 2.

---

## 5. Output Sesi

1. Berita acara presentasi squad dan catatan umpan balik dari mentor.
2. Kompilasi Piagam Etika resmi gabungan seluruh squad.

---

## 6. Tugas Mandiri (Individual)

- **Sifat:** Individu (dikerjakan sendiri setelah sesi Sabtu)
- **Target Waktu:** 15 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_01f.md`

### Instruksi:
Tuliskan refleksi pribadi singkat (3–5 kalimat) yang menjawab 3 hal berikut:
1. Apa 1 konsep paling berharga yang benar-benar kamu pahami di Minggu 1?
2. Materi apa yang masih membuatmu bingung atau penasaran?
3. Apa 1 komitmen pribadimu untuk menyambut materi logika di Minggu 2?

### Contoh Hasil yang Diharapkan:
```markdown
# Tugas Mandiri 01f — Refleksi Pribadi Sprint 1
Nama: [Nama Kamu]

1. Hal yang paling saya pahami: Saya belajar bahwa prompt yang baik harus membedakan Context (latar belakang masalah) dan Constraint (batasan ketat agar AI tidak ngawur).
2. Hal yang masih membuat saya penasaran: Bagaimana cara menyusun alur keputusan bertahap yang rumit saat kasus tokonya memiliki banyak cabang kondisi.
3. Komitmen Minggu 2: Saya berkomitmen lebih aktif berdiskusi dalam squad dan siap mencoba latihan kode JavaScript kecil untuk melatih logika berpikir saya.
```

---

## 7. Checklist Kapabilitas Minggu 1

Mentor memberikan umpan balik berbasis checklist berikut untuk memastikan setiap murid siap melangkah ke minggu berikutnya:

| Indikator Kapabilitas | Bukti Evaluasi | Status | Catatan Feedback Mentor |
|---|---|---|---|
| **Etika Belajar AI** | Memahami kapan AI boleh & dilarang dipakai, bebas plagiarisme buta | [ ] Siap<br>[ ] Hampir Siap<br>[ ] Perlu Pendampingan | |
| **Struktur Prompting** | Menguasai formula R-C-I-C-O dan membedakan Context vs Constraint | [ ] Siap<br>[ ] Hampir Siap<br>[ ] Perlu Pendampingan | |
| **Kurasi & Validasi** | Mampu menemukan halusinasi AI dan memverifikasi data asumsi | [ ] Siap<br>[ ] Hampir Siap<br>[ ] Perlu Pendampingan | |
| **Partisipasi Tim** | Berbicara aktif saat presentasi 5 menit & standup harian | [ ] Siap<br>[ ] Hampir Siap<br>[ ] Perlu Pendampingan | |

> *Catatan Mentor:* Murid berstatus **Perlu Pendampingan** akan mendapatkan sesi klinik 1-on-1 singkat selama 15 menit pada hari Senin pagi untuk mengulang teknik R-C-I-C-O bersama mentor.

---

## 8. Penutup Minggu 1 & Menatap Minggu 2

Selamat! Kamu telah menyelesaikan Minggu 1. Kamu sudah memiliki etika yang kokoh dan tahu cara mengarahkan AI secara terstruktur.

Di **Minggu 2**, kita akan melangkah ke inti dari rekayasa perangkat lunak: **Computational Thinking & Algoritma**. Kita akan belajar membedah proses bisnis warung, menggambar flowchart visual alur pemesanan via WhatsApp, merancang hubungan data (ERD), serta **mulai menyentuh latihan kode JavaScript kecil** untuk menguji logika kita!

---

Lanjut ke: **[2-Computational-Thinking/PANDUAN-MENTOR.md](../2-Computational-Thinking/PANDUAN-MENTOR.md)**
