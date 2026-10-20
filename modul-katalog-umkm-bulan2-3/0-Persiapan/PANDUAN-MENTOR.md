# Panduan Mentor — 0. Persiapan

**Kapan:** hari pertama Bulan 2 (setelah menyelesaikan Bulan 1 Fondasi Pra-Coding), sebelum Slice 0. Alokasi: ±2-3 jam sesi (bisa dipotong jadi 2 sesi).

## Urutan mengajar

1. **01-tentang-modul-ini.md** (10 menit) — jelaskan cara belajar di program ini: produk hidup dari hari 1, bukan kelas teori dulu.
2. **02-setup-starter.md** (30-45 menit, praktik langsung) — pastikan SEMUA peserta berhasil `npm run dev` sebelum lanjut. Ini paling sering jadi titik macet (versi Node, error install).
3. **03-alur-git-dan-pr.md** (30-45 menit, praktik langsung) — peserta sudah tahu Git dasar dari pre-class, tapi alur branch → PR → review → merge di sini biasanya baru buat mereka.
4. **04-format-minta-bantuan.md** (10 menit) — tempel format ini di papan/board, akan dipakai terus 12 bulan.

## Jebakan yang sering muncul

- **Versi Node berbeda-beda di laptop peserta.** Starter diuji dengan Node 22 LTS. Kalau ada yang pakai Node lama (< 20), `npm install` bisa gagal aneh. Siapkan nvm/fnm sebagai solusi cepat.
- **`npm run dev` cuma menjalankan satu proses (Vite) dan API-nya tidak nyala.** Biasanya karena peserta menjalankan `npm run dev:web` saja. Ingatkan: `npm run dev` (tanpa suffix) menjalankan keduanya.
- **Peserta push langsung ke `main`.** Ini momen bagus mengajarkan protected branch / kebiasaan tim, bukan cuma menegur.
- **PR pertama terlalu besar** (semua slice sekaligus). Tegaskan sejak awal: PR kecil, satu potong kerjaan.

## Definisi "siap lanjut ke bab 1"

Semua peserta sudah: repo starter jalan di laptop masing-masing (`npm run dev` menampilkan halaman kosong "Starter siap" di `localhost:5173`), tahu cara membuat branch dan PR, dan hafal format minta bantuan.
