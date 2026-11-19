# 0.2 Setup Starter Repo

## Tujuan

Repo starter jalan lancar di laptopmu: halaman bertulisan *"Starter siap"* muncul di browser, dan API palsu (`json-server`) juga hidup serta siap melayani data JSON.

---

## Yang Dibutuhkan

- **Node.js** versi **22 LTS** (starter memakai Vite 8 yang mensyaratkan minimal **`^20.19.0` atau `>=22.12.0`**). Cek dengan `node -v`.
- **Git** dan akun **GitHub**.
- Editor kode (**VS Code** sangat direkomendasikan).

> [!IMPORTANT]
> Kalau `node -v` menunjukkan versi di bawah `20.19` (atau di bawah `22.12` pada seri Node 22), pasang/perbarui ke **Node.js 22 LTS** terlebih dahulu di Blok 2 bersama mentor sebelum lanjut.

> [!WARNING]
> **Catatan Penting Versi `json-server` (Terkunci di 0.17.x):**  
> Starter repo mengunci dependensi `"json-server": "0.17.4"`.  
> **Jangan upgrade ke versi 1.x!** Versi 1.x mengubah perilaku query URL (`_limit`, `_sort`, `_order`) dan menghilangkan header pagination `X-Total-Count` yang kita pakai di modul ini.

---

## Langkah demi Langkah

### 1. Dapatkan starter repo (Repo Pribadi vs Squad)
Fork/clone repo starter dari organisasi GitHub kelasmu sesuai arahan mentor:
- **Repo latihan:** Pada Bulan 2–3, setiap murid memiliki salinan/fork repo starter masing-masing agar semua orang mengalami semua tahapan slice secara utuh (tidak menumpang kode teman).
- **Kolaborasi squad:** Anggota satu squad saling menjadi **reviewer Pull Request**, pasangan pairing, dan rekan demo saat Sprint Review Sabtu.

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
2. API palsu (`json-server` 0.17.4) di `http://localhost:3001`

### 4. Periksa di browser
Buka `http://localhost:5173` di browser. Kamu harus melihat:

```text
Katalog UMKM
Starter siap. Mulai dari Slice 0 (lihat README).
```

### 5. Cek API palsu
Buka tab baru di browser dan akses `http://localhost:3001/products`. Kamu harus melihat data JSON berisi daftar 12 produk UMKM contoh.

---

## Daftar Skrip Penting di `package.json`

Kenali perintah-perintah yang sudah disiapkan di starter:

| Perintah | Fungsi |
|---|---|
| `npm run dev` | Menjalankan **Vite frontend (`5173`) + API `json-server` (`3001`) sekaligus** (paling sering dipakai). |
| `npm run dev:web` | Hanya menyalakan frontend Vite saja (API tidak aktif). |
| `npm run dev:api` | Hanya menyalakan mock API `json-server` saja. |
| `npm run reset-db` | Mengembalikan isi `db.json` seperti cetakan awal `db.seed.json`. |
| `npm run lint` | Mengecek kualitas kode & aturan React/TypeScript menggunakan **oxlint**. |
| `npm run build` | Mengecek tipe TypeScript (`tsc -b`) dan mem-build bundle produksi Vite. |

---

## Kalau Data `db.json` Berantakan

Data API palsu disimpan di `db.json`, yang otomatis disalin dari cetakan awal `db.seed.json` saat pertama kali menjalankan `npm run dev`.

Kalau nanti datamu berantakan atau terhapus saat latihan CRUD, kembalikan ke kondisi semula dengan menjalankan:

```bash
npm run reset-db
```

---

## Kenali Struktur Folder Starter

```text
katalog-umkm-starter/
├── CONTRIBUTING.md     # Aturan branch, pesan commit, & checklist review
├── db.seed.json        # Cetakan awal data produk & kategori
├── docs/               # Template kontrak-api.md & decision-log.md (untuk Bulan 3)
└── src/
    ├── main.tsx        # Titik masuk aplikasi (entry point)
    ├── index.css       # File CSS global utama
    ├── App.tsx         # Komponen utama — di sinilah kita mulai merangkai UI
    ├── config.ts       # Mengambil VITE_API_URL atau default http://localhost:3001
    ├── types/          # Tempat definisi tipe TypeScript (Product, Category, dll.)
    └── components/     # Tempat komponen React yang kita buat sendiri
```

---

## Cek Pemahaman & Diagnostik

Jawab pertanyaan ini bersama pasangan pairing di Blok 2:
1. Apa bedanya `npm run dev` dengan `npm run dev:web`?
2. Mengapa versi `json-server` harus tetap `0.17.4` dan tidak boleh di-upgrade ke versi `1.x`?
3. Kalau kamu mengubah isi `db.seed.json`, apakah data yang tampil di aplikasi langsung berubah? Mengapa?

---

## Kesalahan Umum & Solusi

| Gejala | Sebab Biasa | Solusi |
|---|---|---|
| `npm install` atau `npm run dev` error engine / Vite gagal jalan | Node.js di bawah `20.19` atau `22.12` | Update ke **Node.js 22 LTS** via `nvm`/`fnm`. |
| Halaman `localhost:5173` blank putih | Ada error TypeScript/JSX di `App.tsx` atau `main.tsx` | Buka terminal dan console browser (F12), baca baris file yang menyebabkan error. |
| `localhost:3001/products` tidak bisa diakses | `json-server` belum menyala | Pastikan menjalankan `npm run dev`, bukan `npm run dev:web` saja. |
| Query parameter `_sort` / `_limit` tidak bekerja | Sengaja atau tidak sengaja upgrade `json-server` ke versi 1.x | Cek `package.json`, pastikan `"json-server": "0.17.4"`, lalu jalankan `npm install`. |

---

Lanjut ke: **[03-alur-git-dan-pr.md](03-alur-git-dan-pr.md)**
