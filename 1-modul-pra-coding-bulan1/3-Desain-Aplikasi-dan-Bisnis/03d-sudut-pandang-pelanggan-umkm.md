# 03d. Sudut Pandang Pelanggan: Persona Berbasis Riset Nyata & Prioritas Fitur

**Minggu 3: Desain Aplikasi & Bisnis | Sesi 4 (Kamis)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Dokumen Persona UMKM (Berbasis Wawancara Nyata) + Daftar Fitur Prioritas

---

## 1. Mengapa Ini Penting?

Bila kamu bertanya ke sembarang orang: *"Kamu mau aplikasi yang seperti apa?"*  
Jawabannya hampir pasti: *"Mau yang serba bisa! Ada game berhadiah, ada live streaming, ada pinjaman modal, ada gratis ongkir!"*

Jika seorang engineer mencoba mengabulkan semua permintaan itu sekaligus:
- Proyek akan macet berbulan-bulan (*scope creep*).
- Aplikasi menjadi terlalu berat dan rumit.
- Produk akhirnya tidak pernah selesai dirilis.

Kunci sukses produk software adalah **fokus tajam pada satu profil pengguna nyata (Persona)** dan **keberanian memprioritaskan fitur mana yang wajib dibangun sekarang vs mana yang ditunda**.

---

## 2. Mengenal User Persona Berbasis Riset Lapangan

**User Persona** adalah representasi ringkas dari sosok pengguna utama yang kita bantu.

> [!IMPORTANT]
> **Aturan Wajib Squad:**  
> Persona yang disusun oleh squad-mu hari ini **wajib berbasis hasil wawancara UMKM nyata** yang telah kalian lakukan di sesi 03c kemarin! Profil "Bu Sri" di bawah ini disajikan sebagai contoh panduan format (ilustrasi pembanding).

### Contoh Format Persona (Ilustrasi Panduan):

```text
┌────────────────────────────────────────────────────────┐
│ PROFIL: Ibu Sri Mulyani (48 Tahun) [ILUSTRASI CONTOH]  │
│ Usaha : Sambal Pecel Madiun "Berkah Ibu"               │
│ Lokasi: Sidoarjo, Jawa Timur                           │
├────────────────────────────────────────────────────────┤
│ Perilaku Teknologi:                                    │
│ - Menggunakan smartphone Android kelas pemula (RAM 3GB)│
│ - Sangat lancar memakai WhatsApp & Facebook            │
│ - Ragu mengklik menu berbahasa Inggris                 │
│ - Mengetik layar HP dengan satu jari telunjuk          │
├────────────────────────────────────────────────────────┤
│ Masalah Terbesar (Pains):                              │
│ - Tiap pagi harus membalas puluhan chat yang sama:     │
│   "Masih ada sambal pedas sedang nggak bu? Harganya?"  │
│ - Sering salah catat pesanan karena chat tertimbun     │
├────────────────────────────────────────────────────────┤
│ Harapan Utama (Gains):                                 │
│ - Punya satu link simpel yang bisa ditaruh di info WA  │
│ - Pembeli langsung lihat daftar menu & stok yang ada   │
└────────────────────────────────────────────────────────┘
```

Saat merancang fitur, kamu tidak lagi bertanya: *"Keren nggak ya kalau ditambah fitur X?"*  
Melainkan: *"Apakah pedagang nyata yang kami wawancarai bisa memakai fitur ini dengan mudah?"*

---

## 3. Prioritas Fitur: Analogi Tas Ransel Mendaki Gunung

Bayangkan kamu akan mendaki gunung dengan tas ransel kecil. Kamu tidak bisa membawa kasur, kulkas, dan sofa sekaligus. Kamu harus memilah barang bawaan dengan tegas:

```text
┌──────────────────────┬────────────────────────────────────────────────────────┐
│ 1. WAJIB ADA (Must)  │ Barang mutlak untuk bertahan hidup. Tanpa ini, jangan  │
│                      │ berangkat!                                             │
│                      │ (Contoh: Menampilkan daftar produk & tombol pesan WA). │
├──────────────────────┼────────────────────────────────────────────────────────┤
│ 2. PENTING (Should)  │ Sangat berguna jika dibawa, tapi masih ada alternatif  │
│                      │ darurat jika belum ada.                                │
│                      │ (Contoh: Filter pencarian kategori produk).            │
├──────────────────────┼────────────────────────────────────────────────────────┤
│ 3. PELENGKAP (Could) │ Menambah kenyamanan jika kapasitas tas masih tersisa.  │
│                      │ (Contoh: Fitur simpan catatan pesanan otomatis).       │
├──────────────────────┼────────────────────────────────────────────────────────┤
│ 4. NANTI DULU (Won't)│ Jangan dibawa sekarang, tinggalkan di rumah!           │
│                      │ (Contoh: Fitur pembayaran kartu kredit, live chat AI). │
└──────────────────────┴────────────────────────────────────────────────────────┘
```

> [!NOTE]
> **Istilah Tambahan (Opsional):**  
> Kerangka pemilahan prioritas (Wajib, Penting, Pelengkap, Nanti Dulu) ini dalam metodologi manajemen produk dikenal dengan singkatan **MoSCoW** (*Must-have, Should-have, Could-have, Won't-have*).

---

## 4. Workshop Praktik Squad (60 Menit)

### Tugas 1: Susun 1 Persona Merchant Berdasarkan Wawancara Nyata
Buka catatan wawancara UMKM dari Sesi 03c kemarin. Susun dokumen persona pedagang nyata yang diwawancarai squad-mu (cantumkan nama asli/inisial, usia, jenis usaha, alat teknologi yang dipakai, penderitaan utama, dan kutipan keluhan aslinya).

### Tugas 2: Pemilahan Fitur Prioritas Platform Tim
1. Kumpulkan ide-ide fitur yang terpikirkan untuk katalog UMKM kalian.
2. Diskusikan dan kelompokkan ide-ide tersebut ke dalam 4 kategori (Wajib Ada, Penting, Pelengkap, Nanti Dulu).
3. **Kunci Maksimal 3 Fitur "Wajib Ada"** untuk scope rilis pertama di Bulan 2:
   - *Fitur 1:* Tampilan Katalog Produk (Foto, Nama, Harga, Stok).
   - *Fitur 2:* Form Tambah/Ubah Produk bagi Pedagang.
   - *Fitur 3:* Tombol Pemesanan Otomatis ke WhatsApp Penjual.

---

## 5. Output Sesi

Dokumen Markdown squad (`persona-dan-prioritas-fitur.md`) yang berisi:
1. Lembar Persona Pedagang UMKM (wajib berbasis hasil wawancara nyata).
2. Tabel Prioritas Fitur dengan alasan mengapa fitur tertentu masuk kategori Wajib Ada vs Nanti Dulu.

---

## 6. Tugas Mandiri (Individual)

- **Sifat:** Individu (dikerjakan sendiri di luar jam kelas)
- **Target Waktu:** 25 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_03d.md`

### Instruksi:
1. Ambil 1 poin penderitaan (*pain point*) terbesar dari pedagang nyata yang diwawancarai squad-mu.
2. Tuliskan dalam 1 halaman ringkas:
   - Apa penderitaan tersebut dan bagaimana cara pedagang mengatasinya saat ini?
   - Mengapa penderitaan tersebut kamu masukkan ke dalam kategori fitur **"Wajib Ada"** untuk diselesaikan oleh aplikasi katalog kita?
   - Berikan 1 usulan desain tombol atau tampilan sederhana yang bisa langsung menghapus rasa sakit tersebut.

### Contoh Hasil yang Diharapkan:
```markdown
# Tugas Mandiri 03d — Analisis Kebutuhan Persona Nyata
Nama: [Nama Kamu]
Narasumber: Ibu Marni (Warung Nasi Gurih & Gorengan)

## 1. Penderitaan Utama:
Bu Marni sering menolak pembeli via WhatsApp karena lontong sayur sudah habis dibeli orang yang datang langsung ke warung. Bu Marni tidak sempat mengetik chat pemberitahuan satu per satu.

## 2. Mengapa Ini Fitur "Wajib Ada":
Tanpa fitur penanda stok habis yang jelas di katalog web, pembeli akan terus merasa kecewa karena sudah capek-capek kirim chat pesanan ternyata makanannya sudah ludes.

## 3. Usulan Solusi Antarmuka:
Pada kartu produk lontong sayur, jika stok diubah menjadi 0 di dashboard, kartu otomatis diberi lapisan abu-abu redup dengan tulisan besar merah: "HABIS HARI INI", dan tombol pesan WA otomatis dinonaktifkan sehingga pembeli tahu sebelum mengirim chat.
```

---

## 7. Cek Pemahaman Diri

1. Mengapa seorang engineer dilarang keras mencoba membuat semua fitur yang diminta pengguna sekaligus pada versi awal aplikasinya?
2. Bagaimana profil persona nyata narasumbermu mempengaruhi keputusan pemilihan ukuran tombol di katalog?

---

Lanjut ke: **[03e-dari-desain-ke-rencana-fitur.md](03e-dari-desain-ke-rencana-fitur.md)**
