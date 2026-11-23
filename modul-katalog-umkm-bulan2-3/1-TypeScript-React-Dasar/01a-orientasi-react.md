# 1.0a Orientasi React — Sebelum Mulai Coding

## Tujuan Sesi Ini

Memahami **apa** itu React, **kenapa** kita memilih React (bukan manipulasi DOM biasa seperti di pre-program), dan **bagaimana** struktur proyek `katalog-umkm` yang baru kamu rakit di Bab 0 disusun.

> Sesi ini berfokus pada pembentukan *mental model*, eksplorasi proyek awal, dan tanya jawab di kelas. Belum ada kode fitur baru yang ditulis ke aplikasi Katalog.

---

## Aktivitas Terbimbing di Kelas (Blok 1 — Mini-Lesson ±25 Menit + Eksplorasi)

Mentor akan memandu membaca dan mendiskusikan konsep inti ini bersama:

- Apa itu React dan filosofi pembuatannya.
- Perbedaan SPA (*Single Page Application*) dengan situs web konvensional (*Multi-Page Application*).
- Cara kerja Virtual DOM dan Reconciliation secara visual sederhana.
- Alasan pemilihan **Vite** sebagai dev server modern (jauh lebih cepat dan ringan dibanding Create React App).

*(Bagi yang ingin membaca referensi teoritis lebih mendalam, kamu dapat membaca Bab 1.1 pada Modul Bootcamp React secara mandiri di waktu luang).*

---

## Ringkasan Konsep Kunci & Analogi

### 1. Apa itu React?
React adalah pustaka (*library*) JavaScript khusus untuk membangun antarmuka pengguna (*User Interface* / UI). React fokus pada satu tugas utama: **merender tampilan visual berdasarkan data yang ada**.

| Vanilla JavaScript (Pre-Class) | React (Mulai Bulan 2) |
|---|---|
| Kamu memanipulasi elemen DOM langsung (`document.getElementById`, `innerHTML`). | React yang mengurus DOM — kamu cukup mendeklarasikan: *"Jika datanya seperti ini, tampilkan bentuk seperti itu"*. |
| Jika tombol interaktif bertambah banyak, kode HTML dan JS menjadi kusut. | Antarmuka dipecah menjadi **komponen-komponen kecil** yang rapi dan dapat digunakan ulang. |
| Kamu harus melacak dan memperbarui teks secara manual saat data berubah. | React otomatis merender ulang (*re-render*) bagian tampilan yang berubah. |

### 2. Apa itu SPA (Single Page Application)?

> **Analogi Sehari-hari:**  
> Bayangkan kamu sedang menggunakan aplikasi smartphone (seperti Instagram atau WhatsApp). Saat kamu berpindah dari tab Beranda ke tab Pesan, layarmu tidak mendadak putih atau memuat ulang dari awal; kontennya langsung berganti dengan mulus di layar yang sama.  
> Itulah **SPA**: browser hanya memuat satu file HTML di awal, lalu JavaScript yang mengganti isi tampilannya secara dinamis tanpa pernah me-reload halaman penuh.

### 3. Mengapa Virtual DOM Begitu Cepat?

> **Analogi Sehari-hari:**  
> Bayangkan seorang arsitek yang merawat gedung megah. Jika salah satu lampu di lantai 3 putus, arsitek tidak akan merobohkan seluruh gedung lalu membangunnya lagi dari nol.  
> Arsitek melihat miniatur cetak biru (Virtual DOM) di mejanya, membandingkan mana lampu yang mati (proses *diffing*), lalu menyuruh teknisi mengganti **satu bohlam itu saja** pada gedung nyata (DOM asli).

---

## Mengenal Lingkungan Proyek `katalog-umkm`

Buka proyek `katalog-umkm` yang sudah kamu rakit pada sesi [02-setup-starter.md](../0-Persiapan/02-setup-starter.md).

### 1. Menjalankan Server Lokal

Buka terminal di folder proyek dan jalankan:

```bash
npm run dev
```

Buka `http://localhost:5173` di browser untuk memastikan server Vite berjalan, dan `http://localhost:3001/products` untuk melihat data JSON dari `json-server`.

### 2. Memahami Struktur Folder

```text
katalog-umkm/
├── public/                   # Berkas statis (ikon, favicon, gambar aset)
├── src/                      # Pusat seluruh kode yang akan kita tulis
│   ├── App.tsx               # Komponen induk tempat merangkai halaman
│   ├── config.ts             # Alamat API (VITE_API_URL / http://localhost:3001)
│   ├── main.tsx              # Titik masuk utama aplikasi (entry point)
│   └── index.css             # Berkas gaya tampilan global
├── db.seed.json              # Data acuan awal (4 kategori, 6 produk UMKM)
├── db.json                   # Database aktif json-server (di-ignore Git)
├── .oxlintrc.json            # Aturan pengecekan cepat linter React & TypeScript
├── package.json              # Daftar pustaka & skrip proyek (json-server dikunci di 0.17.4)
├── tsconfig.json             # Pengaturan aturan compiler TypeScript
└── vite.config.ts            # Konfigurasi bundler Vite
```

> **Catatan Penting `json-server` (Port 3001):**  
> Perintah `npm run dev` menjalankan dua hal sekaligus: aplikasi React di port 5173 dan mock API (`json-server`) di port 3001. API palsu ini membaca dan menulis ke file **`db.json`** (yang disalin dari cetakan `db.seed.json` lewat `npm run reset-db`).

---

## Analisis & Prediksi (Aktivitas Blok 2)

Kerjakan bersama pasangan pairing sebelum masuk ke tugas mandiri:

1. **Prediksi Output Terminal:**  
   Buka terminal baru, jalankan `curl http://localhost:3001/products` atau buka URL tersebut di tab browser. Apa format teks yang dikembalikan?
2. **Uji Coba Hot Module Replacement (HMR):**  
   Buka berkas `src/App.tsx`. Ubah teks `"Katalog UMKM"` menjadi `"Katalog Produk UMKM Nusantara"`. Simpan file (`Ctrl+S`).  
   *Pertanyaan:* Apakah browser melakukan refresh penuh (perhatikan ikon reload browser) atau teks langsung berganti seketika?

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan tugas ini secara mandiri di kelas sebagai catatan belajar pribadi. Simpan jawaban di repositori proyekmu pada path:  
`tugas/tugas_01a.md` *(atau sesuai struktur folder arahan mentor)*.

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Tuliskan identitas singkat (Nama, Squad, Tanggal).
3. Jawab 3 pertanyaan pemahaman berikut dengan bahasamu sendiri (maksimal 2-3 kalimat per nomor, jangan menyalin kalimat modul kata-per-kata):
   - **Pertanyaan 1:** Apa perbedaan mendasar antara SPA (*Single Page Application*) dengan website konvensional (*Multi-Page Application*)? Berikan satu contoh pengalaman pengguna di keduanya.
   - **Pertanyaan 2:** Mengapa React menggunakan Virtual DOM dan tidak langsung mengutak-atik DOM browser secara langsung setiap kali ada perubahan data?
   - **Pertanyaan 3:** Di proyek `katalog-umkm`, sebutkan berkas mana yang menjadi "pintu masuk utama" (*entry point*) aplikasi, dan jelaskan apa fungsi `json-server` di port 3001.
4. Lampirkan ringkasan hasil inspeksi dari file `db.seed.json`: sebutkan berapa banyak produk contoh yang tersedia dan sebutkan 4 nama field yang ada di dalamnya.
5. Commit berkas tugas tersebut ke branch baru dan buka PR di GitHub agar rekan satu squad bisa meninjau.

### Contoh Format Hasil (`tugas_01a.md`)

````markdown
# Tugas Mandiri 01a — Orientasi React & Pondasi Proyek
Nama: Ahmad Dahlan
Squad: Squad 2
Tanggal: 3 November 2026

## Jawaban Pertanyaan Pemahaman
1. SPA memuat satu halaman HTML di awal dan mengganti konten lewat JavaScript tanpa refresh, seperti saat berpindah tab di Twitter/X. Website konvensional memuat ulang seluruh halaman dari awal setiap kali kita mengeklik link baru.
2. React memakai Virtual DOM agar tidak boros tenaga. React membandingkan dulu perubahan data di memori tiruan, lalu hanya mengupdate elemen yang benar-benar berubah di browser asli.
3. Pintu masuk utama adalah `src/main.tsx`. Sedangkan `json-server` adalah server API tiruan yang melayani data produk di port 3001 dari `db.json` seolah-olah ada server backend sungguhan.

## Inspeksi `db.seed.json`
- Total produk awal: 6 produk (4 kategori).
- Contoh 4 nama field: `id`, `name`, `price`, `stock`.
````

---

Lanjut ke: **[01b-jsx-dan-komponen-bertipe.md](01b-jsx-dan-komponen-bertipe.md)**
