# 03e. Dari Desain ke Rencana Fitur: Menyusun Backlog Siap Bangun

**Minggu 3: Desain Aplikasi & Bisnis | Sesi 5 (Jumat)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Draf Rencana Fitur (Backlog) & Rincian Slice 0

---

## 1. Mengapa Ini Penting?

Banyak tim pemula memiliki ide cemerlang, gambar wireframe rapi, dan flowchart lengkap, tetapi ketika hari pertama coding tiba di Bulan 2, mereka bingung:
- *"Siapa ngerjain apa dulu ya?"*
- *"Langsung bikin form tambah produk atau bikin tampilan katalog dulu?"*
- *"Kapan sebuah tugas dianggap benar-benar sudah selesai dan siap dites?"*

Hari ini kita akan menerjemahkan gambar wireframe dan flowchart menjadi **Daftar Rencana Fitur (*Product Backlog*)** yang dibagi dalam potongan kerja bertahap yang disebut **Slices**.

---

## 2. Cara Kerja "Potongan Vertikal" (Analogi Kue Lapis)

Di kurikulum ini, kita tidak menggunakan metode lama yang lambat:
```text
Bikin database 1 bulan → Bikin server 1 bulan → Bikin tampilan 1 bulan → Pas digabung ternyata error semua!
```

Kita menggunakan metode **Potongan Vertikal (*Vertical Slicing / Walking Skeleton*)**:
Bayangkan memotong kue lapis dari lapisan atas (cokelat), tengah (krim), sampai lapisan dasar (bolu). Dengan satu irisan tegak lurus, kita bisa langsung mencicipi rasa kuenya secara utuh sejak hari pertama!

```text
                  IRISAN KUE LAPIS (VERTICAL SLICE)
┌────────────────────────────────────────────────────────┐
│ UI (Tampilan Kartu Produk di Layar Browser)            │ ◄── Lapisan Atas (User)
├────────────────────────────────────────────────────────┤
│ Logika Komponen (Filter Kategori & State)              │ ◄── Lapisan Tengah
├────────────────────────────────────────────────────────┤
│ Data (Data Produk Mock / API Sederhana)                │ ◄── Lapisan Bawah (Data)
└────────────────────────────────────────────────────────┘
  ▲
  │ Satu irisan kecil yang langsung bisa diklik & didemokan!
```

> [!NOTE]
> **Istilah Tambahan (Opsional):**  
> Fondasi kerangka awal yang sangat ramping tetapi menghubungkan ujung-ke-ujung antarmuka hingga data sering disebut **Walking Skeleton**.

---

## 3. Rumus Menulis Tugas: User Story & Syarat Selesai

Agar pembagian tugas di tim developer jelas dan tidak ambigu:

### 1. Format Cerita Pengguna (*User Story*):
> *"Sebagai **[Peran Pengguna]**, saya ingin **[Aksi / Tindakan]**, sehingga **[Tujuan / Manfaat]**."*

### 2. Format Syarat Selesai (*Acceptance Criteria*):
Checklist kondisi pengujian nyata (kapan tugas dianggap lulus):
> - *Kondisi 1:* Saat halaman pertama kali dimuat, daftar kartu produk muncul dengan nama, harga, dan foto.
> - *Kondisi 2:* Jika stok bernilai 0, kartu menampilkan tanda "Habis" dan tombol pemesanan tidak aktif.
> - *Kondisi 3:* Jika tombol "Pesan via WhatsApp" diklik, sistem membuka link WhatsApp dengan template pesan yang benar.

---

## 4. Peta Tahapan Slice Mini Katalog UMKM (Bekal Bulan 2)

Berikut adalah rencana irisan kerja kita menuju coding React di Bulan 2:

| # | Tahapan Slice | User Story Inti | Wujud Nyata yang Terlihat |
|---|---|---|---|
| **0** | **Katalog Tampil** | Sebagai pembeli, saya ingin melihat daftar produk UMKM di layar utama agar saya tahu apa saja yang dijual. | Halaman web menampilkan daftar kartu produk rapi dari data lokal mock. |
| **1** | **Katalog Sinkron** | Sebagai pembeli, saya ingin data produk diambil otomatis dari server lokal agar selalu akurat. | Kartu produk termuat dengan indikator loading saat mengambil data. |
| **2** | **Tambah Produk** | Sebagai pedagang, saya ingin memasukkan barang dagangan baru lewat dashboard form agar katalog bertambah. | Form tambah produk dengan validasi angka & harga; produk baru langsung muncul di katalog. |
| **3** | **Kelola & Hapus** | Sebagai pedagang, saya ingin mengubah harga dan menghapus barang dagangan lama agar etalase tetap segar. | Tombol edit & hapus berfungsi dengan konfirmasi modal. |
| **4** | **Pemesanan WhatsApp** | Sebagai pembeli, saya ingin mengklik produk dan meneruskan pesanan otomatis ke WhatsApp penjual. | Halaman detail produk membuka aplikasi WhatsApp dengan pesan rapi. |

---

## 5. Workshop Praktik Squad (60 Menit)

Agar pengerjaan fokus dan mendalam tanpa membebani tim:

1. **Rincikan SLICE 0 Secara Lengkap (35 Menit):**
   - Tuliskan User Story lengkap untuk Slice 0.
   - Hubungkan dengan Wireframe: Tunjukkan bagian kotak mana di wireframe Halaman 1 yang dihidupkan oleh Slice 0.
   - Hubungkan dengan ERD: Atribut apa saja dari entitas `Produk` yang harus ditampilkan di layar?
   - Tuliskan minimal **3 Syarat Selesai (*Acceptance Criteria*)** yang dapat diuji dengan mata.
2. **Rangkum SLICE 1 dan SLICE 2 Secara Ringkas (25 Menit):**
   - Cukup tuliskan **User Story + 2 Syarat Selesai utama** per slice (tidak perlu dokumen panjang).

---

## 6. Output Sesi

Dokumen Markdown squad (`rencana-fitur-backlog.md`) yang berisi:
- Spesifikasi mendalam Slice 0 (User Story, kaitan wireframe/ERD, dan 3 Acceptance Criteria).
- Rangkuman ringkas Slice 1 dan Slice 2.

---

## 7. Tugas Mandiri (Individual)

- **Sifat:** Individu (dikerjakan sendiri di luar jam kelas)
- **Target Waktu:** 25 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_03e.md`

### Instruksi:
1. Pilih satu fitur sederhana: **Pencarian Produk Berdasarkan Nama**.
2. Tuliskan 1 kalimat **User Story** lengkap dengan format: *"Sebagai [peran], saya ingin [aksi], sehingga [manfaat]"*.
3. Tuliskan **2 Syarat Selesai (*Acceptance Criteria*)** yang jelas dan dapat diuji untuk fitur pencarian tersebut.

### Contoh Hasil yang Diharapkan:
```markdown
# Tugas Mandiri 03e — Menulis User Story & Syarat Selesai
Nama: [Nama Kamu]
Fitur: Pencarian Produk di Katalog

## 1. User Story:
Sebagai pembeli lokal, saya ingin mengetikkan nama barang di kolom pencarian, sehingga saya bisa langsung menemukan produk yang saya cari tanpa harus men-scroll seluruh halaman katalog.

## 2. Syarat Selesai (Acceptance Criteria):
1. Ketika pembeli mengetikkan kata kunci (misal: "kripik"), kartu produk yang tampil di layar hanya kartu yang judulnya mengandung kata "kripik".
2. Jika pembeli mengetikkan kata yang tidak ada di daftar produk (misal: "sepatu"), sistem menampilkan teks ramah: "Maaf, produk tidak ditemukan. Coba kata kunci lain."
```

---

## 8. Cek Pemahaman Diri

1. Apa bedanya membagi pekerjaan developer secara horizontal (bikin tampilan dulu berbulan-bulan) vs secara vertikal (*Vertical Slice*)?
2. Mengapa sebuah tugas developer tidak boleh hanya diberi judul pendek *"Bikin Form"* tanpa menuliskan *Acceptance Criteria*?

---

Lanjut ke: **[03f-review-dan-evaluasi-minggu3.md](03f-review-dan-evaluasi-minggu3.md)**
