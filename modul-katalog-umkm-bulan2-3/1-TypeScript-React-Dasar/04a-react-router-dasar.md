# 4.0a React Router Dasar — Navigasi Multi-Halaman di SPA

## Tujuan sesi ini

Paham cara kerja **routing** di React SPA (halaman berganti tanpa reload browser), dan latihan membuat routing sederhana sebelum implementasi di Katalog.

## Bacaan wajib sebelum sesi

**Bab 3.4 — React Router Routing Dasar** (modul React): BrowserRouter, Route, Link, useParams, useNavigate.

## Ringkasan konsep (dari bab 3.4)

### Kenapa Butuh Router?

Di SPA, seluruh aplikasi berjalan di **satu halaman HTML**. Tapi user tetap butuh:
- URL yang bisa di-bookmark (`/products/3`)
- Tombol back/forward browser yang berfungsi
- Halaman yang bisa di-refresh tanpa kehilangan konteks

**React Router** menghubungkan URL dengan komponen — saat URL berubah, React Router menentukan komponen mana yang ditampilkan, **tanpa** reload halaman.

### Install

```bash
npm install react-router-dom
```

### Setup Dasar

```tsx
// main.tsx — bungkus di level tertinggi
import { BrowserRouter } from 'react-router-dom'

createRoot(document.getElementById('root')!).render(
  <StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </StrictMode>,
)
```

### Definisikan Rute

```tsx
// App.tsx
import { Routes, Route } from 'react-router-dom'

function App() {
  return (
    <Routes>
      <Route path="/" element={<HomePage />} />
      <Route path="/about" element={<AboutPage />} />
      <Route path="/products/:id" element={<ProductDetailPage />} />
    </Routes>
  )
}
```

`:id` di `/products/:id` = **route parameter** — bagian URL yang berubah-ubah.

### Navigasi dengan `Link`

```tsx
import { Link } from 'react-router-dom'

// ✅ Navigasi tanpa reload (SPA)
<Link to="/about">Tentang</Link>

// ❌ Ini reload halaman penuh — JANGAN
<a href="/about">Tentang</a>
```

### Baca Route Parameter dengan `useParams`

```tsx
import { useParams } from 'react-router-dom'

function ProductDetailPage() {
  const { id } = useParams<{ id: string }>()
  // id selalu string (dari URL) — konversi ke number kalau perlu
  const productId = Number(id)
  // ...
}
```

### Navigasi Programatik dengan `useNavigate`

```tsx
import { useNavigate } from 'react-router-dom'

function DeleteButton() {
  const navigate = useNavigate()

  async function handleDelete() {
    await deleteProduct(id)
    navigate('/')  // Arahkan kembali ke halaman utama
  }

  return <button onClick={handleDelete}>Hapus</button>
}
```

## Latihan (sebelum implementasi di Katalog)

1. **Mini app routing:** buat aplikasi dengan 3 halaman (Home, About, Contact) yang masing-masing punya `Link` ke halaman lain. Pastikan navigasi **tanpa reload**.

2. **Route parameter:** tambahkan halaman `/user/:name` yang menampilkan "Halo, {name}!" dengan nama diambil dari URL.

3. **Bedakan Link vs a:** ganti salah satu `<Link>` dengan `<a href>`, klik, amati perbedaannya (lihat di Network tab — ada request baru atau tidak?).

## Cek pemahaman

- Kenapa `<Link>` lebih baik dari `<a href>` di React SPA?
- Apa yang terjadi kalau `BrowserRouter` tidak dipasang di `main.tsx`?
- Kenapa `useParams` mengembalikan string, bukan number?

## Kesalahan umum

| Gejala | Sebab | Solusi |
|---|---|---|
| Error "useRoutes() may only be used..." | `BrowserRouter` belum dibungkus di `main.tsx` | Pastikan `<BrowserRouter>` membungkus `<App />` |
| Klik Link, halaman putih sebentar | Pakai `<a href>` bukan `<Link to>` | Ganti ke `<Link>` |
| Route tidak match | Typo di path (misal `/product` vs `/products`) | Cek path di `<Route>` dan `<Link>` konsisten |

## Kaitkan ke rujukan

**Bab 3.4** modul React untuk penjelasan lebih lengkap. **Bab 3.5** (React Router Advanced — nested routes, protected routes, dll.) akan dipakai di Bulan 3.

---

Lanjut ke: **04b-routing-dan-detail.md** (Slice 4)
