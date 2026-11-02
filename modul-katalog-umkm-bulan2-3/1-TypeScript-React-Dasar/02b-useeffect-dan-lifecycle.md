# 2.0b useEffect & Lifecycle — Menangani Side Effects

## Tujuan Sesi Ini

Memahami **kapan** dan **kenapa** kita menggunakan hook `useEffect`, apa yang dimaksud dengan efek samping (*side effect*), bagaimana *dependency array* mengontrol jadwal eksekusi efek, dan cara mencegah kebocoran memori dengan fungsi pembersih (*cleanup function*).

---

## Aktivitas Terbimbing di Kelas (Blok 1, 10-15 Menit)

Mentor akan memandu demonstrasi konsep inti:
- Mengapa panggilan data asinkron (*fetch*) tidak boleh diletakkan langsung di badan utama (*body*) fungsi komponen.
- Siklus hidup komponen: saat dipasang pertama kali (*mount*), saat diperbarui (*update*), dan saat dilepas (*unmount*).
- 3 variasi perilaku *dependency array*: tanpa array, array kosong `[]`, dan array berisi variabel `[id]`.
- Mencegah bahaya *memory leak* dan *race condition* menggunakan pola bendera pembersih `ignore = true`.

*(Bahan bacaan pendalaman opsional: Modul React Bootcamp Bab 2.3 tentang Component Lifecycle & useEffect).*

---

## Ringkasan Konsep Kunci & Analogi

### 1. Apa itu Side Effect?

> **Analogi Sehari-hari:**  
> Tugas utama fungsi komponen React hanyalah satu: **meracik tampilan visual (JSX) berdasarkan props dan state**.  
> Bayangkan seorang koki restoran yang tugas utamanya menata makanan di atas piring.  
> Jika di tengah-tengah menata piring koki tersebut tiba-tiba meninggalkan dapur untuk pergi ke pasar menagih barang (mengambil data dari server) atau mengecat dinding restoran (mengubah `document.title`), restorannya akan kacau!  
> Semua pekerjaan di luar peracikan piring ini disebut **Side Effect**. Pekerjaan ini harus diserahkan kepada pengingat khusus: hook **`useEffect`**.

### 2. Memahami Dependency Array

Tabel jadwal kerja `useEffect`:

| Dependency Array | Kapan Efek Dijalankan? | Contoh Penggunaan Nyata |
|---|---|---|
| **`[]` (Array kosong)** | **Hanya 1 kali** tepat setelah komponen pertama kali tampil di layar (*mount*). | Mengambil daftar produk awal dari API. |
| **`[id]` (Berisi variabel)** | Saat pertama kali tampil **DAN setiap kali nilai `id` berubah**. | Mengambil data detail produk baru saat user mengklik produk lain. |
| **Tidak ada array sama sekali** | **Setiap kali** komponen re-render (bisa ratusan kali per detik!). | ⚠️ **Hampir selalu merupakan bug!** Sangat berbahaya karena bisa memicu *infinite loop*. |

### 3. Mengapa Butuh Cleanup Function?

> **Analogi Cleanup:**  
> Saat tamu meninggalkan meja restoran (*unmount*), pelayan harus membersihkan meja: mematikan lilin, menghentikan musik meja, dan mencabut pesanan yang belum sempat dimasak.  
> Fungsi pembersih (*cleanup function*) yang di-`return` oleh `useEffect` bertugas menghentikan timer (`clearInterval`) atau mengabaikan balasan data server yang terlambat datang.

---

## Pola Baku Pengambilan Data (Preview Slice 1)

Perhatikan kerangka baku di bawah ini. Tiga bagian ini (`try`, `catch`, `finally`, dan bendera `ignore`) adalah pola yang akan kamu pakai terus:

```tsx
useEffect(() => {
  // 1. Siapkan penanda apakah komponen masih aktif di layar
  let ignore = false

  async function loadData() {
    try {
      const response = await fetch('http://localhost:3001/products')
      const data = await response.json()

      // 2. Hanya perbarui state jika user BELUM berpindah halaman
      if (!ignore) {
        setProducts(data)
      }
    } catch (error) {
      if (!ignore) {
        setErrorMessage('Gagal memuat data dari server')
      }
    } finally {
      if (!ignore) {
        setIsLoading(false)
      }
    }
  }

  loadData()

  // 3. Fungsi pembersih: dijalankan jika komponen dilepas dari layar
  return () => {
    ignore = true
  }
}, []) // Array kosong: hanya jalankan sekali saat mount
```

---

## Latihan Terbimbing: Timer Sederhana

Perhatikan komponen di bawah. Lengkapi bagian `// TODO:` agar timer berhenti saat komponen ditutup:

```tsx
// src/components/SimpleTimer.tsx
import { useEffect, useState } from 'react'

function SimpleTimer() {
  const [seconds, setSeconds] = useState<number>(0)

  useEffect(() => {
    // Jalankan penambah detik setiap 1000 milidetik (1 detik)
    const timerId = setInterval(() => {
      setSeconds((prev) => prev + 1)
    }, 1000)

    // TODO: Kembalikan fungsi pembersih (cleanup) untuk menghentikan timer
    return () => {
      clearInterval(timerId)
    }
  }, [])

  return <p>Waktu sesi belajar berjalan: {seconds} detik</p>
}

export default SimpleTimer
```

---

## Analisis Bug & Prediksi (Aktivitas Blok 2)

Diskusikan bersama rekan pairing:

1. **Prediksi Bencana Infinite Loop:**  
   Perhatikan potongan kode ini:
   ```tsx
   function BadComponent() {
     const [count, setCount] = useState(0)

     useEffect(() => {
       setCount(count + 1)
     }) // Lupa tidak memberi dependency array!

     return <h1>Angka: {count}</h1>
   }
   ```
   *Pertanyaan:* Jelaskan urutan bencana yang terjadi di browser saat kode ini dijalankan! Mengapa browser bisa hang atau freeze?
2. **Kuis Dependency:**  
   Jika di dalam `useEffect` kamu menggunakan variabel `productId`, apa yang wajib kamu cantumkan di dalam tanda kurung siku `[...]`?

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan secara mandiri di kelas. Simpan hasilnya di:  
`tugas/squad-<nomor>/<nama-kamu>/tugas_02b.md`

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Tuliskan identitas diri (Nama, Squad, Tanggal).
3. Buat sebuah rancangan komponen React bernama `DocumentTitleUpdater.tsx`:
   - Komponen memiliki state `productCount` bertipe number (nilai awal `0`).
   - Komponen memiliki tombol untuk menambah `productCount` sebanyak 1.
   - Gunakan `useEffect` untuk memperbarui judul tab browser (`document.title`) menjadi:  
     `"Ada X Produk - Katalog UMKM"`.
   - Pastikan kamu menentukan *dependency array* yang tepat agar judul tab browser sinkron setiap kali `productCount` berubah.
   - Tuliskan kode lengkap komponen tersebut di dalam dokumen tugas.
4. Jawab 2 pertanyaan singkat:
   - Apa perbedaan perilaku jika `useEffect` diberikan dependency array `[]` dibandingkan jika dependency array-nya sengaja dikosongkan/dihilangkan sama sekali?
   - Mengapa variabel `let ignore = false` di dalam `useEffect` sangat penting saat kita mengambil data dengan `fetch`? Apa bahayanya jika tidak ada variabel tersebut?
5. Ajukan Pull Request ke repositori squad.

### Contoh Format Hasil (`tugas_02b.md`)

```markdown
# Tugas Mandiri 02b — useEffect & Lifecycle
Nama: Dewi Lestari
Squad: Squad 6
Tanggal: 10 November 2026

## 1. Kode Komponen DocumentTitleUpdater
```tsx
import { useEffect, useState } from 'react'

function DocumentTitleUpdater() {
  const [productCount, setProductCount] = useState<number>(0)

  useEffect(() => {
    document.title = `Ada ${productCount} Produk - Katalog UMKM`
  }, [productCount]) // Berjalan saat pertama kali mount dan setiap productCount berubah

  return (
    <div>
      <p>Jumlah Produk: {productCount}</p>
      <button type="button" onClick={() => setProductCount((c) => c + 1)}>
        Tambah Produk
      </button>
    </div>
  )
}

export default DocumentTitleUpdater
```

## 2. Jawaban Pertanyaan Pemahaman
1. Jika diberi `[]`, efek hanya dieksekusi 1 kali setelah render perdana. Jika dihilangkan sama sekali, efek akan dieksekusi terus-menerus setiap kali terjadi re-render komponen apa pun, yang dapat menyebabkan pemborosan daya komputasi atau siklus loop tak berujung.
2. Variabel `ignore` melindungi aplikasi dari kondisi balapan (*race condition*) dan pembaruan state pada komponen yang sudah tidak aktif (*unmounted*). Jika pengguna terburu-buru berpindah halaman sebelum server selesai membalas, fungsi pembersih akan mengubah `ignore = true`, sehingga data yang terlambat datang tidak akan dipaksakan masuk ke state komponen yang sudah tiada.
```

---

Lanjut ke: **02c-fetch-dan-loading-state.md** (Slice 1)
