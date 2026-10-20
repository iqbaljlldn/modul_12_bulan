# 3.0c State Management Patterns — Lifting State & Alur Data

## Tujuan sesi ini

Merapikan dan memahami alur data di Katalog: **di mana state seharusnya tinggal**, **kapan state diangkat ke parent**, dan **pola update state yang aman**. Ini bukan materi baru — lebih ke refleksi dan konsolidasi pola yang sudah dipakai di Slice 0-3.

## Bacaan wajib sebelum sesi

**Bab 2.5 — State Management Lanjutan** (modul React): useReducer (pengenalan saja), lifting state, pola state yang lebih kompleks.

> Dari bab 2.5, yang **wajib** dipahami sekarang: **lifting state**. `useReducer` cukup dikenali konsepnya — belum wajib dipakai.

## Konsep

### Lifting State — Angkat State ke Parent

**Masalah:** dua komponen yang setara (sibling) butuh akses ke data yang sama.

**Solusi:** pindahkan state ke **parent** mereka, lalu kirim lewat props.

```text
Sebelum (salah):
  ProductCard A  →  punya state products sendiri
  ProductCard B  →  punya state products sendiri

Sesudah (benar):
  ProductsPage  →  punya state products
    ├── ProductCard A  →  terima product lewat props
    └── ProductCard B  →  terima product lewat props
```

Di Katalog kita, ini sudah terjadi:
- `ProductsPage` menyimpan `products` state
- `ProductList` dan `ProductCard` menerima data lewat props
- Saat produk diedit/dihapus, `handleSave`/`handleDelete` di `ProductsPage` yang mengubah state

### Pola Update State yang Sudah Kita Pakai

Tinjau ulang ketiga pola ini — semuanya sudah muncul di Slice 1-3:

```tsx
// 1. TAMBAH item (Slice 2)
setProducts((current) => [...current, created])

// 2. UPDATE item (Slice 3 — edit)
setProducts((current) => current.map((p) => p.id === id ? updated : p))

// 3. HAPUS item (Slice 3 — delete)
setProducts((current) => current.filter((p) => p.id !== id))
```

Ketiga pola ini punya kesamaan:
- Selalu pakai **callback form** `(current) => ...` — lebih aman dari race condition
- Selalu buat **array baru** — tidak pernah `.push()`, `.splice()`, atau mutasi langsung
- Kembalikan array yang sudah dimodifikasi

### Kapan State di Parent, Kapan di Child?

| State | Di mana | Alasan |
|---|---|---|
| `products` (daftar produk) | `ProductsPage` | Dipakai oleh `ProductList`, `ProductForm`, dan semua `ProductCard` |
| `isLoading`, `errorMessage` | `ProductsPage` | Terkait fetch data yang dilakukan di `ProductsPage` |
| `isEditing` | `ProductCard` | Hanya relevan untuk satu kartu — tidak perlu diketahui parent/sibling |
| `isSubmitting` | `ProductForm` / `ProductEditForm` | Hanya relevan selama proses submit satu form |
| `values` (isi form) | `ProductForm` | Hanya relevan di dalam form itu |

**Aturan simpel:** state tinggal di level **terendah** yang membutuhkannya. Angkat ke atas **hanya** kalau ada komponen lain yang juga perlu datanya.

### Kapan `useReducer` Dipakai? (Preview)

`useReducer` cocok saat:
- State punya banyak sub-value yang saling terkait
- Logic update-nya kompleks (banyak `if/switch`)
- Ingin memisahkan logic update dari komponen

Di Katalog kita **belum perlu** — `useState` masih cukup. Tapi kalau nanti di Bulan 5+ logic state makin rumit, `useReducer` jadi opsi.

## Latihan (refleksi)

1. **Gambar alur data:** buka kode `ProductsPage.tsx` dan gambar (di kertas/papan tulis) bagaimana data `products` mengalir ke `ProductList` → `ProductCard`, dan bagaimana event `onSave`/`onDelete` mengalir balik ke `ProductsPage`. Ini latihan **menjelaskan**, bukan coding.

2. **Identifikasi state:** buka semua komponen yang sudah kamu tulis. Untuk setiap `useState`, jawab: "Kenapa state ini ada di sini dan bukan di tempat lain?"

3. **Coba pindahkan:** bayangkan `isEditing` dipindahkan dari `ProductCard` ke `ProductsPage`. Apa yang harus berubah? Apakah jadi lebih baik atau lebih rumit?

## Cek pemahaman

- Kalau dua komponen sibling butuh data yang sama, apa yang harus dilakukan?
- Kenapa kita selalu buat array baru (bukan `.push()`) saat update state?
- Apa bedanya `setCount(count + 1)` dan `setCount((c) => c + 1)`?

## Kaitkan ke rujukan

**Bab 2.5** modul React untuk penjelasan lebih lengkap tentang lifting state dan pengenalan `useReducer`. Konsep Context API (untuk menghindari "prop drilling" terlalu dalam) akan dibahas di Bulan 3 (Slice 5-6).

---

Lanjut ke: **04a-react-router-dasar.md** (minggu 4)
