# 1.0a Orientasi React — Sebelum Mulai Coding

## Tujuan sesi ini

Paham **apa** itu React, **kenapa** kita pakai React (bukan vanilla JS seperti di pre-class), dan **bagaimana** starter repo yang akan kita kerjakan selama 3 bulan ke depan disusun.

> Sesi ini belum ada kode yang ditulis ke Katalog. Ini sesi baca, eksplorasi, dan tanya-jawab.

## Bacaan wajib sebelum sesi

Baca **Bab 1.1 — Pengenalan React & Setup Environment** di modul React bootcamp. Yang paling penting dipahami:
- Apa itu React dan kenapa dipakai
- SPA vs MPA
- Virtual DOM & Reconciliation
- Struktur folder proyek React (Vite)

Bagian tentang **Create React App** di bab itu boleh di-skip — kita pakai **Vite** di program ini.

## Ringkasan konsep (dari bab 1.1, diringkas)

### Apa itu React?

React adalah **library JavaScript** untuk membangun user interface (UI). Bukan framework lengkap — React fokus pada satu hal: merender UI berdasarkan data. Sisanya (routing, state management global, dll.) ditambahkan lewat library lain sesuai kebutuhan.

Kenapa bukan vanilla JS seperti di pre-class?

| Vanilla JS (pre-class) | React |
|---|---|
| Kamu manipulasi DOM langsung (`document.getElementById(...)`) | React yang mengurus DOM — kamu cukup bilang "datanya begini, tampilkan begitu" |
| Makin banyak elemen interaktif, makin rumit kodenya | Dipecah jadi **komponen** kecil yang bisa dipakai ulang |
| Harus manual lacak data mana yang berubah | React otomatis re-render bagian yang berubah (Virtual DOM) |

### SPA (Single Page Application)

Aplikasi React biasanya berbentuk **SPA**: satu file HTML, dan React yang mengatur kontennya secara dinamis tanpa reload halaman penuh. Ini yang membuat aplikasi terasa cepat dan responsif.

Keuntungan: navigasi tanpa reload, pengalaman pengguna lebih mulus.
Konsekuensi: JavaScript harus diunduh di awal (initial load agak lebih lama).

### Virtual DOM

React tidak langsung mengubah DOM di browser. Proses kerjanya:

```text
State/data berubah
    ↓
React buat Virtual DOM baru (di memori)
    ↓
Bandingkan dengan Virtual DOM lama (diffing)
    ↓
Hanya bagian yang berubah yang diupdate ke DOM asli
```

Kamu **tidak perlu paham detail implementasinya** — cukup paham bahwa React efisien karena tidak mengubah seluruh halaman setiap kali ada perubahan kecil.

## Kenali starter repo

Sekarang buka starter repo (`katalog-umkm-starter`) yang sudah kamu fork/clone.

### Jalankan

```bash
npm install
npm run dev
```

Buka `localhost:5173` di browser. Kamu harusnya melihat halaman kosong (atau halaman default Vite).

### Struktur folder

```text
katalog-umkm-starter/
├── public/                   # Aset statis (favicon, dll.)
├── src/                      # Kode kita di sini
│   ├── App.tsx               # Komponen utama
│   ├── main.tsx              # Entry point (BrowserRouter nanti di sini)
│   └── index.css             # CSS global
├── db.seed.json              # Data produk contoh untuk json-server
├── package.json              # Dependency & scripts
├── tsconfig.json             # Konfigurasi TypeScript
├── vite.config.ts            # Konfigurasi Vite
└── .oxlintrc.json            # Konfigurasi linter
```

**File yang paling sering kamu sentuh:** semua yang di `src/`.

### Kenapa Vite, bukan Create React App?

Bab 1.1 di modul React membahas keduanya. Singkatnya:
- **Vite** lebih cepat (dev server instan, hot reload cepat)
- **CRA** sudah jarang direkomendasikan untuk proyek baru
- Starter kita sudah di-setup Vite — kamu tidak perlu setup sendiri

### Apa itu `json-server`?

Di starter ada script `npm run dev` yang juga menjalankan `json-server`. Ini **API palsu** — server kecil yang membaca `db.seed.json` dan menyediakan endpoint REST (`GET /products`, `POST /products`, dll.) tanpa perlu menulis backend.

```text
Browser  →  React app (localhost:5173)  →  fetch()  →  json-server (localhost:3001)
```

API palsu ini akan kita pakai di Bulan 2-3. Di Bulan 4, diganti backend asli (NestJS + PostgreSQL).

## Latihan (eksplorasi, bukan coding)

1. Buka `db.seed.json`, lihat isinya. Berapa produk yang ada? Field apa saja?
2. Buka `localhost:3001/products` di browser — bandingkan isinya dengan `db.seed.json`.
3. Buka `src/App.tsx`, ganti teks di dalamnya, simpan, lihat browser update otomatis (Hot Module Replacement).
4. Buka `tsconfig.json`, lihat sekilas. Kamu tidak perlu paham semuanya — mentor akan jelaskan seperlunya nanti.

## Cek pemahaman

- Apa bedanya SPA dan MPA? Katalog UMKM kita termasuk yang mana?
- Apa yang dilakukan Virtual DOM saat ada data berubah?
- File apa saja yang ada di `src/`? Mana yang menjadi "pintu masuk" aplikasi?

---

Lanjut ke: **01b-jsx-dan-komponen-bertipe.md**
