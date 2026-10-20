# 2.2d Latihan & Pemantapan Slice 6

> **Tujuan sesi:** Memperkuat penguasaan Context API dan validasi form melalui penambahan fitur varian toast dan penanganan interaksi input dinamis.  
> **Format:** Praktik mandiri / pair programming (45-60 menit) + peer review.

---

## Latihan 1: Toast dengan Varian Warna (`success`, `error`, `info`)

Saat ini toast kita selalu berwarna hitam (`bg-slate-900`). Di aplikasi produksi, pengguna mengharapkan warna hijau untuk sukses dan merah untuk error.

### Tugas:
1. Perbarui tipe `Toast` di `src/context/ToastProvider.tsx`:
   ```ts
   type ToastType = 'success' | 'error' | 'info'

   interface Toast {
     id: number
     message: string
     type: ToastType
   }
   ```
2. Perbarui `ToastContextValue` di `src/context/ToastContext.ts`:
   ```ts
   export interface ToastContextValue {
     showToast: (message: string, type?: ToastType) => void
   }
   ```
3. Petakan warna berdasarkan tipe:
   - `success`: `bg-emerald-600 text-white`
   - `error`: `bg-red-600 text-white`
   - `info`: `bg-slate-900 text-white`
4. Panggil `showToast('Gagal menghapus produk', 'error')` jika request API gagal di blok `catch`.

---

## Latihan 2: Real-time Error Clearance (Bersihkan Error saat Mengetik)

Saat ini, pesan error tetap muncul sampai form di-submit ulang. UX yang lebih baik adalah **menghilangkan pesan error begitu user mulai memperbaiki inputnya**.

### Tugas:
Di `ProductForm.tsx`, buat fungsi bantuan pembaruan field yang sekaligus membersihkan error field bersangkutan:

```tsx
function handleFieldChange(field: keyof typeof values, value: string) {
  setValues((prev) => ({ ...prev, [field]: value }))
  
  // Jika field ini sebelumnya punya error, bersihkan saat user mulai mengetik
  if (fieldErrors[field]) {
    setFieldErrors((prev) => ({ ...prev, [field]: undefined }))
  }
}
```

Terapkan fungsi ini pada `onChange` di setiap komponen `<Input>`.

---

## Checklist Code Review Slice 6

Sebelum mengajukan PR ke branch tim:

- [ ] Fungsi validasi murni terisolasi rapi di `src/utils/validate.ts`.
- [ ] Tipe `FormErrors` dan `RawValues` didefinisikan secara eksplisit.
- [ ] Elemen `<Input>` menggunakan prop `error` dan atribut `aria-invalid`.
- [ ] Context toast terstruktur dalam 3 file terpisah (`ToastContext.ts`, `ToastProvider.tsx`, `useToast.ts`).
- [ ] `<ToastProvider>` terpasang di level tertinggi aplikasi (`main.tsx`).
- [ ] Tombol submit memvalidasi input sebelum memanggil fungsi API.
- [ ] Toast muncul saat sukses tambah, ubah, dan hapus.
- [ ] `npm run lint` dan `npm run build` lulus tanpa kesalahan.

---

**Lanjut ke Minggu 3:** `03a-debounce-dan-optimasi-input.md` (Debounce & Optimasi Input)
