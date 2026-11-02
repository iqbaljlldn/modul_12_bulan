# 4.0a React Router Dasar — Navigasi Multi-Halaman di SPA

## Tujuan Sesi Ini

Memahami cara kerja **routing** pada aplikasi React SPA (*Single Page Application*), membungkus aplikasi dengan `BrowserRouter`, menghubungkan URL dengan komponen melalui `Routes` dan `Route`, serta memahami perbedaan krusial antara komponen `<Link>` dengan tag HTML biasa `<a href>`.

---

## Aktivitas Terbimbing di Kelas (Blok 1, 10-15 Menit)

Mentor akan memandu demonstrasi konsep:
- Mengapa aplikasi SPA tetap membutuhkan URL yang bisa disalin (*copy-paste link*) dan tombol kembali (*back/forward*) browser yang berfungsi.
- Memasang pustaka `react-router-dom` di terminal.
- Membungkus komponen utama dengan `<BrowserRouter>` di `src/main.tsx`.
- Membaca parameter dinamis dari URL (seperti `:id`) menggunakan hook `useParams()`.
- Mengapa `<Link>` menavigasi tanpa reload halaman sedangkan `<a href>` memicu reload penuh.

*(Bahan bacaan pendalaman opsional: Modul React Bootcamp Bab 3.4 tentang React Router Routing Dasar).*

---

## Ringkasan Konsep Kunci & Analogi

### 1. Apa itu Router di Dunia SPA?

> **Analogi Meja Resepsionis Apartemen:**  
> Pada website kuno (MPA), jika kamu ingin melihat informasi kamar 302, pengelola gedung akan merobohkan seluruh gedung lalu membangun ulang gedung baru yang hanya berisi kamar 302 (seluruh halaman web direload penuh).  
> **React Router** bertindak seperti **resepsionis cerdas di lobi**: seluruh gedung apartemen tetap berdiri kokoh. Saat tamu menyebut nomor kamar di alamat URL (`/products/3`), resepsionis cukup memandu lampu sorot ke kamar yang dimaksud tanpa perlu ada renovasi gedung sedikit pun!

### 2. Komponen `<Link>` vs Tag HTML Biasa `<a href>`

> **Analogi Lift Internal vs Keluar Gerbang:**  
> - **Komponen `<Link to="...">`:** Seperti menaiki **lift berkecepatan tinggi di dalam gedung**: kamu berpindah antar lantai dengan sangat halus, musik gedung tidak berhenti berputar, dan tidak ada jeda layar putih.  
> - **Tag HTML `<a href="...">`:** Seperti **keluar dari gerbang apartemen, pulang ke rumah, lalu masuk lagi dari pintu depan**: browser membuang seluruh JavaScript dan CSS dari memori, mengunduh ulang seluruh file dari server, dan membuat pengguna menunggu layar putih.  
> **Aturan Wajib:** Selalu gunakan `<Link>` untuk navigasi halaman internal aplikasi!

---

## Langkah demi Langkah: Latihan Dasar Routing

### Langkah 1: Pasang Dependensi React Router

Buka terminal proyek dan pasang paket resmi React Router:

```bash
npm install react-router-dom
```

---

### Langkah 2: Pasang `BrowserRouter` di `src/main.tsx`

Buka `src/main.tsx`. `BrowserRouter` harus membungkus komponen `<App />` di level paling atas agar seluruh komponen anak memiliki akses ke riwayat navigasi browser:

```tsx
// src/main.tsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import { BrowserRouter } from 'react-router-dom'
import './index.css'
import App from './App.tsx'

createRoot(document.getElementById('root')!).render(
  <StrictMode>
    {/* Bungkus seluruh aplikasi dengan BrowserRouter */}
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </StrictMode>,
)
```

---

### Langkah 3: Konfigurasi Rute di `src/App.tsx`

Perhatikan bagian `// TODO:` di bawah ini. Kita mendefinisikan rute halaman beranda dan rute halaman detail berparameter `:id`:

```tsx
// src/App.tsx
import { Routes, Route, Link } from 'react-router-dom'
import ProductsPage from './pages/ProductsPage'

// Komponen mini contoh untuk memahami rute statis
function AboutPage() {
  return (
    <div>
      <h2>Tentang Mini Katalog UMKM</h2>
      <p>Aplikasi kurasi produk lokal karya pengusaha UMKM Nusantara.</p>
      <Link to="/">← Kembali ke Beranda</Link>
    </div>
  )
}

function App() {
  return (
    <main style={{ maxWidth: '1000px', margin: '0 auto', padding: '24px 16px' }}>
      <header style={{ marginBottom: '24px' }}>
        <h1>Katalog UMKM Nusantara</h1>
        <nav style={{ display: 'flex', gap: '16px' }}>
          <Link to="/">Daftar Produk</Link>
          <Link to="/about">Tentang Kami</Link>
        </nav>
      </header>

      {/* TODO: Definisikan rute menggunakan Routes dan Route */}
      <Routes>
        <Route path="/" element={<ProductsPage />} />
        <Route path="/about" element={<AboutPage />} />
        {/* Rute detail berparameter :id akan kita pasang di sesi berikutnya */}
      </Routes>
    </main>
  )
}

export default App
```

---

## Analisis Bug & Prediksi (Aktivitas Blok 2)

Diskusikan bersama rekan pairing:

1. **Prediksi Error Fatal:**  
   Jika seorang murid lupa menambahkan pembungkus `<BrowserRouter>` di `main.tsx` tetapi langsung menulis `<Routes>` atau `<Link>` di dalam `App.tsx`, apa pesan error merah yang akan meledak di console browser saat aplikasi dibuka?  
   *(Petunjuk: pesan error akan menyebutkan kata kunci "useRoutes() may be used only in the context of a <Router> component")*.
2. **Uji Coba Network Link vs a:**  
   Buka Developer Tools > tab Network.  
   - Klik navigasi yang menggunakan `<Link to="/about">`. Perhatikan: apakah ada file `.html` yang diunduh ulang?
   - Coba ganti sementara dengan `<a href="/about">`, klik link tersebut, dan amati apakah ada kedipan layar putih dan proses reload penuh.

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan secara mandiri di kelas. Simpan hasilnya di:  
`tugas/squad-<nomor>/<nama-kamu>/tugas_04a.md`

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Tuliskan identitas diri (Nama, Squad, Tanggal).
3. Buat sebuah rancangan komponen mini navigasi bernama `UserGreetingRoute.tsx`:
   - Komponen tersebut menggunakan hook `useParams<{ username: string }>()`.
   - Mengambil nilai `username` dari parameter URL.
   - Menampilkan salam personal: `<h2>Selamat Datang, {username}!</h2>`.
   - Menampilkan tautan kembali ke halaman utama: `<Link to="/">Ke Katalog</Link>`.
   - Tuliskan kode komponen dan baris `<Route>` yang dibutuhkan untuk mendaftarkannya di `App.tsx` (misalnya pada path `"/greeting/:username"`).
4. Jawab 2 pertanyaan pemahaman:
   - Mengapa kita tidak boleh menggunakan tag HTML biasa `<a href="...">` untuk navigasi antar halaman di dalam aplikasi React SPA?
   - Mengapa nilai parameter yang dihasilkan oleh `useParams()` selalu bertipe `string` (atau `undefined`), meskipun di URL kita mengetikkan angka seperti `/products/15`?
5. Ajukan Pull Request ke repositori squad.

### Contoh Format Hasil (`tugas_04a.md`)

```markdown
# Tugas Mandiri 04a — React Router Dasar
Nama: Lukman Hakim
Squad: Squad 2
Tanggal: 19 November 2026

## 1. Kode Komponen UserGreetingRoute
```tsx
import { useParams, Link } from 'react-router-dom'

function UserGreetingRoute() {
  const { username } = useParams<{ username: string }>()

  return (
    <div className="greeting-card">
      <h2>Selamat Datang, {username ?? 'Tamu'}!</h2>
      <p>Terima kasih telah mengunjungi etalase UMKM kami.</p>
      <Link to="/">← Kembali ke Katalog</Link>
    </div>
  )
}

export default UserGreetingRoute
```

Pendaftaran rute di `App.tsx`:
```tsx
<Route path="/greeting/:username" element={<UserGreetingRoute />} />
```

## 2. Jawaban Pertanyaan Pemahaman
1. Tag `<a href>` memicu perilaku bawaan browser untuk melakukan refresh halaman secara penuh (*full page reload*). Hal ini merusak pengalaman mulus aplikasi SPA, membuang state yang tersimpan di memori JavaScript, dan memaksa browser mengunduh ulang seluruh file aset. Komponen `<Link>` menggunakan HTML5 History API di balik layar untuk mengubah URL tanpa memuat ulang halaman.
2. Karena seluruh isi alamat URL di bilah peramban (*address bar*) pada dasarnya adalah barisan teks karakter (string). Komputer tidak bisa menebak apakah angka "15" di URL dimaksudkan sebagai nomor identitas atau teks biasa, sehingga React Router selalu mengembalikannya dalam bentuk tipe `string`. Jika kita membutuhkan nilai angka untuk kalkulasi atau query API, kita wajib mengonversinya secara sadar menggunakan `Number(id)`.
```

---

Lanjut ke: **04b-routing-dan-detail.md** (Slice 4)
