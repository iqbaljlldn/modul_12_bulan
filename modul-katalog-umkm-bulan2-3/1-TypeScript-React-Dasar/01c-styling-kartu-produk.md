# 1.0c Styling Kartu Produk — CSS di React

## Tujuan sesi ini

Kartu produk yang sudah jalan dari sesi sebelumnya masih **polos** (tanpa styling). Sesi ini menambahkan CSS supaya kartu terlihat layak dan peserta paham cara styling di React.

## Bacaan wajib sebelum sesi

**Bab 1.4 — Styling dalam React** (modul React): inline styles, CSS classes, CSS Modules, responsive design.

## Ringkasan konsep (dari bab 1.4)

Ada beberapa cara styling di React. Di program ini kita mulai dari yang paling sederhana:

### 1. CSS Classes (cara yang kita pakai)

Tulis CSS di file `.css` biasa, pakai `className` di JSX:

```tsx
// ProductCard.tsx
<article className="product-card">...</article>
```

```css
/* index.css atau ProductCard.css */
.product-card {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 12px;
}
```

### 2. Inline Styles (kadang berguna, jangan jadi default)

```tsx
<p style={{ color: 'green', fontWeight: 'bold' }}>Tersedia</p>
```

Perhatikan: **double curly braces** — yang luar untuk JSX expression, yang dalam untuk objek JavaScript. Property CSS ditulis **camelCase** (`fontWeight` bukan `font-weight`).

Inline style berguna untuk nilai dinamis (misal warna berdasarkan data), tapi jangan dipakai untuk semua styling — susah di-maintain.

### 3. CSS Modules (opsional, dipakai nanti kalau tribe sepakat)

File CSS dengan nama `*.module.css` di-scope otomatis per komponen — menghindari bentrokan nama class.

```tsx
import styles from './ProductCard.module.css'
<article className={styles.card}>...</article>
```

> **Keputusan tribe:** di Bulan 3 nanti tribe akan memutuskan standar styling (CSS biasa, CSS Modules, atau Tailwind). Untuk sekarang, pakai **CSS biasa** supaya semua fokus ke React dulu.

## Langkah: styling Katalog UMKM

### 1. Tambahkan CSS untuk kartu produk

Di `src/index.css` (atau buat `src/components/ProductCard.css` dan import di `ProductCard.tsx`):

```css
/* === Layout === */
.product-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 16px;
  padding: 16px 0;
}

/* === Kartu Produk === */
.product-card {
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  padding: 20px;
  background: #ffffff;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
  transition: box-shadow 0.2s ease;
}

.product-card:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.12);
}

.product-card h3 {
  margin: 0 0 8px;
  font-size: 1.1rem;
  color: #1a202c;
}

.product-card p {
  margin: 4px 0;
  color: #4a5568;
  font-size: 0.9rem;
  line-height: 1.5;
}

/* === Badge (status draft) === */
.badge {
  display: inline-block;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 0.75rem;
  font-weight: 600;
  background: #edf2f7;
  color: #718096;
}

/* === Out of stock === */
.out-of-stock {
  color: #e53e3e;
  font-weight: 600;
}
```

### 2. Responsive dasar

CSS Grid dengan `auto-fill` + `minmax` sudah otomatis responsif: di layar kecil kartu satu kolom, di layar besar bisa 2-3 kolom.

Coba resize browser untuk melihat efeknya.

### 3. Pakai class baru di komponen

Update `ProductCard.tsx` untuk memanfaatkan class yang baru:

```tsx
<p className={isOutOfStock ? 'out-of-stock' : ''}>
  {isOutOfStock ? 'Stok habis' : `Stok: ${product.stock}`}
</p>
```

## Latihan

1. Tambahkan **hover effect** pada kartu (misalnya: border warna berubah saat mouse di atas). Coba tulis CSS-nya sendiri.
2. Buat variasi warna badge: `active` = hijau muda, `draft` = abu-abu. Gunakan **conditional className** di JSX.
3. Coba tulis satu property styling sebagai **inline style** (misal harga berwarna hijau). Bandingkan kode dengan versi CSS class — mana yang lebih mudah dibaca?
4. Buka di layar HP (atau pakai DevTools responsive mode) — apakah tampilannya masih oke?

## Cek pemahaman

- Kenapa `className` bukan `class`?
- Kapan sebaiknya pakai inline style vs CSS class?
- Apa keuntungan CSS Modules dibanding CSS biasa?

## Kesalahan umum

| Gejala | Sebab | Solusi |
|---|---|---|
| Styling tidak muncul sama sekali | File CSS tidak di-import | Tambahkan `import './index.css'` di `main.tsx` atau import per komponen |
| `style="color: red"` di JSX → error | Inline style di JSX harus pakai objek JS | Tulis `style={{ color: 'red' }}` |
| Class bentrok (nama class sama di file beda) | CSS biasa memang global | Untuk sekarang: beri nama class yang spesifik. Nanti pertimbangkan CSS Modules. |

## Kaitkan ke rujukan

**Bab 1.4** modul React membahas semua cara styling lebih lengkap, termasuk contoh responsive design dan CSS Modules.

---

Lanjut ke: **01d-tipe-dasar-dan-list-rendering.md** (Slice 0)
