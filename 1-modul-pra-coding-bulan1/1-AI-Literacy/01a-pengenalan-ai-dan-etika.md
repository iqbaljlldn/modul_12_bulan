# 01a. Pengenalan AI dan Etika

**Minggu 1: AI Literacy | Sesi 1 (Senin)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Piagam Etika AI Tribe (Draft Squad)

---

## 1. Mengapa Ini Penting?

Kecerdasan Buatan (khususnya *Generative AI* seperti ChatGPT, Claude, Gemini, GitHub Copilot) telah mengubah cara kerja industri teknologi secara drastis. Saat ini, programmer profesional memanfaatkan AI setiap hari untuk mempercepat penulisan dokumen, mencari dokumentasi, menemukan bug, hingga mendesain arsitektur sistem.

Namun, di tangan orang yang salah, AI justru menjadi bumerang:
- Membuat orang menjadi malas berpikir kritis.
- Mengikis kemampuan pemecahan masalah (*problem solving*).
- Menghasilkan kode atau keputusan bisnis yang keliru fatal karena menelan "halusinasi" AI bulat-bulat.

Hari ini kita akan memahami cara kerja AI secara realistis dan menyepakati aturan main etis penggunaannya di program ini.

---

## 2. Konsep Inti: Apa Itu AI Sebenarnya?

### 2.1 Bukan Dukun Serba Tahu, Tapi "Mesin Pemprediksi Kata"
Model bahasa besar (*Large Language Models* / LLM) tidak memiliki kesadaran, perasaan, atau pemahaman logis layaknya manusia. Secara sederhana, LLM dilatih dengan membaca triliunan teks di internet untuk mempelajari pola hubungan antar kata.

Saat kamu memberikan pertanyaan:
> *"Ibu kota Indonesia adalah..."*

LLM menghitung secara statistik: kata apa yang paling mungkin muncul berikutnya berdasarkan pola data yang dipelajarinya? Jawabannya adalah *"Jakarta"* (atau *"IKN Nusantara"*).

### 2.2 Apa yang AI Sangat Bagus Lakukan
- **Sintesis & Rangkuman:** Mengubah teks panjang menjadi poin-poin penting.
- **Pencarian Pola & Variasi Ide:** Memberikan 10 opsi ide nama produk, slogan, atau strategi kampanye.
- **Transformasi Format:** Mengubah teks biasa menjadi tabel, format JSON, atau poin presentasi.
- **Penjelasan Berulang Tanpa Lelah:** Menerangkan kembali konsep sulit dengan gaya bahasa berbeda (misal: "jelaskan seperti untuk anak usia 10 tahun").

### 2.3 Apa yang AI Tidak Bisa / Sangat Berbahaya Jika Diandalkan Sendirian
- **Kebenaran Mutlak & Fakta Baru:** AI sering mengalami **Halusinasi** (*hallucination*) — yaitu mengarang fakta, referensi buku, aturan hukum, atau fungsi kode yang sebenarnya tidak pernah ada dengan nada bicara yang sangat meyakinkan.
- **Konteks Lokal Spesifik:** AI tidak tahu kondisi riil pasar becek tempat penjual keripik singkong UMKM binaanmu berjualan, kecuali kamu memberitahukannya secara eksplisit.
- **Pertanggungjawaban Moral:** Jika kamu merilis software yang menghapus saldo pengguna karena mengikuti saran AI, kamu yang dipecat atau digugat, bukan AI-nya.

---

## 3. Garis Batas Etika: Kapan Boleh vs Kapan Dilarang?

| Skenario | Boleh / Direkomendasikan | Dilarang Keras |
|---|---|---|
| **Memahami Konsep Baru** | Minta analogi sederhana: *"Jelaskan apa itu database menggunakan analogi lemari dapur."* | Meng-copy penjelasan AI untuk tugas tanpa membaca dan memahami intinya. |
| **Brainstorming Ide** | Minta opsi: *"Beri 5 ide fitur untuk pedagang pasar tradisional."* | Memilih satu ide tanpa mengkaji apakah pedagang tersebut punya smartphone atau internet. |
| **Penyusunan Kalimat** | Meminta saran tata bahasa: *"Perbaiki kalimat pitch deck ini agar lebih persuasif."* | Mengarang data statistik penjualan fiktif memakai AI. |
| **Pemecahan Masalah (CT)** | Mendiskusikan alternatif alur kerja. | Menyerahkan seluruh perancangan logika ke AI tanpa tahu alur diagramnya. |

> **Prinsip Utama:** Bantuan AI boleh mempercepat eksekusimu, tetapi pemahaman dan keputusan akhir wajib 100% berasal dari kepalamu sendiri.

---

## 4. Workshop Praktik: Kasus Dilema Etis (60 Menit)

Berkumpullah bersama squad-mu. Diskusikan 3 kasus di bawah ini:

### Kasus A: "Tugas Presentasi Kilat"
Andi mendapat tugas membuat presentasi profil UMKM binaan. Karena kehabisan waktu, Andi memasukkan prompt: *"Buatkan slide lengkap profil pengrajin batik Pak Joko di Solo beserta omzetnya."* AI memberikan data lengkap termasuk estimasi omzet Rp 50 juta/bulan. Andi langsung menempelkannya ke slide tanpa bertanya ke Pak Joko aslinya.
- *Pertanyaan Diskusi:* Apa kesalahan fatal Andi? Apa dampaknya bagi bisnis Pak Joko? Bagaimana seharusnya Andi menggunakan AI dalam kasus ini?

### Kasus B: "Copy-Paste Pembawa Petaka"
Siti meminta AI membuatkan aturan diskon untuk aplikasi katalog. AI menyarankan kode logika diskon beli 2 gratis 1, namun ada bug tersembunyi yang membuat pembeli bisa mendapat barang gratis tanpa batas. Siti tidak membaca teliti dan langsung menyetujui alur tersebut.
- *Pertanyaan Diskusi:* Siapa yang bersalah jika toko mengalami kerugian besar? Apa pelajaran tentang verifikasi logika?

### Kasus C: "Transparansi ke Mentor"
Budi menyelesaikan tugas dekomposisi masalah dalam waktu 15 menit dengan bantuan prompt terstruktur ke Claude. Budi menyertakan tangkapan layar prompt dan menjelaskan secara lisan bagian mana yang merupakan hasil brainstorming AI dan bagian mana yang merupakan keputusan timnya.
- *Pertanyaan Diskusi:* Apakah tindakan Budi etis? Mengapa transparansi proses lebih dihargai daripada hasil instan tanpa jejak?

---

## 5. Output Sesi: Draft "Piagam Etika AI Tribe"

Tiap squad wajib menyusun **5 Butir Kesepakatan Etika Penggunaan AI** yang akan berlaku selama 12 bulan ke depan.

Contoh format:
```markdown
# Piagam Etika AI — Squad [Nama Squad]
1. Kami berjanji tidak akan menyalin (copy-paste) teks dari AI tanpa membaca, memahami, dan memvalidasinya secara sadar.
2. Kami akan selalu mencantumkan dan mendokumentasikan prompt penting yang kami gunakan dalam proses penyelesaian tugas tim.
3. Jika AI memberikan data statistik atau fakta empiris, kami wajib melakukan verifikasi silang (cross-check) ke sumber primer.
4. Kami menggunakan AI sebagai alat pemantik diskusi dan sparring partner, bukan pengganti proses berpikir anggota tim.
5. Kami bertanggung jawab penuh 100% atas setiap dokumen, desain, dan kode yang kami serahkan ke mentor.
```

Kumpulkan draf ini ke mentor untuk digabungkan menjadi **Piagam Etika AI Tribe resmi**.

---

## 6. Cek Pemahaman Diri

Sebelum mengakhiri sesi, jawablah dalam hati:
1. Mengapa LLM bisa menjawab pertanyaan yang salah dengan bahasa yang sangat yakin?
2. Jika mentormu menanyakan: *"Jelaskan kenapa alur ini memilih percabangan X?"*, apakah kamu bisa menjawabnya tanpa membuka riwayat chat AI-mu?

Lanjut ke: **[01b-ct-dan-problem-solving-dengan-ai.md](file:///home/iqbaal/gelombang-3/modul%2012%20bulan/modul-pra-coding-bulan1/1-AI-Literacy/01b-ct-dan-problem-solving-dengan-ai.md)**
