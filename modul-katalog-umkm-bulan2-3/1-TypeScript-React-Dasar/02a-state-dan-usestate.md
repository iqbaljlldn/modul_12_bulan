# 2.0a State & useState — Data yang Berubah di Dalam Komponen

## Tujuan Sesi Ini

Memahami **kapan** dan **kenapa** kita menggunakan state (bukan variabel biasa atau props), menguasai konsep **daya ingat komponen** lewat hook `useState`, dan mempraktikkan prinsip **kekekalan data (*immutability*)** saat memperbarui state.

---

## Aktivitas Terbimbing di Kelas (Blok 1, 10-15 Menit)

Mentor akan memandu pembahasan konsep inti:
- Mengapa variabel JavaScript biasa (`let total = 0`) selalu ter-reset setiap kali fungsi komponen dijalankan ulang oleh React.
- Anatomi hook `useState`: sepasang nilai saat ini (*current value*) dan fungsi pengubah (*setter function*).
- Siklus hidup render ulang (*re-render cycle*) yang dipicu oleh pemanggilan fungsi setter.
- Prinsip *Immutability* (larangan mengubah objek/array secara langsung tanpa membuat salinan baru).

*(Bahan bacaan pendalaman opsional: Modul React Bootcamp Bab 1.5 tentang State dan useState Hook).*

---

## Ringkasan Konsep Kunci & Analogi

### 1. Variabel Biasa vs State

> **Analogi Sehari-hari:**  
> - **Variabel Biasa (`let x = 0`)** seperti menulis catatan pesanan di atas **selembar tisu basah**: begitu pelayan selesai menyajikan makanan (proses render selesai), kertas tisu itu dibuang ke tong sampah. Saat meja baru datang, pelayan mulai dari tisu kosong lagi.  
> - **State (`useState`)** seperti **papan tulis putih mini (*whiteboard*) yang terpasang kokoh di meja kasir**: kasir bisa menghapus angka lama dan menulis angka baru menggunakan spidol khusus (fungsi *setter*). Catatan di papan tulis tersebut tetap aman dan tidak hilang meskipun pelayan bolak-balik menyajikan makanan.

### 2. Apa itu Hook di React?

> **Analogi Hook:**  
> Komponen React pada dasarnya hanyalah fungsi JavaScript biasa. Agar fungsi biasa ini memiliki "kekuatan khusus" (seperti kemampuan mengingat memori atau berbicara dengan server), komponen meminjam alat bantu dari kotak perkakas resmi React.  
> Semua perkakas ini diawali dengan kata **`use`** (misalnya `useState`, `useEffect`).

---

## Aturan Emas Bekerja dengan State

### 1. Dilarang Mutasi Langsung!
Jangan pernah mengubah isi variabel state secara langsung menggunakan operator penugasan (`=`) atau metode mutasi array (`.push()`, `.splice()`).

```tsx
// ❌ FATAL: Mutasi langsung! React tidak tahu ada data yang berubah
count = count + 1
items.push('Produk Baru')

// ✅ BENAR: Selalu gunakan fungsi setter dengan nilai baru atau salinan baru
setCount(count + 1)
setItems([...items, 'Produk Baru'])
```

### 2. Pola Pembaruan Berdasarkan Nilai Sebelumnya (Functional Updater)
Gunakan fungsi pembaruan (*updater callback*) jika nilai baru bergantung pada nilai saat ini:

```tsx
// Sangat aman dari risiko race condition
setCount((currentCount) => currentCount + 1)
```

### 3. Tiga Jurus Utama Memperbarui Array State

Perhatikan tiga jurus ini karena akan dipakai di seluruh operasi CRUD Katalog UMKM:

```tsx
// Jurus 1: MENAMBAH item baru (Spread Operator)
setProducts((current) => [...current, newProduct])

// Jurus 2: MENGHAPUS item tertentu (.filter)
setProducts((current) => current.filter((item) => item.id !== targetId))

// Jurus 3: MENGUBAH satu item di dalam daftar (.map)
setProducts((current) =>
  current.map((item) => (item.id === targetId ? { ...item, price: newPrice } : item))
)
```

---

## Latihan Kode Interaktif Terbimbing

Perhatikan komponen `ProductCounter` di bawah ini. Lengkapi bagian `// TODO:` agar tombol penambah dan pereset berfungsi:

```tsx
// src/components/ProductCounter.tsx
import { useState } from 'react'

function ProductCounter() {
  const [quantity, setQuantity] = useState<number>(1)

  function handleIncrement() {
    // TODO 1: Tambahkan jumlah quantity sebanyak 1 menggunakan functional updater
    setQuantity((prev) => prev + 1)
  }

  function handleDecrement() {
    // TODO 2: Kurangi quantity sebanyak 1, tetapi cegah agar nilai tidak kurang dari 1
    setQuantity((prev) => (prev > 1 ? prev - 1 : 1))
  }

  function handleReset() {
    // TODO 3: Kembalikan nilai quantity ke angka 1
    setQuantity(1)
  }

  return (
    <div className="counter-box">
      <p>Jumlah Pesanan: <strong>{quantity}</strong></p>
      <div style={{ display: 'flex', gap: '8px' }}>
        <button type="button" onClick={handleDecrement}>-</button>
        <button type="button" onClick={handleIncrement}>+</button>
        <button type="button" onClick={handleReset}>Reset</button>
      </div>
    </div>
  )
}

export default ProductCounter
```

---

## Analisis Bug & Prediksi (Aktivitas Blok 2)

Diskusikan bersama rekan pairing:

1. **Prediksi Jebakan Mutasi Array:**  
   Perhatikan potongan kode berikut:
   ```tsx
   const [tags, setTags] = useState<string[]>(['makanan', 'murah'])

   function addTag() {
     tags.push('laris')
     setTags(tags)
   }
   ```
   *Pertanyaan:* Mengapa saat tombol yang memanggil `addTag()` diklik, tampilan layar **tidak kunjung bertambah** kata `'laris'`, meskipun jika di-`console.log(tags)` katanya sebenarnya masuk?  
   *(Petunjuk: pikirkan bagaimana React membandingkan alamat memori objek).*
2. **Perbaiki Kode:**  
   Tuliskan satu baris perbaikan yang benar untuk fungsi `addTag()` di atas!

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan secara mandiri di kelas. Simpan hasilnya di:  
`tugas/squad-<nomor>/<nama-kamu>/tugas_02a.md`

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Tuliskan identitas diri (Nama, Squad, Tanggal).
3. Buat sebuah rancangan komponen mini React bernama `StockToggle.tsx`:
   - Komponen memiliki state boolean `isOpen` (nilai awal `false`).
   - Terdapat sebuah tombol bertuliskan: *"Lihat Jam Operasional UMKM"*.
   - Saat tombol diklik, nilai `isOpen` dibalik (`true` jadi `false`, `false` jadi `true`).
   - Jika `isOpen === true`, tampilkan paragraf: `<p>Buka setiap hari: 08.00 - 17.00 WIB</p>`.
   - Tuliskan kode lengkap komponen tersebut di dalam dokumen tugas.
4. Jawab 2 pertanyaan singkat:
   - Apa yang sebenarnya terjadi di balik layar saat fungsi `setter` (seperti `setIsOpen`) dipanggil oleh React?
   - Mengapa kita dilarang keras mengubah state array secara langsung menggunakan metode `.push()`?
5. Ajukan Pull Request ke repository squad untuk diperiksa rekan.

### Contoh Format Hasil (`tugas_02a.md`)

```markdown
# Tugas Mandiri 02a — State & useState
Nama: Rian Pratama
Squad: Squad 5
Tanggal: 9 November 2026

## 1. Kode Komponen StockToggle
```tsx
import { useState } from 'react'

function StockToggle() {
  const [isOpen, setIsOpen] = useState<boolean>(false)

  return (
    <div className="operational-box">
      <button type="button" onClick={() => setIsOpen((prev) => !prev)}>
        {isOpen ? 'Tutup Info Jam Operasional' : 'Lihat Jam Operasional UMKM'}
      </button>

      {isOpen && (
        <p className="schedule-text">
          Buka setiap hari: 08.00 - 17.00 WIB
        </p>
      )}
    </div>
  )
}

export default StockToggle
```

## 2. Jawaban Pertanyaan Pemahaman
1. Saat fungsi setter dipanggil, React menjadwalkan pembaharuan nilai state di memorinya. Kemudian React memanggil ulang (*re-render*) fungsi komponen tersebut dengan nilai state yang baru, menghitung perbedaannya via Virtual DOM, dan memperbarui elemen DOM browser yang relevan.
2. Karena React mendeteksi perubahan state dengan membandingkan alamat referensi memori (*reference equality check*). Jika kita melakukan `.push()`, alamat memori array tetap sama persis, sehingga React mengira tidak ada perubahan apa pun dan tidak melakukan re-render ke layar.
```

---

Lanjut ke: **02b-useeffect-dan-lifecycle.md**
