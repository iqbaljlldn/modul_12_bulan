# 2.3d Latihan & Pemantapan Slice 7

> **Tujuan sesi:** Memperdalam pemahaman arsitektur state di URL, penanganan kondisi tepi (*edge cases*) pencarian kosong, dan tombol reset filter.  
> **Format:** Praktik mandiri / pair programming (45-60 menit) + peer review.

---

## Latihan 1: Tampilan Status Kosong (*Empty State*) & Reset Filter

Saat ini, jika pengguna mencari kata kunci yang tidak ada hasilnya (misalnya `"zzzzzzz"`), daftar produk kosong tanpa ada pesan ramah.

### Tugas:
1. Di `ProductsPage.tsx`, periksa kondisi ketika data produk kosong (`products.length === 0` dan tidak sedang loading):
   ```tsx
   {products.length === 0 ? (
     <div className="rounded-lg border border-dashed border-slate-300 p-8 text-center">
       <p className="text-slate-600">Tidak ada produk yang cocok dengan pencarian Anda.</p>
       <Button
         variant="secondary"
         className="mt-3"
         onClick={() => setSearchParams({})}
       >
         Reset Semua Filter
       </Button>
     </div>
   ) : (
     <ProductList ... />
   )}
   ```
2. Uji coba dengan mengetik kata acak di kotak pencarian, lalu klik tombol **Reset Semua Filter**. Pastikan URL kembali bersih dan semua produk tampil kembali.

---

## Latihan 2: Pengujian Navigasi Riwayat Browser (Back & Forward)

Karena state kita sekarang tersimpan di URL via `useSearchParams`, tombol panah **Back** (Kembali) dan **Forward** (Maju) di pojok kiri atas browser seharusnya berfungsi seperti saat kita menjelajahi website biasa.

### Skenario Uji:
1. Buka halaman utama.
2. Cari kata `"Kopi"`.
3. Ganti kategori ke salah satu pilihan.
4. Klik halaman `2`.
5. Sekarang, klik tombol panah **Back** di browser 3 kali berturut-turut.
   - Amati address bar dan tampilan: apakah aplikasi mundur langkah demi langkah sesuai riwayat pencarianmu?
6. Klik tombol **Forward** di browser: apakah aplikasi maju kembali ke kondisi sebelumnya?

Jika semua bekerja mulus, kamu baru saja merasakan kekuatan arsitektur URL-as-State!

---

## Checklist Code Review Slice 7

Sebelum mengajukan PR ke branch tim:

- [ ] Fungsi `fetchPage` membaca header `X-Total-Count` secara tepat.
- [ ] Custom hook `useDebouncedValue` memiliki timer dan fungsi cleanup `clearTimeout`.
- [ ] Nilai input pencarian terbagi menjadi dua: `urlFilters.q` (instan) dan `activeFilters.q` (debounced).
- [ ] Objek filter selalu menyertakan `page: 1` setiap kali query teks atau kategori berganti.
- [ ] Komponen `ProductFilters` bersifat murni terkontrol (*controlled component* tanpa state mandiri).
- [ ] Komponen `Pagination` otomatis menonaktifkan tombol di batas minimum (1) dan maksimum (`totalPages`).
- [ ] Halaman dapat di-refresh dan dibagikan link-nya tanpa kehilangan kondisi filter.
- [ ] `npm run lint` dan `npm run build` lulus tanpa kesalahan.

---

**Lanjut ke Minggu 4:** `04a-desain-responsif-dan-layout-mobile.md` (Desain Responsif & Layout Mobile)
