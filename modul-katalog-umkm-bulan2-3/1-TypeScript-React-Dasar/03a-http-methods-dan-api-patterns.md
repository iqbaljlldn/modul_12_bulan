# 3.0a HTTP Methods & API Patterns — PATCH, PUT, DELETE

## Tujuan sesi ini

Paham perbedaan **PATCH vs PUT vs DELETE**, konvensi REST, dan menulis fungsi API untuk update dan hapus produk — persiapan sebelum Slice 3.

## Bacaan wajib sebelum sesi

- **Bab 2.4** — API Integration & Async Operations (modul React, review bagian HTTP methods)
- **Bab 2.2** — Conditional Rendering & Lists (modul React, bagian advanced key handling)

## Konsep

### HTTP Methods — Ringkasan

| Method | Arti | Contoh | Body? |
|---|---|---|---|
| `GET` | Ambil data | `GET /products` → daftar produk | Tidak |
| `POST` | Buat data baru | `POST /products` → tambah produk | Ya |
| `PUT` | Ganti **seluruh** data | `PUT /products/1` → ganti semua field | Ya |
| `PATCH` | Ganti **sebagian** data | `PATCH /products/1` → ubah harga saja | Ya |
| `DELETE` | Hapus data | `DELETE /products/1` → hapus produk | Tidak |

**Di Katalog kita pakai PATCH** (bukan PUT), karena saat edit kita cuma kirim field yang berubah (misal harga dan stok saja), bukan seluruh objek produk.

### Status Code yang Perlu Diketahui

| Code | Arti | Kapan muncul |
|---|---|---|
| `200` | OK | Request berhasil, ada data yang dikembalikan |
| `201` | Created | Data baru berhasil dibuat (POST) |
| `204` | No Content | Berhasil tapi tidak ada data balikan (DELETE) |
| `400` | Bad Request | Data yang dikirim salah/tidak valid |
| `404` | Not Found | Data yang dicari tidak ada |
| `500` | Internal Server Error | Ada masalah di server |

### Custom Error Class — `ApiError`

Sampai sekarang error kita cuma `new Error('...')`. Masalahnya: kita tidak tahu apakah error itu dari API (misal 404) atau dari bug kode kita sendiri.

Solusinya: buat **class error khusus** yang menyimpan status code:

```ts
// src/errors/ApiError.ts
export class ApiError extends Error {
  status: number

  constructor(status: number, message: string) {
    super(message)
    this.name = 'ApiError'
    this.status = status
  }
}
```

Ini juga **perkenalan pertama ke `class` TypeScript** — konsep yang akan jauh lebih banyak dipakai di Bulan 3 saat NestJS.

### Fungsi API untuk Update & Delete

```ts
// src/api/products.ts

// Partial<T> → semua field jadi opsional (cocok untuk PATCH)
export type UpdateProductInput = Partial<CreateProductInput>

export function updateProduct(id: number, input: UpdateProductInput): Promise<Product> {
  return fetchJson<Product>(`/products/${id}`, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(input),
  })
}

export function deleteProduct(id: number): Promise<void> {
  return fetchJson<void>(`/products/${id}`, { method: 'DELETE' })
}
```

### Menangani 204 No Content

`DELETE` yang berhasil biasanya mengembalikan status `204` **tanpa body**. Kalau kita tetap coba `.json()`, akan error. Solusinya:

```ts
if (response.status === 204) {
  return undefined as T
}
```

## Latihan

1. Buka DevTools Network, lakukan POST (tambah produk dari Slice 2). Amati: method apa, status code apa, apa isi request body dan response body?
2. Coba request manual lewat **REST client** (bisa pakai extension VS Code seperti Thunder Client, atau `curl`):
   - `PATCH /products/1` dengan body `{ "price": 25000 }`
   - `DELETE /products/2`
   - Cek hasilnya di `localhost:3001/products`

## Cek pemahaman

- Apa bedanya PATCH dan PUT?
- Kenapa `UpdateProductInput` pakai `Partial`?
- Kapan status code 204 muncul dan kenapa perlu ditangani khusus?

---

Lanjut ke: **03b-edit-hapus-dan-error.md** (Slice 3)
