# 0.2 Rakit Pondasi Proyek (Vite + React + Mock API)

> [!NOTE]
> **Tanpa Starter Pack Jadi:** Di sesi ini, kamu **merakit sendiri pondasi proyek** dari nol menggunakan Vite, React, TypeScript, `json-server`, dan `oxlint`. Dengan merakitnya sendiri, kamu paham persis fungsi setiap folder, skrip, dan konfigurasi sebelum mulai coding Slice 0.

## Tujuan

Proyek `katalog-umkm` berdiri di laptopmu dari nol, terhubung ke GitHub, menampilkan halaman pembuka di browser (`http://localhost:5173`), dan API palsu (`json-server` di `http://localhost:3001`) siap melayani data JSON.

---

## Yang Dibutuhkan

- **Node.js** versi **26** (Vite 8 mensyaratkan minimal **`^20.19.0` atau `>=22.12.0`**). Cek dengan `node -v`.
- **Git** dan akun **GitHub**.
- Editor kode (**VS Code** sangat direkomendasikan).

> [!IMPORTANT]
> Kalau `node -v` menunjukkan versi di bawah `20.19` (atau di bawah `22.12` pada seri Node 22), perbarui ke **Node.js 26** terlebih dahulu di Blok 2 bersama mentor sebelum lanjut.

> [!WARNING]
> **Kunci Versi `json-server` di `0.17.4`!**  
> Saat memasang nanti, wajib tulis `@0.17.4` (`npm install -D json-server@0.17.4`).  
> **Jangan upgrade ke versi `1.x`!** Versi `1.x` mengubah perilaku parameter URL (`_limit`, `_sort`, `_order`) dan menghilangkan header `X-Total-Count` yang kita pakai di Bulan 3.

---

## Langkah demi Langkah Merakit Proyek (45–60 Menit)

### 1. Buat Proyek React + TypeScript dengan Vite
Buka terminal di folder kerjamu, lalu jalankan:

```bash
npm create vite@latest katalog-umkm -- --template react-ts
cd katalog-umkm
npm install
```

### 2. Pasang Mock API, `concurrently`, dan Linter (`oxlint`)
Jalankan perintah berikut tepat sesuai versinya:

```bash
npm install -D json-server@0.17.4 concurrently oxlint
```

- `json-server@0.17.4`: server REST API palsu berbasis file JSON lokal.
- `concurrently`: menjalankan server web Vite dan mock API bersamaan dalam 1 perintah terminal.
- `oxlint`: linter super cepat untuk mengecek bug React Hooks & TypeScript.

### 3. Atur `.gitignore` dan Skrip di `package.json`
1. Buka `.gitignore` dan tambahkan dua baris berikut di bagian paling bawah agar data percobaan dan variabel rahasia tidak ikut ter-commit:
   ```text
   db.json
   .env
   ```
2. Buka `package.json`, lalu lengkapi bagian `"scripts"` menjadi seperti ini:
   ```json
   "scripts": {
     "dev": "concurrently -n web,api -c cyan,yellow \"vite\" \"json-server --watch db.json --port 3001\"",
     "dev:web": "vite",
     "dev:api": "json-server --watch db.json --port 3001",
     "reset-db": "node -e \"import('node:fs').then(f => f.copyFileSync('db.seed.json', 'db.json'))\"",
     "build": "tsc -b && vite build",
     "lint": "oxlint",
     "preview": "vite preview"
   }
   ```

| Perintah | Fungsi |
|---|---|
| `npm run dev` | Menjalankan **Vite frontend (`5173`) + API `json-server` (`3001`) sekaligus** (paling sering dipakai). |
| `npm run dev:web` | Hanya menyalakan frontend Vite saja (API tidak aktif). |
| `npm run dev:api` | Hanya menyalakan mock API `json-server` saja. |
| `npm run reset-db` | Mengembalikan isi `db.json` ke kondisi awal dari `db.seed.json`. |
| `npm run lint` | Mengecek kualitas kode & aturan React Hooks menggunakan `oxlint`. |
| `npm run build` | Mengecek tipe TypeScript (`tsc -b`) dan mem-build bundle produksi Vite. |

### 4. Buat Konfigurasi `oxlint` dan `src/config.ts`
1. Buat file `.oxlintrc.json` di folder root proyek:
   ```json
   {
     "$schema": "./node_modules/oxlint/configuration_schema.json",
     "plugins": ["react", "typescript", "oxc"],
     "rules": {
       "react/rules-of-hooks": "error",
       "react/only-export-components": ["warn", { "allowConstantExport": true }]
     }
   }
   ```
2. Buat file `src/config.ts` untuk menyimpan alamat API:
   ```ts
   // Bulan 2-3 memakai mock API lokal (port 3001). Bulan 4 diganti alamat NestJS lewat .env
   export const API_URL: string = import.meta.env.VITE_API_URL ?? 'http://localhost:3001'
   ```
3. Siapkan folder kosong `src/types/`, `src/components/`, dan `docs/` untuk sesi berikutnya.

### 5. Buat Data Awal (`db.seed.json` → `db.json`)
Buat file `db.seed.json` di folder root proyek dan salin data acuan berikut (menggunakan format `snake_case` pada nama field agar konsisten dengan kontrak database):

```json
{
  "categories": [
    { "id": 1, "name": "Kuliner" },
    { "id": 2, "name": "Kerajinan" },
    { "id": 3, "name": "Fashion" },
    { "id": 4, "name": "Pertanian" }
  ],
  "products": [
    {
      "id": 1,
      "name": "Keripik Tempe Original",
      "description": "Keripik tempe renyah tanpa pengawet, kemasan 250 gram.",
      "price": 18000,
      "stock": 120,
      "status": "active",
      "category_id": 1,
      "merchant_name": "Dapur Bu Sari",
      "created_at": "2026-01-12T08:00:00Z"
    },
    {
      "id": 2,
      "name": "Sambal Bawang Botol",
      "description": "Sambal bawang pedas gurih, tahan 3 bulan, isi 200 gram.",
      "price": 25000,
      "stock": 60,
      "status": "active",
      "category_id": 1,
      "merchant_name": "Dapur Bu Sari",
      "created_at": "2026-01-12T08:10:00Z"
    },
    {
      "id": 3,
      "name": "Brownies Kukus Cokelat",
      "description": "Brownies kukus lembut, satu loyang isi 8 potong.",
      "price": 35000,
      "stock": 25,
      "status": "draft",
      "category_id": 1,
      "merchant_name": "Kue Mbak Rina",
      "created_at": "2026-01-20T10:00:00Z"
    },
    {
      "id": 4,
      "name": "Tas Anyaman Pandan",
      "description": "Tas anyaman pandan dengan lapisan kain, ukuran sedang.",
      "price": 120000,
      "stock": 15,
      "status": "active",
      "category_id": 2,
      "merchant_name": "Anyaman Nusa",
      "created_at": "2026-02-02T07:45:00Z"
    },
    {
      "id": 5,
      "name": "Kerudung Segi Empat Motif",
      "description": "Kerudung voal segi empat, motif bunga.",
      "price": 65000,
      "stock": 0,
      "status": "active",
      "category_id": 3,
      "merchant_name": "Butik Kirana",
      "created_at": "2026-02-25T09:00:00Z"
    },
    {
      "id": 6,
      "name": "Madu Hutan Murni",
      "description": "Madu hutan murni tanpa campuran, botol 500 ml.",
      "price": 95000,
      "stock": 18,
      "status": "active",
      "category_id": 4,
      "merchant_name": "Tani Makmur",
      "created_at": "2026-03-05T08:15:00Z"
    }
  ]
}
```

Salin `db.seed.json` menjadi `db.json` menggunakan skrip yang baru kamu buat, lalu nyalakan server:

```bash
npm run reset-db
npm run dev
```

### 6. Periksa di Browser & Hubungkan ke GitHub
1. Buka `http://localhost:5173` — pastikan aplikasi Vite bawaan tampil tanpa error di terminal/console. *(Rapikan `src/App.tsx` menjadi kerangka bersih `<h1>Katalog UMKM</h1>` jika mentor mengarahkan.)*
2. Buka tab baru `http://localhost:3001/products` — pastikan muncul daftar JSON 6 produk dari `db.json`.
3. Buat repositori baru bernama `katalog-umkm` di akun **GitHub pribadimu**, lalu lakukan commit awal:
   ```bash
   git init
   git add .
   git commit -m "chore: rakit pondasi proyek katalog-umkm"
   git branch -M main
   git remote add origin <URL-REPO-GITHUB-MU>
   git push -u origin main
   ```
   *(Catatan kepemilikan repo: pada Bulan 2–3, setiap murid mengerjakan kode di repo GitHub pribadinya agar semua berlatih end-to-end, sementara rekan satu **squad** saling menjadi reviewer PR dan pasangan pairing.)*

---

## Bekal Penting Aturan TypeScript & `json-server 0.17.4`

Sebelum mulai coding di Bulan 2, pahami 2 hal penting pada template Vite modern + `json-server`:

1. **Aturan `tsconfig.app.json` (jika aktif di template Vite-mu):**
   - `verbatimModuleSyntax`: Saat mengimpor **type/interface** saja, wajib menulis `import type { Product } from '../types/product'` agar TypeScript tidak error.
   - `erasableSyntaxOnly` (jika aktif): Hindari `enum` dan parameter properties di constructor class; gunakan union tipe literal seperti `type ProductStatus = 'active' | 'draft'`.
2. **Cheat Sheet Query `json-server 0.17.4`:**

| Kebutuhan | Contoh Endpoint |
|---|---|
| Semua / satu produk | `GET /products` · `GET /products/1` |
| Tambah / ubah sebagian / hapus | `POST /products` · `PATCH /products/1` · `DELETE /products/1` |
| Filter / cari teks / urutkan | `GET /products?category_id=1` · `?q=keripik` · `?_sort=price&_order=desc` |
| Paginasi | `GET /products?_page=1&_limit=6` *(total data ada di header `X-Total-Count`)* |

*(Catatan: **jangan gunakan `_expand=category`** di `json-server`, karena `_expand` mengasumsikan nama kolom `categoryId` sedangkan data kita memakai `category_id`. Kita akan memanggil `/categories` secara terpisah di Bulan 3.)*

---

## Cek Pemahaman & Diagnostik

Jawab pertanyaan ini bersama pasangan pairing di Blok 2:
1. Apa bedanya `npm run dev` dengan `npm run dev:web`?
2. Mengapa `json-server` dikunci di versi `0.17.4` dan tidak boleh di-upgrade ke `1.x`?
3. Mengapa `db.json` dimasukkan ke `.gitignore`, sedangkan `db.seed.json` ikut di-commit ke Git?

---

## Kesalahan Umum & Solusi

| Gejala | Sebab Biasa | Solusi |
|---|---|---|
| `npm install` atau `npm run dev` gagal jalan | Node.js di bawah `20.19` atau `22.12` | Update ke **Node.js 26** via `nvm`/`fnm`. |
| `localhost:3001/products` error atau kosong | Belum menjalankan `npm run reset-db` atau memakai `dev:web` | Jalankan `npm run reset-db` lalu `npm run dev`. |
| Query `_sort` / `_limit` tidak bekerja | Lupa `@0.17.4` saat `npm install` sehingga terpasang versi `1.x` | Jalankan `npm install -D json-server@0.17.4`. |
| TypeScript menegur import `Product` | `verbatimModuleSyntax` aktif di `tsconfig` | Tambahkan kata kunci `type`: `import type { Product } from ...`. |

---

Lanjut ke: **[03-alur-git-dan-pr.md](03-alur-git-dan-pr.md)**
