# 03a. Prinsip UX Dasar: Membangun Aplikasi yang Mudah Dipakai Manusia

**Minggu 3: Desain Aplikasi & Bisnis | Sesi 1 (Senin)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Laporan "UX Review" Singkat Aplikasi Nyata

---

## 1. Mengapa Ini Penting?

Banyak aplikasi gagal bukan karena fiturnya kurang canggih atau kodenya lambat, melainkan karena pengguna merasa bingung, frustrasi, lalu menutup aplikasi tersebut dalam 30 detik pertama:
- *"Tombol pesannya di mana ya?"*
- *"Kok muter-muter terus nggak ada keterangan apa-apa?"*
- *"Udah capek-capek ngetik form panjang, pas salah satu huruf malah kereset semua!"*

Sebagai pembuat software, kamu tidak membuat aplikasi untuk dirimu sendiri. Kamu membuatnya untuk manusia lain dengan berbagai tingkat literasi teknologi.

Hari ini kita akan membedah **User Experience (UX)** dan memahami prinsip dasar psikologi antarmuka manusia.

---

## 2. UI vs UX: Apa Bedanya?

```text
┌───────────────────────────────────────┬───────────────────────────────────────┐
│        UI (User Interface)            │        UX (User Experience)           │
├───────────────────────────────────────┼───────────────────────────────────────┤
│ "Bagaimana tampilannya terlihat"      │ "Bagaimana rasanya saat digunakan"    │
│ Warna, font, icon, keindahan visual,  │ Kecepatan alur, kemudahan menemukan   │
│ animasi transisi, konsistensi tombol. │ menu, kejelasan pesan error, rasa     │
│                                       │ puas tanpa kebingungan.               │
└───────────────────────────────────────┴───────────────────────────────────────┘
```

> **Analogi Sendok Makan:**  
> Sendok makan berbahan emas berkilau dengan ukiran bunga indah adalah **UI yang cantik**.  
> Tetapi jika gagangnya terlalu berat ke belakang dan cekungannya sangat ceper sehingga kuah sup selalu tumpah saat disendok, sendok itu memiliki **UX yang sangat buruk**.

---

## 3. Empat Prinsip Emas UX untuk Aplikasi UMKM

### 1. Prinsip Kebiasaan Pengguna (Jangan Bikin Pusing dengan Pola Aneh)
> *"Orang terbiasa dengan pola yang sering mereka temui di aplikasi lain."*

Jangan membuat tata letak yang aneh-aneh hanya demi terlihat "beda". Jika di hampir semua aplikasi tombol keranjang/pesanan ada di pojok kanan atau di bawah layar ponsel, ikutilah pola itu! Mengubah pola yang sudah mendarah daging hanya akan membuat pengguna merasa tersesat.

### 2. Prinsip Tombol Mudah Dijangkau Jempol (Hierarki Ukuran & Jarak)
> *"Semakin penting sebuah tindakan, semakin besar tombolnya dan semakin dekat dengan jangkauan jempol."*

- **Tombol Utama (Call to Action / CTA):** Harus berukuran paling besar dengan warna kontras tegas (misal: tombol hijau besar *"Pesan via WhatsApp"*).
- **Tombol Sekunder:** Cukup garis tepi atau warna redup (misal: tombol *"Batal"*).
- Karena pengguna membuka katalog di layar smartphone sambil memegang HP dengan satu tangan, letakkan tombol aksi di zona jangkauan jempol (*thumb zone*) di bagian bawah layar.

### 3. Visibilitas Status Sistem (Beri Kabar Cepat)
Sistem harus selalu memberi tahu pengguna apa yang sedang terjadi melalui umpan balik yang jelas dan wajar:
- Saat tombol ditekan: Tampilkan teks *"Sedang membuka WhatsApp..."* atau indikator loading. Jangan biarkan layar membeku tanpa respon.
- Saat sukses: Tampilkan centang hijau jelas.
- Saat error: Jangan tampilkan kode teknis asing seperti *"Error 500"*! Tampilkan pesan ramah: *"Koneksi internetmu terputus. Silakan coba kirim ulang."*

### 4. Pencegahan & Pengampunan Kesalahan (*Error Prevention*)
- Cegah error sebelum terjadi: Jika kolom nomor WhatsApp hanya boleh angka, langsung munculkan keyboard angka di layar ponsel pengguna.
- Jika pengguna salah mengisi form, jangan mengosongkan kembali kolom lain yang sudah diketik dengan susah payah. Beri penanda merah tepat di kolom yang salah disertai petunjuk cara membenarkannya.

---

> [!NOTE]
> **Istilah Tambahan / Referensi Desain (Opsional):**  
> Di dunia profesional UI/UX, Prinsip Kebiasaan Pengguna dikenal sebagai **Hukum Jakob (*Jakob’s Law*)**, sedangkan prinsip ukuran dan jangkauan tombol dikenal sebagai **Hukum Fitts (*Fitts’s Law*)**.

---

## 4. Workshop Praktik Squad (60 Menit)

Tiap squad akan melakukan **Audit UX Sederhana** terhadap 2 aplikasi nyata yang sering dipakai di Indonesia (misal: WhatsApp Bisnis, Tokopedia, Shopee, Sayurbox, atau website dinas publik):

### Panduan Audit Tim:
1. Pilih 1 aplikasi yang menurut timmu memiliki UX **Sangat Nyaman / Enak Digunakan**.
2. Pilih 1 aplikasi/website yang menurut timmu memiliki UX **Sangat Membingungkan / Menjengkelkan**.
3. Bedah kedua aplikasi tersebut menggunakan 4 prinsip emas di atas:
   - Temukan 3 hal positif yang membuat aplikasi pertama terasa nyaman.
   - Temukan 3 hal negatif yang membuat aplikasi kedua membuat jengkel pengguna.
   - Tuliskan 1 saran perbaikan konkret untuk kekurangan tersebut.

---

## 5. Output Sesi

Kumpulkan dokumen Markdown laporan UX Review squad berisi:
- Nama kedua aplikasi yang diulas.
- Bukti tangkapan layar bagian antarmuka yang dibahas.
- Catatan 3 Temuan Positif vs 3 Temuan Menjengkelkan.
- 1 Pembelajaran UX terpenting yang akan diterapkan pada Platform Katalog UMKM timmu.

---

## 6. Tugas Mandiri (Individual)

- **Sifat:** Individu (dikerjakan sendiri di luar jam kelas)
- **Target Waktu:** 20 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_03a.md`

### Instruksi:
1. Amati orang tua, saudara, atau tetangga di sekitarmu saat mereka sedang menggunakan smartphone mereka (atau refleksikan pengalaman pribadimu).
2. Temukan **1 momen di mana mereka sempat bingung, salah pencet, atau mengeluh** saat memakai sebuah aplikasi.
3. Tuliskan dalam 3 poin:
   - Apa aplikasi yang digunakan dan apa yang ingin mereka lakukan?
   - Mengapa antarmuka aplikasi tersebut membingungkan mereka?
   - Bagaimana solusi perbaikan tombol/tata letak yang lebih ramah pengguna?

### Contoh Hasil yang Diharapkan:
```markdown
# Tugas Mandiri 03a — Observasi Hambatan UX
Nama: [Nama Kamu]

## 1. Situasi Pengamatan:
Ibu saya ingin mencari resep opor ayam di sebuah website resep masakan lokal.

## 2. Masalah UX yang Ditemukan:
Ketika membuka halaman, layar langsung tertutup 3 jendela pop-up iklan yang bertumpuk. Tombol tanda silang (X) untuk menutup iklan sangat kecil di pojok kanan atas, sehingga ibu saya berulang kali salah memencet iklan dan terlempar ke halaman lain. Ibu saya langsung merasa panik dan mengira HP-nya terkena virus.

## 3. Solusi Perbaikan Berdasarkan Prinsip UX:
Jangan memasang iklan menutupi konten utama. Jika ada jendela pemberitahuan, tombol tutup (X) harus berukuran minimal 44x44 pixel dan kontras jelas agar mudah disentuh jari pengguna paruh baya.
```

---

## 7. Cek Pemahaman Diri

1. Mengapa tombol penting seperti *"Pesan via WhatsApp"* harus diletakkan di bagian bawah layar smartphone (bukan di pojok atas)?
2. Mengapa menampilkan kode error teknis seperti *"Error 404"* sangat buruk bagi pengalaman pengguna awam UMKM?

---

Lanjut ke: **[03b-wireframe-dan-merancang-tampilan.md](03b-wireframe-dan-merancang-tampilan.md)**
