# 2.1d Latihan & Pemantapan Slice 5

> **Tujuan sesi:** Memperdalam pemahaman component composition, custom hook, dan isolasi kegagalan sebelum masuk ke validasi form di Slice 6.  
> **Format:** Blok 1 (Review singkat) → Blok 2 (Pairing & Eksperimen) → Blok 3 (Tugas Mandiri + PR Review Squad).

---

## Latihan 1: Terapkan Komponen Atomik `Badge.tsx` di `ProductCard.tsx` (Blok 2)

Di bab `01c`, kita masih menulis badge kategori dan badge status secara manual menggunakan elemen `<span>`:
```tsx
<span className="rounded bg-slate-100 px-2 py-0.5 text-xs font-medium text-slate-600">
  {categoryName}
</span>
```

Sekarang saatnya memaksimalkan komponen reusable `src/components/ui/Badge.tsx` yang sudah kita bangun di unit `01a` (`variant: 'neutral' | 'success' | 'warning' | 'info'`).

### Tugas:
1. Pastikan file `src/components/ui/Badge.tsx` mendukung 4 varian:
   - `neutral`: `bg-slate-100 text-slate-700`
   - `success`: `bg-emerald-50 text-emerald-700 border border-emerald-200`
   - `warning`: `bg-amber-50 text-amber-700 border border-amber-200`
   - `info`: `bg-sky-50 text-sky-700 border border-sky-200`
2. Ganti seluruh badge manual di `ProductCard.tsx` dengan `<Badge variant="...">...</Badge>`:
   - Nama kategori memakai varian `'neutral'`.
   - Status produk memakai `'success'` jika `'active'`, atau `'warning'` jika `'draft'`.
   - Jika `product.stock === 0`, tampilkan `<Badge variant="warning">Stok Habis</Badge>` *(atau varian `'info'` untuk label promo/pilihan jika ingin bereksperimen)*.

---

## Latihan 2: Pengujian Graceful Degradation (Ketahanan API — Blok 2)

Di aplikasi web profesional, jika salah satu endpoint pendukung (seperti kategori) gagal merespons, halaman utama produk **tidak boleh ikut mati total**.

### Skenario Pengujian:
1. Buka file `src/api/categories.ts`.
2. Ubah URL pemanggilan menjadi salah:
   ```ts
   export function getCategories(): Promise<Category[]> {
     return fetchJson<Category[]>('/categories-error-simulasi')
   }
   ```
3. Refresh browser di `http://localhost:5173`.
4. Amati apa yang terjadi:
   - Apakah daftar produk tetap tampil normal?
   - Apakah form tetap bisa dibuka tanpa error fatal?
   - Apa yang tampil di badge kategori pada kartu produk?
5. Kembalikan URL ke `/categories` setelah kamu memahami pentingnya menangani error secara terisolasi di dalam `useCategories`.

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan individual di kelas dan simpan hasilnya di repositori pribadimu pada:  
`tugas/tugas_01d.md`

1. Tuliskan identitas diri (Nama, Squad, Tanggal).
2. Salin cuplikan penggunaan `<Badge>` di `ProductCard.tsx`.
3. Catat hasil pengamatan saat endpoint `/categories` disimulasikan error: mengapa halaman produk tidak ikut layar putih?
4. Jalankan `npm run lint` dan `npm run build`, lalu tempelkan ringkasan output suksesnya.

---

## Checklist Code Review Dasar Slice 5 (PR Repo Pribadi)

Buat Pull Request dari branch fitur Slice 5 ke branch `main` repositori pribadimu, lalu minta minimal **1 rekan satu squad** me-review menggunakan checklist dasar berikut sebelum di-merge:

- [ ] **Nama & Struktur Jelas:** `useCategories`, `useProducts`, `Button`, `Input`, `Badge` memakai penamaan konsisten di folder masing-masing (`src/hooks/`, `src/components/ui/`).
- [ ] **Tipe TypeScript Benar:** Tidak ada `any`; `Button`/`Input`/`Badge` memakai `HTMLAttributes`/`ReactNode` yang tepat.
- [ ] **Cek Celah Bug:** Tailwind v4 aktif tanpa sisa CSS lama yang bentrok di `src/index.css`; `<select>` kategori di form dan `<Badge>` kategori di kartu berfungsi (`Number(product.category_id)`); endpoint kategori error tidak menjatuhkan daftar produk.
- [ ] **Bisa Dijalankan & Lolos Audit:** `npm run lint` (`oxlint`) dan `npm run build` lulus dengan **0 error dan 0 warning**.

---

## Misi Squad Mingguan (Persiapan Sprint Review 1 — Sabtu)

Walaupun setiap anggota membangun di **repositori pribadi (`katalog-umkm`)** masing-masing, squad menyiapkan demo berdurasi **12-15 menit** untuk Sprint Review Sabtu:

1. **Pastikan PR Keempat Anggota Ter-review:** Tidak ada anggota squad yang tertinggal tanpa review PR Slice 5.
2. **Siap Diundi Mentor:** Cek bersama bahwa `npm run dev`, `lint`, dan `build` berjalan normal di laptop ke-4 anggota.
3. **Pembagian Peran Demo Squad:**
   - **Driver Demo:** Mendemokan antarmuka baru Tailwind v4 + form dengan dropdown kategori + badge kategori di kartu.
   - **Code Explorer:** Membandingkan `ProductsPage.tsx` yang kini jauh lebih ramping setelah logika diekstrak ke `useProducts.ts`.
   - **Resilience & Bug Storyteller:** Mendemokan *graceful degradation* `/categories` dan menceritakan 1 bug migrasi Tailwind/Hooks minggu ini.

---

**Lanjut ke Minggu 2:** `02a-validasi-form-dan-arsitektur-input.md` (Validasi Form & Arsitektur Input)
