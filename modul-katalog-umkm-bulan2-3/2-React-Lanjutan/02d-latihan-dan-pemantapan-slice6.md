# 2.2d Latihan & Pemantapan Slice 6

> **Tujuan sesi:** Memperkuat penguasaan Context API dan validasi form melalui penambahan fitur varian toast dan penanganan interaksi input dinamis.  
> **Format:** Blok 2 (Pairing & Eksperimen) → Blok 3 (Tugas Mandiri + PR Review Squad).

---

## Latihan 1: Toast dengan Varian Warna (`success`, `error`, `info`)

Saat ini toast kita selalu berwarna gelap (`bg-slate-900`). Di aplikasi produksi, pengguna mengharapkan warna hijau untuk sukses dan merah untuk error.

### Tugas:
1. Perbarui tipe `Toast` di `src/context/ToastProvider.tsx` (ekspor `ToastType` dari `ToastContext.ts` agar dipakai bersama):
   ```ts
   // src/context/ToastContext.ts
   export type ToastType = 'success' | 'error' | 'info'

   export interface ToastContextValue {
     showToast: (message: string, type?: ToastType) => void
   }
   ```
   ```ts
   // src/context/ToastProvider.tsx
   interface Toast {
     id: number
     message: string
     type: ToastType
   }
   ```
2. Petakan warna berdasarkan tipe di `ToastProvider.tsx` (default `type = 'info'`):
   - `success`: `bg-emerald-600 text-white`
   - `error`: `bg-red-600 text-white`
   - `info`: `bg-slate-900 text-white`
3. Perbarui panggilan `showToast`: gunakan `'success'` saat tambah/ubah/hapus berhasil, dan bungkus `remove(id)` di `ProductsPage.tsx` dengan `try/catch` untuk memanggil `showToast('Gagal menghapus produk', 'error')` jika API gagal.

---

## Latihan 2: Real-time Error Clearance (Bersihkan Error saat Mengetik)

Saat ini, pesan error tetap muncul sampai form di-submit ulang. UX yang lebih baik adalah **menghilangkan pesan error begitu user mulai memperbaiki inputnya**.

### Tugas:
Di `ProductForm.tsx`, buat fungsi bantuan pembaruan field teks (`name`, `description`, `price`, `stock`, `merchant_name`) yang sekaligus membersihkan error field bersangkutan:

```tsx
type TextField = 'name' | 'description' | 'price' | 'stock' | 'merchant_name'

function handleFieldChange(field: TextField, value: string) {
  setValues((prev) => ({ ...prev, [field]: value }))

  // Jika field ini sebelumnya punya error, bersihkan saat user mulai mengetik
  if (field !== 'description' && fieldErrors[field]) {
    setFieldErrors((prev) => ({ ...prev, [field]: undefined }))
  }
}
```

Terapkan fungsi ini pada `onChange` komponen `<Input>` yang relevan.

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan individual di kelas dan simpan hasilnya di repositori proyekmu pada:  
`tugas/tugas_02d.md`

1. Tuliskan identitas diri (Nama, Squad, Tanggal).
2. Jelaskan skenario uji saat `json-server` dimatikan (`dev:web` saja) lalu tombol hapus diklik: toast varian apa yang muncul?
3. Jalankan `npm run lint` dan `npm run build` dan tempelkan output suksesnya.

---

## Checklist Code Review Dasar Slice 6 (PR Repo Pribadi)

Ajukan PR ke branch `main` repositori pribadimu, lalu minta review minimal **1 rekan satu squad**:

- [ ] **Nama & Struktur Jelas:** Fungsi validasi murni (`validate`, `validateEdit`) terisolasi di `src/utils/validate.ts`; Context terstruktur dalam 3 file terpisah (`ToastContext.ts`, `ToastProvider.tsx`, `useToast.ts`).
- [ ] **Tipe TypeScript Benar:** `FormErrors`, `RawValues`, dan `ToastType` didefinisikan eksplisit tanpa `any`.
- [ ] **Cek Celah Bug:** Elemen `<Input>` memakai `error` + `aria-invalid`; `<ToastProvider>` membungkus `<App />` di `main.tsx`; submit form invalid tidak memicu HTTP `POST`/`PATCH`; toast error muncul saat API gagal.
- [ ] **Bisa Dijalankan & Lolos Audit:** `npm run lint` (`oxlint`) dan `npm run build` lulus tanpa kesalahan atau warning.

---

## Misi Squad Mingguan (Persiapan Sprint Review 2 & Retrospektif Tengah Bulan — Sabtu)

1. **PR Cross-Review Antaranggota:** Pastikan ke-4 anggota squad sudah selesai me-review PR Slice 6 masing-masing dan mengetes form invalid bersama.
2. **Siap Diundi Mentor:** Cek kesiapan aplikasi dan kelengkapan `npm run lint` / `npm run build` di keempat laptop.
3. **Pembagian Peran Demo Squad (12-15 menit):**
   - **Driver Demo:** Mendemokan form invalid (border merah + tidak ada request Network) → form valid + toast hijau → toast merah error saat server dimatikan.
   - **Architecture Narrator:** Menjelaskan arsitektur 3 file Context API vs bahaya Prop Drilling & Fast Refresh.
   - **Bug & Retro Storyteller:** Menyiapkan poin utama **Retrospektif Tengah Bulan** squad (apa yang berjalan lancar & apa yang perlu diperbaiki di Minggu 3).

---

**Lanjut ke Minggu 3:** `03a-debounce-dan-optimasi-input.md` (Debounce & Optimasi Input)
