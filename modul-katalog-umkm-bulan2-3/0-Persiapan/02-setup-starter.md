# 0.2 Setup Starter Repo

## Tujuan

Repo starter jalan di laptopmu: halaman kosong bertulisan "Starter siap" muncul di browser, dan API palsu (`json-server`) juga hidup.

## Yang dibutuhkan

- **Node.js** versi LTS terbaru (starter diuji dengan Node 22). Cek dengan `node -v`.
- **Git**, dan akun di layanan hosting repo yang dipakai tribe (GitHub/GitLab/dst — sesuai keputusan mentor).
- Editor kode (VS Code direkomendasikan, tapi bebas).

> Kalau `node -v` menunjukkan versi di bawah 20, install ulang Node versi LTS terbaru sebelum lanjut. Jangan dipaksa jalan di versi lama.

## Langkah

1. **Dapatkan starter repo** dari mentor (fork/clone sesuai instruksi mentor — tiap peserta punya repo sendiri).

2. **Install dependency:**

   ```bash
   npm install
   ```

3. **Jalankan:**

   ```bash
   npm run dev
   ```

   Ini menjalankan **dua hal sekaligus**: web (Vite) di `http://localhost:5173` dan API palsu (`json-server`) di `http://localhost:3001`.

4. **Buka `http://localhost:5173` di browser.** Kamu harus melihat:

   ```text
   Katalog UMKM
   Starter siap. Mulai dari Slice 0 (lihat README).
   ```

5. **Cek API palsu juga hidup.** Buka `http://localhost:3001/products` di tab baru — harus muncul data JSON berisi daftar produk.

## Kalau errornya karena file `db.json`

Data API palsu disimpan di `db.json`, yang otomatis dibuat dari `db.seed.json` saat pertama kali `npm run dev`. Kalau datanya berantakan (habis dicoba-coba), jalankan:

```bash
npm run reset-db
```

## Kenali struktur foldernya

```text
src/
├── main.tsx        # titik masuk aplikasi (jangan diubah dulu)
├── App.tsx         # halaman utama — di sinilah kamu mulai coding Slice 0
├── config.ts        # alamat API
├── types/           # tempat tipe data (Product, dll) — masih kosong
└── components/      # tempat komponen — masih kosong
```

## Cek pemahaman

- Apa bedanya `npm run dev` dengan `npm run dev:web`?
- Kalau kamu ubah `db.seed.json`, apakah data yang tampil di aplikasi langsung berubah? Kenapa (atau kenapa tidak)?

## Kesalahan umum

| Gejala | Sebab biasa | Solusi |
|---|---|---|
| `npm install` error panjang soal `node-gyp` atau versi | Node terlalu lama | Update Node ke versi LTS terbaru |
| Halaman `localhost:5173` blank / error merah | Biasanya typo saat nanti mengedit `App.tsx` | Baca error di terminal/browser console, cocokkan baris yang disebut |
| `localhost:3001/products` tidak bisa diakses | `json-server` belum jalan (mungkin cuma jalankan `dev:web`) | Pastikan pakai `npm run dev`, bukan `dev:web` saja |

Lanjut ke: **03-alur-git-dan-pr.md**
