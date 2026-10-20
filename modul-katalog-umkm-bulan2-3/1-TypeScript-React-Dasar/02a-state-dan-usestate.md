# 2.0a State & useState — Data yang Berubah di Dalam Komponen

## Tujuan sesi ini

Paham **kapan** dan **kenapa** pakai state (bukan props), dan bisa memakai `useState` untuk membuat komponen yang interaktif.

## Bacaan wajib sebelum sesi

**Bab 1.5 — State dan useState Hook** (modul React): konsep state vs props, useState, re-rendering, state objek/array.

## Ringkasan konsep (dari bab 1.5)

### State vs Props — Kapan Pakai yang Mana?

| | Props | State |
|---|---|---|
| **Dari mana** | Dikirim oleh komponen **induk** | Dikelola **di dalam** komponen itu sendiri |
| **Bisa diubah?** | Tidak (read-only) | Ya, lewat setter function |
| **Contoh** | `product` yang dikirim ke `ProductCard` | `isEditing` di dalam `ProductCard` |
| **Kalau berubah?** | Komponen di-render ulang oleh induknya | Komponen di-render ulang oleh React |

**Aturan sederhana:** kalau datanya datang dari luar → props. Kalau datanya dikelola sendiri dan bisa berubah → state.

### useState — Hook Pertama

```tsx
import { useState } from 'react'

function Counter() {
  const [count, setCount] = useState(0)  // [nilai saat ini, fungsi untuk mengubah]

  return (
    <div>
      <p>Hitungan: {count}</p>
      <button onClick={() => setCount(count + 1)}>Tambah</button>
    </div>
  )
}
```

**Apa yang terjadi saat `setCount` dipanggil:**
1. React menyimpan nilai baru
2. Komponen di-**render ulang** (fungsi `Counter` dijalankan lagi)
3. `count` sekarang bernilai baru
4. JSX berubah sesuai data baru

### Aturan Penting

1. **Jangan ubah state langsung** — selalu lewat setter:
   ```tsx
   // ❌ SALAH
   count = count + 1
   
   // ✅ BENAR
   setCount(count + 1)
   ```

2. **State bisa bertipe apa saja** — `number`, `string`, `boolean`, `object`, `array`:
   ```tsx
   const [name, setName] = useState('')
   const [isOpen, setIsOpen] = useState(false)
   const [items, setItems] = useState<string[]>([])
   ```

3. **Update state berdasarkan state sebelumnya** — pakai callback form:
   ```tsx
   // ✅ Lebih aman, terutama kalau ada banyak update beruntun
   setCount((current) => current + 1)
   ```

### State yang Berupa Objek/Array

Kalau state-nya objek, **jangan mutasi langsung** — buat objek baru:

```tsx
const [user, setUser] = useState({ name: '', age: 0 })

// ❌ SALAH — mutasi langsung
user.name = 'Budi'

// ✅ BENAR — buat objek baru dengan spread
setUser({ ...user, name: 'Budi' })
// atau lebih aman:
setUser((current) => ({ ...current, name: 'Budi' }))
```

Untuk array:

```tsx
const [items, setItems] = useState<string[]>([])

// Tambah item
setItems((current) => [...current, 'item baru'])

// Hapus item
setItems((current) => current.filter((item) => item !== 'item yang dihapus'))

// Update item
setItems((current) => current.map((item) => item === 'lama' ? 'baru' : item))
```

> **Pola ini akan kamu pakai terus** di slice-slice berikutnya (tambah produk, edit produk, hapus produk). Latihannya sekarang, terapkan di Katalog nanti.

## Latihan (sebelum masuk ke slice)

1. **Counter:** buat komponen `Counter` dengan tombol +, −, dan reset. Tampilkan angkanya.
2. **Toggle:** buat komponen yang menampilkan/sembunyikan teks saat tombol diklik (`isVisible` state).
3. **Daftar:** buat komponen dengan input dan tombol "Tambah". Ketik nama → klik Tambah → nama masuk ke daftar di bawahnya. Pakai `useState<string[]>`.

Latihan ini kecil tapi penting — kalau `useState` belum "klik", slice berikutnya akan terasa berat.

## Cek pemahaman

- Apa yang terjadi pada komponen saat `setState` dipanggil?
- Kenapa kita tidak boleh menulis `items.push('baru')` untuk menambah item ke array state?
- Kapan sebaiknya pakai callback form (`setCount((c) => c + 1)`) vs langsung (`setCount(count + 1)`)?

## Kaitkan ke rujukan

**Bab 1.5** modul React membahas `useState` lebih lengkap, termasuk contoh dengan beberapa state variable dan state bertipe objek. Bab **2.5** (State Management Lanjutan) akan dibahas di minggu 3.

---

Lanjut ke: **02b-useeffect-dan-lifecycle.md**
