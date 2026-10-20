# 0.4 Format Minta Bantuan

Di tim software, minta bantuan itu **skill**, bukan tanda lemah. Yang bikin beda: cara memintanya.

## Format

```text
Aku mau ...       (apa yang ingin dicapai)
Sudah coba ...    (apa yang sudah dicoba)
Hasilnya ...      (apa yang terjadi — termasuk pesan error lengkap, bukan "error aja")
Dugaanku ...      (menurutmu kira-kira kenapa, meski salah tebak tidak masalah)
```

**Contoh buruk:** "eh kok error ya, tolong dong"

**Contoh baik:**
```text
Aku mau: menampilkan nama produk di kartu.
Sudah coba: pakai {product.name} di JSX.
Hasilnya: muncul error "Cannot read properties of undefined (reading 'name')" di console.
Dugaanku: mungkin product-nya belum ada isinya pas komponen pertama kali render?
```

Yang kedua bisa langsung dibantu dalam hitungan detik. Yang pertama butuh tanya balik dulu.

## Urutan minta bantuan

Kalau macet lebih dari **±20 menit**:

```text
1. Coba sendiri dulu (baca error pelan-pelan, cek dokumentasi)
2. Tanya pasangan (kalau sedang pairing)
3. Tanya squad
4. Tanya Chapter (kalau sudah terbentuk, mulai Bulan 3)
5. Tanya mentor
```

Jangan lompat langsung ke mentor sebelum coba langkah 1-2 — bukan soal aturan kaku, tapi karena proses mencoba sendiri itu sendiri adalah belajar.

## Debug clinic

Kalau macetnya soal bug/error (bukan konsep), coba pola ini dulu sebelum minta bantuan:

1. Baca pesan error **kata per kata** (jangan langsung scroll ke Stack Overflow).
2. Cari baris kode yang disebut di error.
3. `console.log()` nilai yang dicurigai, tepat sebelum baris error.
4. Kalau masih bingung — sekarang baru minta bantuan, dengan format di atas + apa yang sudah kamu temukan dari 3 langkah tadi.

## Cek pemahaman

- Kalau kamu error dan minta bantuan tanpa menyertakan pesan error lengkap, apa yang biasanya terjadi?

---

**Kamu sudah siap.** Lanjut ke folder `1-TypeScript-React-Dasar/01-tipe-dasar-dan-komponen.md`.
