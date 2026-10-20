# 2.1d Latihan & Pemantapan Slice 5

> **Tujuan sesi:** Memperdalam pemahaman component composition, custom hook, dan isolasi kegagalan sebelum masuk ke validasi form di Slice 6.  
> **Format:** Praktik mandiri / pair programming (45-60 menit) + peer review santai.

---

## Latihan 1: Ekstraksi Komponen Atomik `Badge.tsx`

Di bab `01c`, kita menulis badge kategori dan badge status langsung menggunakan kelas Tailwind:
```tsx
<span className="rounded bg-slate-100 px-2 py-0.5 text-xs font-medium text-slate-600">
  {categoryName}
</span>
```

### Tugas:
1. Buat file `src/components/ui/Badge.tsx`.
2. Definisikan tipe varian:
   ```ts
   type BadgeVariant = 'neutral' | 'success' | 'warning' | 'info'
   ```
3. Petakan varian ke kelas Tailwind yang harmonis:
   - `neutral`: `bg-slate-100 text-slate-700`
   - `success`: `bg-emerald-50 text-emerald-700 border border-emerald-200`
   - `warning`: `bg-amber-50 text-amber-700 border border-amber-200`
   - `info`: `bg-sky-50 text-sky-700 border border-sky-200`
4. Ganti seluruh badge manual di `ProductCard.tsx` dengan komponen `<Badge variant="...">...</Badge>`.

---

## Latihan 2: Pengujian Graceful Degradation (Ketahanan API)

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

## Checklist Code Review Slice 5

Sebelum membuat Pull Request ke branch utama squad:

- [ ] Tailwind terpasang dengan benar dan tidak ada CSS lama yang tertinggal di `index.css`.
- [ ] Komponen `Button` dan `Input` di `src/components/ui/` memakai TypeScript `HTMLAttributes` yang benar.
- [ ] Custom hook `useCategories` dan `useProducts` berada di folder `src/hooks/`.
- [ ] Form tambah dan edit produk memiliki dropdown `<select>` kategori yang berfungsi.
- [ ] Kartu produk menampilkan badge nama kategori yang sesuai.
- [ ] `ProductsPage.tsx` bersih dan tidak memuat `fetch` langsung.
- [ ] Jalankan `npm run lint` dan `npm run build` — pastikan 0 error dan 0 warning!

---

**Lanjut ke Minggu 2:** `02a-validasi-form-dan-arsitektur-input.md` (Validasi Form & Arsitektur Input)
