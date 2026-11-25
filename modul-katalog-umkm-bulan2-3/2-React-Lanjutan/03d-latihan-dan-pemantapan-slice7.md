# 2.3d Latihan & Pemantapan Slice 7

> **Tujuan sesi:** Memperdalam pemahaman arsitektur state di URL, penanganan kondisi tepi (*edge cases*) pencarian kosong, dan tombol reset filter.  
> **Format:** Blok 2 (Pairing & Eksperimen) → Blok 3 (Tugas Mandiri + PR Review Squad).

---

## Latihan 1: Tampilan Status Kosong (*Empty State*) & Reset Filter (Blok 2)

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

## Latihan 2: Pengujian Navigasi Riwayat Browser (Back & Forward — Blok 2)

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

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan individual di kelas dan simpan hasilnya di repositori proyekmu pada:  
`tugas/tugas_03d.md`

1. Tuliskan identitas diri (Nama, Squad, Tanggal).
2. Dokumentasikan skenario uji Empty State & tombol Back/Forward: apa yang muncul di layar saat kata kunci `"zzzzzzz"` diketik, dan apakah `Reset Semua Filter` membersihkan query string URL?
3. Jalankan `npm run lint` dan `npm run build` dan tempelkan output suksesnya.

---

## Checklist Code Review Dasar Slice 7 (PR Repo Pribadi)

Ajukan PR ke branch `main` repositori pribadimu, lalu minta review minimal **1 rekan satu squad**:

- [ ] **Nama & Struktur Jelas:** `fetchPage`, `useDebouncedValue`, `ProductFilters`, `Pagination` dan tipe `ProductFilters` tertata rapi.
- [ ] **Tipe TypeScript Benar:** Header `X-Total-Count` dibaca via `fetchPage<T>` tanpa `any`; props `ProductFilters` dan `Pagination` bertipe eksplisit.
- [ ] **Cek Celah Bug:** `useDebouncedValue` punya cleanup `clearTimeout`; `urlFilters.q` terpisah dari `activeFilters.q`; perubahan filter mereset `page: 1`; `F5` dan tombol Back/Forward mempertahankan filter.
- [ ] **Bisa Dijalankan & Lolos Audit:** `npm run lint` (`oxlint`) dan `npm run build` lulus tanpa kesalahan atau warning.

---

## Misi Squad Mingguan (Persiapan Sprint Review 3 — Sabtu)

1. **PR Cross-Review Antaranggota:** Pastikan ke-4 anggota squad sudah selesai me-review PR Slice 7 masing-masing.
2. **Siap Diundi Mentor:** Cek bersama bahwa `db.seed.json` punya cukup data uji (minimal > 6 produk bila ingin menguji 2 halaman, atau klik `Tambah Produk` agar pagination aktif di keempat laptop!).
3. **Pembagian Peran Demo Squad (12-15 menit):**
   - **Driver Demo:** Mendemokan ketik pencarian → ganti kategori → pindah halaman 2 → tekan **F5** (filter tetap utuh) → uji `"zzzzzzz"` (*Empty State*) → Reset Filter.
   - **Network Inspector:** Membuktikan jeda debounce 400ms (hanya 1 request terkirim) dan menunjukkan header `X-Total-Count` di tab Response Headers.
   - **Code & Bug Storyteller:** Menjelaskan kenapa dependency array `useProducts` harus field-by-field (`filters.q`, dst) dan menceritakan 1 bug paling berkesan minggu ini.

---

**Lanjut ke Minggu 4:** `04a-desain-responsif-dan-layout-mobile.md` (Desain Responsif & Layout Mobile)
