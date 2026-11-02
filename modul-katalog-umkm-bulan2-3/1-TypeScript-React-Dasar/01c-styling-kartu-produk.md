# 1.0c Styling Kartu Produk — CSS di React

## Tujuan Sesi Ini

Memberikan tampilan visual yang rapi, profesional, dan responsif pada kartu produk Katalog UMKM menggunakan **CSS Classes** murni, serta memahami kapan saat yang tepat menggunakan inline style.

---

## Aktivitas Terbimbing di Kelas (Blok 1, 10-15 Menit)

Mentor akan memandu demonstrasi singkat:
- Cara mengimpor berkas CSS ke dalam komponen React.
- Mengatur tata letak kartu menggunakan CSS Grid responsif (`repeat(auto-fill, minmax(...))`).
- Perbedaan mendasar antara *CSS Classes* dengan *Inline Styles* di React.
- Menentukan kelas visual secara kondisional di JSX (misal: teks merah saat stok habis).

*(Bahan bacaan pendalaman opsional: Modul React Bootcamp Bab 1.4 tentang Styling dalam React).*

---

## Ringkasan Konsep Kunci & Analogi

### 1. CSS Classes vs Inline Style

> **Analogi Sehari-hari:**  
> **CSS Classes** seperti **seragam sekolah**: semua murid yang mengenakan tanda pengenal `.product-card` otomatis rapi dengan warna, jahitan, dan ukuran saku yang sama. Jika ada aturan seragam yang diubah di tata tertib (file `.css`), seluruh murid otomatis rapi bersamaan.  
> **Inline Style** (`style={{ ... }}`) seperti menempelkan plester warna khusus di lengan satu murid tertentu. Berguna untuk kondisi yang sangat khusus dan dinamis (misalnya progress bar baterai), tapi jika seluruh pakaian diatur dengan plester, kode menjadi sangat sulit dirawat.

### 2. Aturan Inline Style di JSX
Jika kamu harus menggunakan inline style, ingat dua pasang kurung kurawal `{{ ... }}`:
1. Kurung luar `{}`: penanda ekspresi JavaScript di JSX.
2. Kurung dalam `{}`: objek JavaScript berisi pasangan properti dan nilai.
3. Properti CSS ditulis dalam format **camelCase** (contoh: `backgroundColor`, `fontSize`, `borderRadius`).

```tsx
// ✅ Benar: objek JS dengan camelCase
<p style={{ color: '#e53e3e', fontWeight: 'bold' }}>Stok Menipis!</p>
```

---

## Langkah demi Langkah: Menata Kartu Katalog

### Langkah 1: Tambahkan Tata Letak Grid dan Gaya Kartu

Buka berkas `src/index.css` dan tambahkan aturan tata letak dasar berikut:

```css
/* === Tata Letak Galeri Produk (Grid Otomatis Responsif) === */
.product-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 16px;
  padding: 16px 0;
}

/* === Kartu Produk === */
.product-card {
  border: 1px solid #e2e8f0;
  border-radius: 10px;
  padding: 18px;
  background: #ffffff;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.06);
  transition: transform 0.15s ease, box-shadow 0.15s ease;
}

.product-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 14px rgba(0, 0, 0, 0.1);
}

.product-card h3 {
  margin: 0 0 8px;
  font-size: 1.15rem;
  color: #1a202c;
}

.product-card p {
  margin: 6px 0;
  color: #4a5568;
  font-size: 0.9rem;
  line-height: 1.45;
}

/* === Indikator Badge Status === */
.badge {
  display: inline-block;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 0.75rem;
  font-weight: 600;
  background: #edf2f7;
  color: #4a5568;
}

/* === Status Kritis / Habis === */
.stock-warning {
  color: #e53e3e;
  font-weight: 600;
}
```

---

### Langkah 2: Pasang Dynamic Class di `ProductCard.tsx`

Buka `src/components/ProductCard.tsx`. Perhatikan bagian `// TODO:` untuk menerapkan kelas CSS kondisional:

```tsx
// src/components/ProductCard.tsx
import type { Product } from '../types/product'

interface ProductCardProps {
  product: Product
}

function ProductCard({ product }: ProductCardProps) {
  const isOutOfStock = product.stock === 0

  return (
    <article className="product-card">
      <h3>{product.name}</h3>
      {product.status === 'draft' && <span className="badge">Draft</span>}
      <p>{product.description}</p>
      <p>
        <strong>Rp {product.price.toLocaleString('id-ID')}</strong>
      </p>

      {/* TODO: Jika isOutOfStock bernilai true, berikan className="stock-warning".
          Jika stok masih ada, kosongkan class (className="") */}
      <p className={isOutOfStock ? 'stock-warning' : ''}>
        {isOutOfStock ? 'Stok habis' : `Stok: ${product.stock}`}
      </p>

      <p>
        <small>UMKM: {product.merchant_name}</small>
      </p>
    </article>
  )
}

export default ProductCard
```

---

## Analisis Bug & Prediksi (Aktivitas Blok 2)

Diskusikan bersama pasangan pairing:

1. **Temukan Bug:**  
   Seorang murid menulis baris berikut di dalam JSX:
   ```tsx
   <div style="background-color: red; margin-top: 10px;">Pemberitahuan</div>
   ```
   Mengapa kode di atas menyebabkan error saat aplikasi dijalankan? Tuliskan perbaikan yang benar!
2. **Prediksi Tampilan:**  
   Apa keuntungan dari aturan CSS `grid-template-columns: repeat(auto-fill, minmax(260px, 1fr))` saat halaman dibuka di layar ponsel selebar 360px dibandingkan saat dibuka di layar laptop selebar 1366px?

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan tugas ini secara mandiri di kelas. Simpan hasilnya di:  
`tugas/squad-<nomor>/<nama-kamu>/tugas_01c.md`

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Tuliskan identitas diri (Nama, Squad, Tanggal).
3. Buat rancangan class CSS baru bernama `.badge-active` untuk produk yang statusnya aktif:
   - Warna latar (*background*): hijau muda lembut (contoh `#e6fffa`)
   - Warna teks: hijau tua tegas (contoh `#234e52`)
   - Tuliskan potongan CSS-nya.
4. Tuliskan potongan JSX cara menerapkan class tersebut pada elemen status produk secara kondisional berdasarkan nilai `product.status === 'active'`.
5. Jawab 2 pertanyaan pemahaman:
   - Kapan sebaiknya kita menggunakan CSS Classes biasa dan kapan kita boleh menggunakan inline style di React?
   - Mengapa kita tidak perlu menulis media query rumit (`@media (max-width: 600px)`) hanya untuk membuat daftar kartu produk kita responsif di ponsel?
6. Buka PR di repository squad untuk direview rekan.

### Contoh Format Hasil (`tugas_01c.md`)

```markdown
# Tugas Mandiri 01c — Styling Kartu Produk
Nama: Budi Santoso
Squad: Squad 1
Tanggal: 5 November 2026

## 1. Aturan CSS Badge Aktif
```css
.badge-active {
  display: inline-block;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 0.75rem;
  font-weight: 600;
  background: #e6fffa;
  color: #234e52;
}
```

## 2. Penerapan di JSX
```tsx
<span className={product.status === 'active' ? 'badge-active' : 'badge'}>
  {product.status === 'active' ? 'Tersedia' : 'Draft'}
</span>
```

## 3. Jawaban Pertanyaan
- CSS Classes sebaiknya menjadi standar utama untuk seluruh tata letak dan komponen yang berulang agar kode bersih dan mudah dirawat. Inline styles hanya digunakan untuk nilai yang dinamis berubah setiap waktu melalui JavaScript (misalnya lebar persentase progress bar).
- Karena aturan `repeat(auto-fill, minmax(260px, 1fr))` pada CSS Grid sudah otomatis menghitung ruang layar: jika layar < 520px, browser otomatis menampilkan 1 kolom penuh; jika layar melebar, browser otomatis menambah jumlah kolom sesuai kelipatan minimal 260px.
```

---

Lanjut ke: **01d-tipe-dasar-dan-list-rendering.md**
