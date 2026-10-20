# Latihan Tambahan — React Lanjutan (Bulan 3)

Latihan-latihan ini ditujukan untuk peserta atau squad yang **menyelesaikan slice mingguan lebih cepat** dan ingin tantangan ekstra sebelum masuk ke Bulan 4.

---

## Tantangan 1: Skeleton Loading Placeholder (Minggu 1)

Saat `isLoading === true`, daripada hanya menampilkan teks `<p>Memuat produk...</p>`, gantilah dengan **Skeleton Loading Card** menggunakan animasi pulsa Tailwind:

```tsx
function ProductCardSkeleton() {
  return (
    <div className="animate-pulse rounded-lg border border-slate-200 bg-white p-5 shadow-sm">
      <div className="mb-3 h-48 w-full rounded-md bg-slate-200" />
      <div className="mb-2 h-5 w-3/4 rounded bg-slate-200" />
      <div className="mb-4 h-4 w-1/2 rounded bg-slate-200" />
      <div className="h-8 w-full rounded bg-slate-200" />
    </div>
  )
}
```

Tampilkan 6 skeleton card saat data produk pertama kali dimuat.

---

## Tantangan 2: Toast Queue & Tombol Tutup Silang (Minggu 2)

Perluas sistem `ToastProvider`:
1. Tambahkan tombol silang `×` di pojok kanan setiap toast agar pengguna bisa menutup notifikasi secara manual sebelum timer 3 detik habis.
2. Tambahkan animasi slide-in dari bawah layar menggunakan class transition Tailwind.
3. Batasi jumlah toast di layar maksimal 3 buah sekaligus (antrean FIFO).

---

## Tantangan 3: Filter Range Harga Minimum & Maksimum (Minggu 3)

Perluas antarmuka pencarian `ProductFilters.tsx` dan backend query:
1. Tambahkan input `minPrice` dan `maxPrice`.
2. `json-server` mendukung operator perbandingan:
   - `price_gte=10000` (Greater than or equal / Lebih dari atau sama dengan)
   - `price_lte=50000` (Less than or equal / Kurang dari atau sama dengan)
3. Sinkronkan nilai `minPrice` dan `maxPrice` ini ke URL Search Params!

---

## Tantangan 4: Konfirmasi Modal Kustom (Bukan `window.confirm`) (Minggu 4)

Ganti `if (confirm('Yakin hapus?'))` bawaan browser dengan **Modal Dialog Kustom** yang dibangun menggunakan React Portal atau komponen dialog Tailwind:
- Memiliki judul, pesan peringatan, tombol Batal (abu-abu), dan tombol Hapus (merah).
- Aksesibilitas: Menekan tombol `Escape` di keyboard otomatis membatalkan dan menutup modal.

---

## Tantangan 5: Persiapan Spesifikasi OpenAPI / Swagger (Menjelang Bulan 4)

Jika squad sangat tertarik pada backend:
- Pelajari dasar spesifikasi OpenAPI 3.0.
- Buat file `docs/openapi.yaml` sederhana yang memformalkan isi `docs/kontrak-api.md`. Ini akan menjadi modal luar biasa saat masuk ke NestJS Swagger di Bulan 4!
