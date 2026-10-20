# 03a. Prinsip UX Dasar: Membangun Aplikasi yang Mudah Dipakai Manusia

**Minggu 3: Desain Aplikasi & Bisnis | Sesi 1 (Senin)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Laporan "UX Review" Singkat Aplikasi Nyata

---

## 1. Mengapa Ini Penting?

Banyak software gagal bukan karena fiturnya kurang banyak atau kodenya lambat, melainkan karena pengguna merasa bingung, frustrasi, lalu menghapus aplikasi tersebut setelah 30 detik pertama:
- *"Tombol bayarnya di mana ya?"*
- *"Kok muter-muter terus nggak ada pemberitahuan apa-apa?"*
- *"Udah ngetik form panjang, pas salah huruf malah kereset semua!"*

Sebagai pembuat software, kamu tidak membuat aplikasi untuk dirimu sendiri. Kamu membuatnya untuk manusia lain dengan berbagai tingkat literasi digital.

Hari ini kita akan membedah **User Experience (UX)** dan memahami prinsip dasar psikologi antarmuka.

---

## 2. UI vs UX: Apa Bedanya?

```text
┌───────────────────────────────────────┬───────────────────────────────────────┐
│        UI (User Interface)            │        UX (User Experience)           │
├───────────────────────────────────────┼───────────────────────────────────────┤
│ "Bagaimana tampilannya terlihat"      │ "Bagaimana rasanya saat digunakan"    │
│ Warna, font, icon, keindahan grafis,  │ Kecepatan alur, kemudahan menemukan   │
│ animasi transisi, konsistensi visual. │ menu, kejelasan pesan error, rasa     │
│                                       │ puas tanpa kebingungan.               │
└───────────────────────────────────────┴───────────────────────────────────────┘
```

> **Analogi Sendok Makan:**  
> Sendok makan berbahan emas berkilau dengan ukiran bunga yang indah adalah **UI yang cantik**.  
> Tetapi jika gagangnya terlalu berat ke belakang dan cekungannya datar sehingga kuah sup selalu tumpah, sendok itu memiliki **UX yang sangat buruk**.

---

## 3. Empat Prinsip Emas UX untuk Aplikasi UMKM

### 1. Hukum Jakob (*Jakob’s Law*)
> *"Pengguna menghabiskan sebagian besar waktu mereka di aplikasi lain, bukan di aplikasimu."*

Jangan membuat tata letak yang aneh-aneh hanya demi terlihat "unik". Jika di hampir semua toko online tombol keranjang ada di pojok kanan atas dan tombol beli ada di bagian bawah layar, ikutilah pola itu! Mengubah pola familiar hanya akan membingungkan pengguna.

### 2. Visibilitas Status Sistem & Feedback Cepat
Sistem harus selalu memberi tahu pengguna apa yang sedang terjadi melalui umpan balik yang jelas dalam waktu wajar.
- Saat tombol "Beli" ditekan: Jangan biarkan layar membeku. Tampilkan animasi loading atau teks *"Sedang memproses pesanan..."*.
- Saat berhasil: Tampilkan centang hijau *"Pesanan berhasil dicatat!"*.
- Saat gagal: Jangan tampilkan *"Error 500"*! Tampilkan *"Koneksi internetmu terputus. Silakan coba lagi."*.

### 3. Hierarki Visual & Fitts's Law
Elemen penting harus lebih mencolok dan mudah disentuh jempol:
- **Tombol Utama (Primary Button):** Ukuran lebih besar, warna tegas dan kontras tinggi (misal: "Konfirmasi Pesanan").
- **Tombol Sekunder (Secondary Button):** Garis tepi saja / warna redup (misal: "Batal").
- Tombol penting di smartphone harus berada di zona jangkauan jempol (*thumb zone*).

### 4. Pencegahan & Pengampunan Kesalahan (*Error Prevention & Recovery*)
- Cegah error sebelum terjadi (misal: jika nomor HP wajib angka, tampilkan keyboard khusus angka di layar ponsel).
- Jika pengguna salah mengisi, jangan kosongkan kembali seluruh form. Beri tanda merah tepat di kolom yang salah disertai petunjuk cara memperbaikinya.

---

## 5. Workshop Praktik Squad (60 Menit)

Tiap squad akan melakukan **Audit UX Sederhana** terhadap 2 aplikasi nyata yang sering dipakai di Indonesia (misal: Tokopedia, Shopee, WhatsApp Bisnis, Sayurbox, atau website dinas pemerintah):

### Panduan Audit:
1. Pilih 1 aplikasi yang menurut timmu memiliki UX **Sangat Nyaman / Hebat**.
2. Pilih 1 aplikasi/website yang menurut timmu memiliki UX **Sangat Membingungkan / Menyebalkan**.
3. Bedah masing-masing aplikasi berdasarkan 4 prinsip di atas. Temukan:
   - 3 hal positif yang membuat aplikasi pertama terasa mulus.
   - 3 hal negatif yang membuat aplikasi kedua membuat jengkel pengguna.
   - Usulan perbaikan konkrit untuk kekurangan tersebut.

---

## 6. Output Sesi: Laporan "UX Review" Squad

Kumpulkan file Markdown singkat berisi:
- Nama aplikasi yang diaudit.
- Bukti tangkapan layar / sketsa bagian antarmuka yang diulas.
- Catatan 3 Temuan Bagus vs 3 Temuan Buruk.
- 1 Pembelajaran UX terpenting yang akan diadopsi ke Platform Katalog UMKM timmu.

---

## 7. Cek Pemahaman Diri

1. Mengapa tombol "Hapus Toko" atau "Hapus Produk" sebaiknya tidak diberi warna mencolok yang sama dengan tombol "Simpan"?
2. Mengapa pengguna paruh baya pemilik UMKM sering takut menekan tombol baru di aplikasi ponsel mereka? Bagaimana prinsip UX mengatasi ketakutan ini?

Lanjut ke: **[03b-wireframe-dan-merancang-tampilan.md](file:///home/iqbaal/gelombang-3/modul 12 bulan/modul-pra-coding-bulan1/3-Desain-Aplikasi-dan-Bisnis/03b-wireframe-dan-merancang-tampilan.md)**
