# Panduan Mentor — Minggu 2: Computational Thinking & Algoritma

**Fokus Minggu Ini:** Mengonversi masalah bisnis UMKM menjadi representasi logika yang dapat dipahami komputer: dekomposisi langkah, perancangan algoritma/pseudocode, pemodelan alur visual (Flowchart dengan simbol baku), dan pengenalan relasi data (Entity Relationship Diagram - ERD dasar).

**Ritme:** 5 Sesi Materi & Workshop (Senin–Jumat) + 1 Sesi Review & Evaluasi (Sabtu). Alokasi per sesi: ±90-120 menit.

---

## Peta Sesi Minggu 2

| Sesi | Hari | File Modul | Poin Mini-Lesson Mentor (20-30 Menit) | Output Sesi / Workshop |
|---|---|---|---|---|
| 1 | Senin | `02a-dekomposisi-dan-pengenalan-pola.md` | Membedah proses bisnis UMKM (penerimaan pesanan, kelola stok) menjadi sub-proses mikro; mencari pola berulang (*reusability*). | **Peta Dekomposisi & Pola Bisnis UMKM** |
| 2 | Selasa | `02b-abstraksi-dan-algoritma.md` | Memisahkan data esensial dari detail tak penting; menulis pseudocode bahasa Indonesia dengan struktur runtut (sekuensial, kondisional/if-else, perulangan/loop). | **Dokumen Pseudocode Logika Bisnis** |
| 3 | Rabu | `02c-flowchart.md` | Standar simbol ISO/ANSI: Terminator, Process, Decision, Input/Output, Arrow. Aturan panah kembali (*loop*) dan percabangan (*Yes/No*). | **Minimal 2 Flowchart Fitur Platform UMKM per Squad** |
| 4 | Kamis | `02d-erd-dasar.md` | Mengapa database butuh model data; konsep Entitas, Atribut, Primary Key sederhana, dan Relasi (1:1, 1:N, N:N). Studi kasus: Produk, Kategori, Merchant. | **Draft ERD Sederhana Platform UMKM** |
| 5 | Jumat | `02e-latihan-terpadu-ct.md` | Menghubungkan semua pilar: dari cerita user UMKM → Dekomposisi → Pseudocode → Flowchart → Skema Data ERD. | **Portofolio Terpadu Logika Fitur** |
| 6 | Sabtu | `02f-review-dan-evaluasi-minggu2.md` | Sprint Review & Evaluasi Mingguan: Presentasi flowchart & ERD squad, ujian membaca diagram dan melacak bug alur (*tracing test*). | **Rubrik Penilaian Minggu 2 & Feedback Teknis** |

---

## Jebakan Mental Model Siswa Minggu Ini

1. **Flowchart "menggantung" tanpa Terminator:** Siswa sering membuat percabangan decision (*Yes/No*), tapi salah satu cabang tidak berujung ke mana-mana (*dead end*) atau lupa diberi panah `End/Selesai`.
2. **Kondisi decision tidak jelas Yes/No-nya:** Siswa menulis pertanyaan di diamond, tapi kedua garis keluar tidak dilabeli mana yang "Ya" dan mana yang "Tidak".
3. **Bingung membedakan Entitas vs Atribut pada ERD:** Siswa sering membuat "Harga" atau "Nama Produk" sebagai entitas tersendiri, padahal itu adalah atribut dari entitas "Produk". Jelaskan dengan analogi benda nyata (Entitas = Formulir/Benda, Atribut = Kolom isian pada formulir).
4. **Pseudocode terlalu teknis atau terlalu santai:** Jika terlalu santai (*"lalu pesanannya diproses"*), komputer tidak bisa menerjemahkannya. Jika terlalu memusingkan sintaks bahasa tertentu (seperti semicolon), mereka kehilangan fokus pada logikanya.

---

## Rubrik Penilaian Sprint Review (Sabtu)

| Kriteria | Bobot | Indikator Skor Maksimal (4) |
|---|---|---|
| **Ketepatan Flowchart** | 35% | Simbol standar tepat, semua percabangan memiliki label Yes/No, tidak ada panah buntu, alur logis diuji dengan *edge cases*. |
| **Kematangan Konsep ERD** | 30% | Entitas dan atribut terpisah benar, relasi 1:N dijelaskan logis (misal 1 Kategori memiliki banyak Produk), atribut kunci teridentifikasi. |
| **Kerapian Pseudocode & Dekomposisi** | 20% | Langkah tidak ambigu, struktur sekuensial dan if-else jelas, memecah masalah dari hulu ke hilir. |
| **Tanya Jawab & Pelacakan Alur (*Tracing*)** | 15% | Mampu menjawab skenario kegagalan: *"Bagaimana jika pembeli bayar tapi stok pas habis?"* dengan menunjuk diagramnya secara tepat. |
