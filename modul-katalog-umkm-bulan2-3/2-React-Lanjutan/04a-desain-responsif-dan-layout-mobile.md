# 2.4a Desain Responsif & Layout Mobile dengan Tailwind CSS

> **Bacaan wajib sebelum sesi:** Modul React Programmer Pit — **Bab 4.2** (Advanced Styling & UI Libraries — bagian Responsive Design).  
> **Prasyarat:** Menguasai utility classes Tailwind CSS dasar dari unit `01a`.

---

## Kenapa Unit Ini Ada?

Di Indonesia, lebih dari **85% pelaku UMKM mengelola bisnis mereka menggunakan smartphone**, bukan laptop atau komputer meja.
Sebagus apa pun fitur pencarian, filter, dan validasi form yang kita bangun di Slice 5-7, jika saat dibuka di layar HP:
- Tombol Simpan terpotong atau keluar layar,
- Kartu produk saling tumpang tindih,
- Kolom filter terlalu kecil untuk disentuh jari (*fat-finger problem*),

maka aplikasi kita **gagal dipakai oleh pengguna sesungguhnya**.

Di unit ini, kita menerapkan prinsip **Mobile-First Design** menggunakan sistem breakpoint responsif bawaan Tailwind CSS.

---

## 1. Filosofi Mobile-First Tailwind CSS

Tailwind dirancang dengan pendekatan **Mobile-First**:
- Kelas tanpa awalan (*prefix*) berlaku untuk **semua ukuran layar (dimulai dari HP terkecil)**.
- Awalan breakpoint (`sm:`, `md:`, `lg:`, `xl:`) hanya aktif **ketika ukuran layar sama dengan atau lebih besar** dari breakpoint tersebut:

| Prefix | Lebar Layar Minimum | Target Perangkat |
|---|---|---|
| *(tanpa prefix)* | `0px` | Smartphone portrait (iPhone, Android) |
| `sm:` | `640px` | Smartphone landscape / tablet kecil |
| `md:` | `768px` | Tablet portrait (iPad) |
| `lg:` | `1024px` | Laptop / Desktop standar |
| `xl:` | `1280px` | Monitor desktop lebar |

> **Prinsip Utama:** Jangan pernah menulis class untuk desktop dulu lalu menimpanya untuk HP. Selalu tentukan tampilan HP terlebih dahulu, lalu tambahkan `sm:` atau `lg:` saat layar melebar!

---

## 2. Praktik Adaptasi Responsif di Katalog UMKM

### A. Grid Daftar Produk (`ProductList.tsx`)
Di layar HP, kartu produk harus tampil 1 kolom penuh agar foto dan detail terbaca jelas. Di tablet tampil 2 kolom, dan di layar laptop tampil 3 kolom:

```tsx
<div className="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3">
  {products.map((product) => (
    <ProductCard key={product.id} ... />
  ))}
</div>
```

### B. Baris Kontrol Filter (`ProductFilters.tsx`)
Di HP, elemen input pencarian, kategori, dan urutan sebaiknya tersusun vertikal atau membungkus rapi (*wrap*), lalu menjadi satu baris sejajar di desktop:

```tsx
<div className="mb-6 flex flex-col gap-4 rounded-lg border border-slate-200 bg-white p-4 shadow-sm sm:flex-row sm:items-end">
  {/* Kolom Cari: melebar penuh di HP, ukuran fleksibel di layar besar */}
  <div className="flex-1">
    <Input label="Cari Produk" ... />
  </div>

  {/* Dropdown Kategori & Urutkan */}
  <div className="flex gap-3">
    <select className="w-full sm:w-auto" ... />
    <select className="w-full sm:w-auto" ... />
  </div>
</div>
```

### C. Form Tambah & Edit Produk (`ProductForm.tsx`)
Input form tampil 1 kolom di HP agar nyaman diketik dengan keyboard virtual, dan menjadi 2 kolom di tablet/desktop:

```tsx
<div className="grid grid-cols-1 gap-4 sm:grid-cols-2">
  <Input label="Nama Produk" ... />
  <Input label="Harga (Rp)" ... />
  <Input label="Stok" ... />
  <Input label="Nama UMKM" ... />
</div>
```

### D. Kenyamanan Sentuhan (*Touch Target Sizing*)
Jari manusia membutuhkan area sentuh minimal **44 x 44 piksel** agar tidak salah pencet. Pastikan tombol memiliki padding yang cukup:
```tsx
// ✅ Nyaman disentuh di HP:
className="px-4 py-2.5 text-sm font-medium sm:py-2"
```

---

## 3. Cara Menguji Tampilan Responsif di Browser

Jangan menunggu meminjam HP teman untuk mengetes! Gunakan **Device Mode** di Chrome/Firefox DevTools:

1. Tekan tombol `F12` atau `Ctrl + Shift + I` (Linux/Windows) / `Cmd + Option + I` (Mac).
2. Klik ikon **Toggle Device Toolbar** (ikon HP/Tablet di pojok kiri atas jendela DevTools, atau tekan `Ctrl + Shift + M`).
3. Pilih perangkat:
   - **iPhone SE (375px):** Uji coba ukuran layar HP sempit.
   - **Pixel 7 (412px):** Uji coba ukuran Android umum.
   - **iPad Mini (768px):** Uji coba tablet.
4. Coba lakukan pencarian produk, pilih kategori, dan isi form langsung dalam mode HP tersebut.

---

## Latihan Mandiri (30 Menit)

1. **Uji Layar 320px:**
   Di DevTools Device Toolbar, ubah lebar layar menjadi `320px` (layar HP sangat kecil). Periksa apakah ada teks atau tombol yang terpotong ke samping (*horizontal scrollbar* yang tidak disengaja). Jika ada, perbaiki menggunakan kelas `max-w-full` atau `overflow-hidden`.
2. **Navigasi Pagination di HP:**
   Periksa komponen `Pagination.tsx` di layar 375px. Pastikan tombol "Sebelumnya" dan "Berikutnya" tidak menabrak teks "Halaman X dari Y".

---

## Cek Pemahaman

1. Mengapa pendekatan *Mobile-First* lebih disukai dibandingkan *Desktop-First* di Tailwind CSS?
2. Jika sebuah elemen diberi class `p-2 sm:p-4 lg:p-8`, berapa ukuran padding yang aktif saat website dibuka di layar selebar 800px?
3. Apa risiko jika tombol aksi di layar HP diberi padding terlalu kecil (misalnya `p-0.5`)?

---

**Lanjut ke:** `04b-konsolidasi-dan-kontrak-api.md` (Slice 8 — Konsolidasi & Kontrak API Tertulis)
