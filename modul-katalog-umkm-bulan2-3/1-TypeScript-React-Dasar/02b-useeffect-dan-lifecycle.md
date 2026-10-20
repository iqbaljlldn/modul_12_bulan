# 2.0b useEffect & Lifecycle — Side Effects di Komponen

## Tujuan sesi ini

Paham **kapan** dan **kenapa** pakai `useEffect`, apa itu "side effect", dan bagaimana dependency array mengontrol kapan efek dijalankan. Ini persiapan sebelum fetch data dari API di slice berikutnya.

## Bacaan wajib sebelum sesi

**Bab 2.3 — Component Lifecycle & useEffect Hook** (modul React): lifecycle phases, useEffect, cleanup function, dependency array.

## Ringkasan konsep (dari bab 2.3)

### Apa itu Side Effect?

**Side effect** = sesuatu yang terjadi "di luar" proses render komponen. Contoh:
- Mengambil data dari server (fetch)
- Mengubah judul halaman (`document.title`)
- Menjalankan timer (`setTimeout`, `setInterval`)
- Menambahkan event listener

Semua ini **tidak boleh** langsung ditulis di body fungsi komponen — harus dibungkus `useEffect`.

### Kenapa?

Fungsi komponen bisa dijalankan **berkali-kali** oleh React (setiap re-render). Kalau `fetch` ditulis langsung di body fungsi tanpa `useEffect`, data akan diambil ulang setiap kali komponen re-render — boros dan bisa menyebabkan loop tak terbatas.

### useEffect — Pola Dasar

```tsx
import { useEffect } from 'react'

function MyComponent() {
  useEffect(() => {
    // Kode side effect di sini
    console.log('Komponen sudah tampil!')
  }, []) // ← dependency array

  return <p>Halo</p>
}
```

### Dependency Array — Kapan Efek Dijalankan?

| Dependency array | Kapan efek jalan |
|---|---|
| `[]` (array kosong) | **Sekali** setelah render pertama (mount) |
| `[id]` | Setelah render pertama **dan** setiap `id` berubah |
| `[a, b]` | Setelah render pertama **dan** setiap `a` atau `b` berubah |
| Tidak ada (dihilangkan) | **Setiap** render — **biasanya salah**, jangan lakukan |

### Cleanup Function — Bersih-bersih

`useEffect` bisa mengembalikan fungsi yang dipanggil saat:
- Komponen **dibongkar** (unmount)
- Sebelum efek **dijalankan ulang** (kalau dependency berubah)

```tsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log('tick')
  }, 1000)

  // Cleanup: hentikan timer saat komponen dibongkar
  return () => {
    clearInterval(timer)
  }
}, [])
```

### Pola Fetch Data (preview — detail di Slice 1)

```tsx
useEffect(() => {
  let ignore = false  // ← mencegah update state setelah unmount

  async function loadData() {
    const response = await fetch('/api/products')
    const data = await response.json()
    if (!ignore) {
      setProducts(data)
    }
  }

  loadData()

  return () => {
    ignore = true  // ← cleanup
  }
}, [])
```

**Kenapa `ignore`?** Bayangkan user membuka halaman, lalu langsung pindah halaman lain sebelum fetch selesai. Tanpa `ignore`, React akan mencoba `setProducts` pada komponen yang sudah dibongkar — membuang resource dan bisa menyebabkan warning.

## Latihan (sebelum masuk ke slice)

1. **Log lifecycle:** buat komponen yang `console.log('mount')` saat pertama tampil dan `console.log('unmount')` saat dihapus. Pakai cleanup function.

2. **Timer:** buat komponen yang menampilkan detik yang berjalan (0, 1, 2, ...). Pakai `setInterval` di `useEffect` dan pastikan timer berhenti saat komponen di-unmount.

3. **Document title:** buat komponen `Counter` yang mengubah `document.title` menjadi `"Hitungan: X"` setiap kali `count` berubah. Pakai `[count]` di dependency array.

4. **Dependency array experiment:** di latihan 3, coba ganti `[count]` jadi `[]`. Apa yang terjadi pada title saat tombol diklik? Kenapa?

## Cek pemahaman

- Apa yang terjadi kalau dependency array dihilangkan (bukan `[]`, tapi benar-benar tidak ada)?
- Kapan cleanup function dipanggil?
- Kenapa fetch data harus di `useEffect`, bukan langsung di body fungsi komponen?

## Kesalahan umum

| Gejala | Sebab | Solusi |
|---|---|---|
| Fetch jalan terus-menerus (infinite loop) | Dependency array salah atau tidak ada | Pastikan ada `[]` atau dependency yang tepat |
| Warning "Can't perform state update on unmounted component" | Tidak ada cleanup / variabel `ignore` | Tambahkan cleanup function |
| Effect tidak jalan ulang saat data berubah | Lupa memasukkan variabel ke dependency array | Tambahkan variabel yang relevan ke `[...]` |

## Kaitkan ke rujukan

**Bab 2.3** modul React membahas lifecycle lebih mendalam, termasuk analogi dengan class component lifecycle methods. **Bab 2.4** (API Integration) — akan dibahas di sesi berikutnya (Slice 1).

---

Lanjut ke: **02c-fetch-dan-loading-state.md** (Slice 1)
