# 0.2 Setup Starter Repo

## Tujuan

Repo starter jalan di laptopmu: halaman bertulisan "Starter siap" muncul di browser, dan API palsu (`json-server`) juga hidup dan siap melayani data.

---

## Yang Dibutuhkan

- **Node.js** versi LTS terbaru (starter diuji dengan Node 22). Cek dengan `node -v`.
- **Git**, dan akun di GitHub/GitLab (sesuai instruksi mentor).
- Editor kode (VS Code sangat direkomendasikan).

> [!IMPORTANT]
> Kalau `node -v` menunjukkan versi di bawah 20, install ulang Node versi LTS terbaru sebelum lanjut. Jangan dipaksa jalan di versi lama karena Vite dan TypeScript modern butuh Node 20+.

> [!WARNING]
> **Catatan Penting Versi `json-server` (Terkunci di 0.17.x):**
> Starter repo kita sengaja mengunci dependensi `"json-server": "0.17.4"`.
> **Jangan upgrade ke versi 1.x!** Versi 1.x mengubah perilaku query URL (seperti `_limit`, `_sort`, `_order`) dan menghilangkan header pagination `X-Total-Count` yang kita gunakan untuk fitur pencarian, filter, dan pagination di modul ini.

---

## Langkah demi Langkah

### 1. Dapatkan starter repo
Fork/clone repo starter dari organisasi GitHub kelasmu sesuai arahan mentor (tiap murid punya repo sendiri untuk latihan, lalu berkolaborasi di repo squad).

### 2. Masuk ke folder proyek dan pasang dependensi

```bash
cd katalog-umkm-starter
npm install
```

### 3. Jalankan server lokal

```bash
npm run dev
```

Skrip ini menjalankan **dua proses sekaligus** secara otomatis:
1. Web frontend (Vite) di `http://localhost:5173`
2. API palsu (`json-server` 0.17.x) di `http://localhost:3001`

### 4. Periksa di browser
Buka `http://localhost:5173` di browser. Kamu harus melihat:

```text
Katalog UMKM
Starter siap. Mulai dari Slice 0 (lihat README).
```

### 5. Cek API palsu
Buka tab baru di browser dan akses `http://localhost:3001/products`. Kamu harus melihat data JSON berisi daftar produk UMKM contoh.

---

## Kalau Error karena File `db.json`

Data API palsu disimpan di `db.json`, yang otomatis dibuat dari cetakan awal `db.seed.json` saat pertama kali `npm run dev`.

Kalau nanti datamu berantakan atau terhapus habis dicoba-coba, kembalikan ke kondisi semula dengan menjalankan:

```bash
npm run reset-db
```

---

## Kenali Struktur Folder Starter

```text
src/
├── main.tsx        # Titik masuk aplikasi (entry point)
├── App.tsx         # Komponen utama — di sinilah kita mulai merangkai UI
├── config.ts       # Menyimpan alamat API (http://localhost:3001)
├── types/          # Tempat definisi tipe TypeScript (Product, Category, dll.)
└── components/     # Tempat komponen React yang kita buat sendiri
```

---

## Cek Pemahaman & Diagnostik

Jawab pertanyaan ini bersama pasangan pairing di Blok 2:
1. Apa bedanya `npm run dev` dengan `npm run dev:web`?
2. Mengapa versi `json-server` harus tetap 0.17.x dan tidak boleh di-upgrade ke versi 1.x?
3. Kalau kamu mengubah isi `db.seed.json`, apakah data di aplikasi langsung berubah? Mengapa (atau mengapa tidak)?

---

## Kesalahan Umum & Solusi

| Gejala | Sebab Biasa | Solusi |
|---|---|---|
| `npm install` error panjang soal `node-gyp` atau engine | Node.js terlalu lama (< 20) | Update Node.js ke versi LTS terbaru (22 LTS direkomendasikan). |
| Halaman `localhost:5173` blank putih | Ada error kompilasi di `App.tsx` atau `main.tsx` | Buka terminal dan console browser (F12), baca baris file yang menyebabkan error. |
| `localhost:3001/products` tidak bisa diakses | `json-server` belum hidup | Pastikan menjalankan `npm run dev`, bukan `npm run dev:web` saja. |
| Query parameter `_sort` / `_limit` tidak bekerja | Sengaja atau tidak sengaja upgrade `json-server` ke versi 1.x | Cek `package.json`, pastikan `"json-server": "0.17.4"`, lalu jalankan `npm install`. |

---

Lanjut ke: **03-alur-git-dan-pr.md**
