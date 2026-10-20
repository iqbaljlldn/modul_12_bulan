# 04b. AI untuk Merancang Alur Aplikasi: User Flow Tervalidasi

**Minggu 4: Pitching & Showcase | Sesi 2 (Selasa)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Dokumen User Flow Terpadu & Flowchart Tervalidasi Lengkap

---

## 1. Mengapa Ini Penting?

Sebelum memasukkan artefak ke dalam slide pitch deck, kita harus memastikan tidak ada "lubang hitam" dalam pengalaman pengguna aplikasi kita:
- Pengguna masuk dari mana?
- Setelah menekan tombol konfirmasi, layar apa yang muncul?
- Bagaimana data mengalir dari layar pembeli ke layar dashboard penjual?

Kombinasi antara **User Flow** (perjalanan langkah pengguna dari awal sampai akhir) dan **Flowchart Sistem** adalah bukti otentik bahwa produkmu matang dan siap dibangun di Bulan 2.

Hari ini kita akan memanfaatkan AI untuk melakukan *stress-test* terhadap user flow aplikasi kita, lalu memvalidasinya dengan ketat.

---

## 2. Apa Itu User Flow?

Jika flowchart berfokus pada **logika mesin** (*"Apakah stok > 0?"*), maka **User Flow** berfokus pada **tindakan dan layar yang dilalui manusia**:

```text
┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐
│  Landing Page   │ ──►   │ Filter Kategori │ ──►   │  Halaman Detail │ ──►   │ Klik Hubungi WA │
│ (Melihat Promo) │       │ (Pilih Sambal)  │       │ (Baca Komposisi)│       │ (Kirim Pesanan) │
└─────────────────┘       └─────────────────┘       └─────────────────┘       └─────────────────┘
```

---

## 3. Memanfaatkan AI untuk Melakukan Audit "Titik Kebuntuan" (*Blindspots*)

AI sangat hebat dalam memetakan skenario yang sering dilupakan manusia.

### Template Prompt Audit User Flow:
> **[Role]** Bertindaklah sebagai Lead UX Architect & QA Engineer profesional.  
> **[Context]** Kami sedang merancang User Flow untuk Platform Katalog UMKM. Pengguna utama kami adalah pembeli lokal yang memesan produk camilan dari pedagang rumahan.  
> **[Instruction]** Berikut adalah draf alur pengguna kami:  
> 1. Pembeli membuka link katalog toko di WhatsApp.  
> 2. Pembeli mencari produk camilan keripik.  
> 3. Pembeli membuka halaman detail produk.  
> 4. Pembeli menekan tombol 'Pesan via WhatsApp'.  
> 5. Sistem membuka aplikasi WhatsApp dengan template pesan otomatis terisi.  
> **[Task]** Analisis 4 skenario kebuntuan atau kegagalan (edge cases) di mana alur ini bisa rusak atau membuat pengguna frustrasi di dunia nyata Indonesia. Berikan rekomendasi perbaikan untuk setiap skenario.

---

## 4. Workshop Praktik Squad (60 Menit)

Setiap squad akan menyempurnakan **2 Alur Pengguna Utama**:

### Alur A: Perjalanan Pembeli (Buyer Journey)
Dari pertama kali menerima tautan toko → menyaring produk makanan → melihat detail & stok → melakukan pemesanan langsung ke WhatsApp penjual.

### Alur B: Perjalanan Pedagang (Merchant Journey)
Dari login pemilik toko → melihat ringkasan stok → mengedit harga produk yang sedang promo → menambah foto produk baru → mengecek tampilan katalog toko dari sisi pembeli.

### Langkah Kerja:
1. **Langkah 1 (Brainstorming Awal - 15 Menit):** Susun draf langkah-langkah Alur A dan Alur B di dokumen Markdown squad.
2. **Langkah 2 (Audit dengan AI - 20 Menit):** Gunakan prompt di atas untuk mencari celah kebuntuan pada alur kalian.
3. **Langkah 3 (Validasi Silang dengan ERD & Wireframe - 25 Menit):**
   - Pastikan setiap layar di User Flow memiliki gambar wireframe pendukung (dari Minggu 3).
   - Pastikan setiap data yang berpindah (misal: template pesan WA) memiliki atribut yang cocok di ERD (dari Minggu 2).

---

## 5. Output Sesi

Dokumen Markdown terpadu (`user-flow-tervalidasi.md`) yang memuat:
1. Diagram User Flow lengkap (bisa menggunakan sintaks Mermaid `graph LR` atau flowchart visual).
2. Daftar 3 potensi celah/kebuntuan yang ditemukan bersama AI beserta solusi penanganannya.
3. Konfirmasi keselarasan dengan Wireframe dan ERD.

---

## 6. Cek Pemahaman Diri

1. Apa perbedaan fokus antara diagram *User Flow* dengan *Flowchart Sistem*?
2. Mengapa integrasi pesan WhatsApp otomatis merupakan solusi yang sangat cerdas untuk UMKM Indonesia dibandingkan memaksa pembeli menggunakan keranjang belanja checkout yang rumit?

Lanjut ke: **[04c-menyusun-pitch-deck.md](file:///home/iqbaal/gelombang-3/modul 12 bulan/modul-pra-coding-bulan1/4-Pitching-dan-Showcase/04c-menyusun-pitch-deck.md)**
