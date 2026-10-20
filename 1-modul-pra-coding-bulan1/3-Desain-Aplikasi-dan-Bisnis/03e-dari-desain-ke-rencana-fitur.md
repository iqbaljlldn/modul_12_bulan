# 03e. Dari Desain ke Rencana Fitur: Menyusun Backlog Siap Bangun

**Minggu 3: Desain Aplikasi & Bisnis | Sesi 5 (Jumat)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Draf Backlog & Slice Roadmap Platform UMKM

---

## 1. Mengapa Ini Penting?

Banyak tim pemula memiliki ide cemerlang, desain wireframe yang rapi, dan flowchart yang lengkap, tapi ketika hari pertama coding tiba di Bulan 2, mereka bingung:
- *"Siapa ngerjain apa dulu ya?"*
- *"Langsung bikin form checkout atau bikin halaman login dulu?"*
- *"Kapan sebuah fitur dianggap sudah selesai dan siap dites?"*

Hari ini kita akan menerjemahkan semua artefak desain dan bisnis yang telah dibuat menjadi **Product Backlog** yang terbagi dalam irisan kerja kecil yang disebut **Slices**.

---

## 2. Konsep "Product Slice" & Walking Skeleton

Di kurikulum ini, kita tidak menggunakan metode jadul:
```text
Bikin database 1 bulan → Bikin API 1 bulan → Bikin tampilan 1 bulan → Pas digabung ternyata error semua!
```

Kita menggunakan metode **Vertical Slicing (Walking Skeleton)**:
Setiap potongan kerja kecil mengiris dari tampilan depan (UI) sampai ke data di belakangnya, sehingga sejak hari pertama ada barang nyata yang bisa diklik dan didemokan.

```text
               KUE LAPIS METAFORA (VERTICAL SLICE)
┌────────────────────────────────────────────────────────┐
│ UI (Tampilan Kartu Produk React)                       │ ◄── Terlihat oleh user
├────────────────────────────────────────────────────────┤
│ Logika Komponen (Filter & State)                       │
├────────────────────────────────────────────────────────┤
│ Data / API (JSON Mock Server)                          │ ◄── Terhubung ke data
└────────────────────────────────────────────────────────┘
  ▲
  │ Satu slice kecil yang langsung bisa dipakai & dites!
```

---

## 3. Menulis User Story & Kriteria Penerimaan (*Acceptance Criteria*)

Agar setiap tugas jelas bagi engineer, kita menuliskannya dalam formula standar industri:

### Format User Story:
> *"Sebagai **[Peran Pengguna]**, saya ingin **[Tindakan/Kemampuan]**, sehingga **[Manfaat/Nilai Bisnis]**."*

### Format Acceptance Criteria (Kapan Fitur Dianggap Selesai):
Gunakan skenario kondisi:
> - *Kondisi 1:* Saat pengguna membuka halaman, sistem menampilkan...
> - *Kondisi 2:* Jika kolom input kosong saat tombol ditekan, sistem menampilkan pesan error...
> - *Kondisi 3:* Jika simpan berhasil, data langsung muncul di daftar...

---

## 4. Peta Slice Mini Katalog UMKM (Bekal Menuju Bulan 2)

Mari kita selaraskan rencana kita dengan kurikulum Bulan 2:

| # | Slice | User Story Inti | Output Nyata yang Terlihat |
|---|---|---|---|
| **0** | **Katalog Tampil** | Sebagai pembeli, saya ingin melihat daftar produk UMKM di layar utama agar saya tahu apa saja yang dijual. | Daftar kartu produk muncul rapi (data mock). |
| **1** | **Katalog dari API** | Sebagai pembeli, saya ingin data produk diambil secara otomatis dari server agar selalu sinkron. | Indikator loading muncul saat memuat data dari API. |
| **2** | **Tambah Produk** | Sebagai merchant, saya ingin memasukkan barang dagangan baru lewat formulir agar katalog saya bertambah. | Form dengan validasi harga & stok; data baru langsung bertambah ke daftar. |
| **3** | **Edit & Hapus** | Sebagai merchant, saya ingin mengubah harga dan menghapus produk lama agar etalase toko selalu akurat. | Tombol edit & hapus berfungsi dengan modal konfirmasi. |
| **4** | **Halaman Detail** | Sebagai pembeli, saya ingin mengklik produk untuk membaca info lengkap dan kontak WA penjual. | Navigasi halaman detail independen per produk. |

---

## 5. Workshop Praktik Squad (60 Menit)

Rincikan **Slice 0, Slice 1, dan Slice 2** ke dalam dokumen kerja teknis:

1. **User Story Lengkap:** Tuliskan untuk setiap slice peran, tindakan, dan tujuannya.
2. **Keterkaitan dengan Wireframe:** Tunjukkan bagian kotak mana pada wireframe Minggu 3 Sesi 03b yang diwakili oleh slice tersebut.
3. **Keterkaitan dengan Flowchart & ERD:** Sebutkan cabang flowchart mana dan entitas data apa yang dihidupkan oleh slice tersebut.
4. **Acceptance Criteria (Checklist Selesai):** Tuliskan minimal 3 kriteria pengujian fungsional per slice.

---

## 6. Output Sesi

Kumpulkan dokumen Markdown (`rencana-fitur-backlog.md`) berisi rincian spesifikasi Slice 0 sampai Slice 2 lengkap dengan *Acceptance Criteria* yang siap dieksekusi di Bulan 2.

---

## 7. Cek Pemahaman Diri

1. Apa bedanya membagi pekerjaan secara horizontal (UI dulu baru Database) vs secara vertikal (*Vertical Slice*)?
2. Mengapa sebuah tugas tidak boleh hanya diberi judul pendek seperti *"Bikin Form"* tanpa ada *Acceptance Criteria*?

Lanjut ke: **[03f-review-dan-evaluasi-minggu3.md](file:///home/iqbaal/gelombang-3/modul 12 bulan/modul-pra-coding-bulan1/3-Desain-Aplikasi-dan-Bisnis/03f-review-dan-evaluasi-minggu3.md)**
