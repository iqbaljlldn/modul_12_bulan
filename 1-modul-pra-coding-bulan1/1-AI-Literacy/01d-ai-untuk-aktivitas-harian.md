# 01d. AI untuk Aktivitas Harian & Proyek Kreatif UMKM

**Minggu 1: AI Literacy | Sesi 4 (Kamis)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Draf Solusi Operasional UMKM (Berbasis Asumsi) + Rencana Riset Lapangan

---

## 1. Mengapa Ini Penting?

Banyak pelaku UMKM di Indonesia adalah *solopreneur* (dijalankan seorang diri) atau usaha keluarga kecil: mereka memasak sendiri, melayani pembeli sendiri, mencatat stok di buku tulis lecek, dan membalas chat WhatsApp pembeli satu per satu hingga larut malam.

Bagi mereka, AI bisa menjadi "asisten magang serba bisa" tanpa biaya jika mereka tahu cara mengarahkannya dengan benar.

Hari ini, squad-mu bertindak sebagai konsultan teknologi pemula untuk UMKM. Kamu akan mempraktikkan bagaimana AI mempercepat penulisan deskripsi katalog produk dan standar layanan, sekaligus belajar **menandai dengan jujur mana data yang merupakan asumsi sementara** sebelum nantinya divalidasi ke pelaku UMKM nyata di lapangan.

---

## 2. Empat Bidang Aplikasi AI untuk UMKM

```text
┌────────────────────────────────────────────────────────┐
│             AI SEBAGAI ASISTEN OPERASIONAL             │
├──────────────────────────┬─────────────────────────────┤
│ 1. Riset Awal & Pola     │ 2. Pembuatan Konten Produk  │
│    Melihat variasi menu, │    Deskripsi katalog rapi,  │
│    tren minat pembeli    │    kejelasan varian & harga │
├──────────────────────────┼─────────────────────────────┤
│ 3. Perencanaan Sederhana │ 4. Standardisasi Pesan WA   │
│    Jadwal harian toko,   │    Template balas pesan,    │
│    pengingat stok habis  │    respons ramah komplain   │
└──────────────────────────┴─────────────────────────────┘
```

> [!WARNING]
> **Prinsip Kejujuran Data (Tandai Sebagai Asumsi):**  
> Di sesi ini kita menggunakan profil UMKM binaan percontohan. Semua data harga, perkiraan omzet, atau kebiasaan pembeli yang kamu diskusikan bersama AI **wajib diberi label tegas: [ASUMSI SQUAD]**, sampai squad-mu melakukan wawancara nyata dengan pelaku UMKM di sekitar tempat tinggalmu pada Minggu 3!

---

## 3. Langkah Kerja Workshop Tim (60 Menit)

Tiap squad memilih **1 Profil UMKM Binaan Percontohan**:
- **Pilihan A: Dapur Sambal Mak Inem** (Kuliner rumahan sambal botol khas Jawa Timur).
- **Pilihan B: Kerajinan Anyaman Bambu Pak Tirto** (Produk kriya rumah tangga dan suvenir bambu).
- **Pilihan C: Kopi Susu Gang Buntu** (Kedai kopi gerobakan dekat kampus).

*(Catatan: Profil di atas adalah studi kasus percontohan. Beri tanda [ASUMSI] pada seluruh data angka yang digunakan).*

### Alur Kerja Squad:
1. **Langkah 1: Menentukan 2 Kebutuhan Utama (10 Menit)**  
   Pilih 2 hal operasional yang ingin diselesaikan:
   - Contoh: Menulis 3 deskripsi produk katalog yang menggugah selera + Membuat 1 template pesan WhatsApp untuk konfirmasi pesanan masuk.
2. **Langkah 2: Eksekusi Prompting R-C-I-C-O (25 Menit)**  
   Gunakan formula R-C-I-C-O dari Sesi 01c. Catat prompt yang dikirim dan hasil respon dari AI.
3. **Langkah 3: Kurasi Manusia & Coret Halusinasi (15 Menit)**  
   Coret saran AI yang tidak realistis untuk pedagang kecil (misal: AI menyarankan kemasan kaleng bersegel vakum mahal untuk warung sambal kecil). Sesuaikan gaya bahasa agar tetap ramah dan membumi.
4. **Langkah 4: Tinjau Rencana Wawancara Nyata (10 Menit)**  
   Ingat bahwa di Minggu 3 nanti, tiap squad wajib mewawancarai 1 pelaku UMKM nyata di sekitar. Diskusikan calon warung/toko di dekat tempat tinggal anggota tim yang bisa didatangi.

---

## 4. Output Sesi

Kumpulkan satu file Markdown (`studi-kasus-umkm-asumsi.md`) berisi:
1. Profil UMKM percontohan yang dipilih (lengkap dengan label `[ASUMSI]`).
2. Teks prompt formula R-C-I-C-O yang digunakan tim.
3. Hasil akhir: 3 deskripsi produk katalog + 1 template pesan balasan WhatsApp yang sudah dikurasi manusia.
4. Catatan kurasi: 2 hal aneh/halusinasi dari AI yang sengaja dibuang oleh squad beserta alasannya.

---

## 5. Tugas Mandiri (Individual)

- **Sifat:** Individu (dikerjakan sendiri di luar jam kelas)
- **Target Waktu:** 25 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_01d.md`

### Instruksi:
1. Pikirkan satu produk makanan/minuman yang sering kamu beli di dekat rumahmu (misal: pisang goreng Bu Ani, es teh manis, atau nasi goreng Mas Doni).
2. Tuliskan deskripsi produk tersebut yang saat ini ada di kepalamu (biasanya sangat singkat).
3. Buat prompt formula R-C-I-C-O ke AI untuk membuatkan deskripsi katalog produk yang menarik (maksimal 3-4 kalimat ringkas, sebutkan bahan, rasa, dan harga terjangkau).
4. Edit hasilnya sendiri: buang kalimat lebay/berlebihan yang tidak sesuai dengan warung aslinya.

### Contoh Hasil yang Diharapkan:
```markdown
# Tugas Mandiri 01d — Kurasi Deskripsi Produk
Nama: [Nama Kamu]
Produk: Pisang Goreng Crispy "Warung Bu Ani"

## 1. Deskripsi Awal Saya:
Pisang goreng manis enak anget harga dua ribu sebiji.

## 2. Prompt R-C-I-C-O:
[Role] Copywriter kuliner lokal Indonesia.
[Context] Warung Bu Ani berjualan di pinggir jalan perkampungan, pembeli utamanya warga sekitar yang mencari camilan sore.
[Instruction] Tulis deskripsi produk singkat untuk kartu katalog online.
[Constraint] Maksimal 3 kalimat, gaya bahasa ramah sehari-hari, jangan pakai kata puitis lebay.
[Output] 1 paragraf pendek + info harga.

## 3. Hasil Kurasi Mandiri:
Pisang kepok manis pilihan digoreng hangat dengan balutan tepung renyah keemasan. Pas dinikmati bersama secangkir kopi atau teh di sore hari. Hanya Rp 2.000 per potong, selalu fresh setiap sore!
```

---

## 6. Cek Pemahaman Diri

1. Mengapa gaya bahasa hasil copywriting murni dari AI sering terasa kaku dan perlu sentuhan kurasi manusia?
2. Mengapa kita wajib menandai profil studi kasus fiktif sebagai `[ASUMSI]` sebelum melakukan wawancara lapangan nyata?

---

Lanjut ke: **[01e-ai-untuk-belajar-mandiri.md](01e-ai-untuk-belajar-mandiri.md)**
