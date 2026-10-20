# 2.3a Debounce & Optimasi Input Pencarian

> **Bacaan wajib sebelum sesi:** Modul React Programmer Pit — **Bab 2.3** (Component Lifecycle & useEffect — bagian cleanup) & **Bab 3.3** (Performance Optimization).  
> **Prasyarat:** Memahami siklus hidup `useEffect`, dependency array, dan cleanup function dari Bulan 2 (Slice 1).

---

## Kenapa Unit Ini Ada?

Ketika kita membuat kotak pencarian (*search bar*) yang langsung memfilter data saat pengguna mengetik (*live search*), ada masalah besar yang sering diabaikan pemula:

Katakanlah pengguna mengetik kata: **`K e r i p i k`** (7 huruf).
Jika kita memicu pemanggilan API di setiap ketukan tombol (`onChange`):
1. **7 request HTTP terkirim ke server secara bertubi-tubi** dalam waktu kurang dari 2 detik!
2. **Server kelebihan beban (*server thrashing*)** melayani kueri-kueri parsial yang sebenarnya tidak diinginkan pengguna (`"K"`, `"Ke"`, `"Ker"`, dst).
3. **Bahaya *Race Condition*:**
   Request untuk `"Ker"` bisa saja selesai **lebih lambat** daripada request untuk `"Keripik"` (karena latensi jaringan yang fluktuatif). Akibatnya, hasil akhir yang tampil di layar adalah hasil pencarian `"Ker"`, bukan `"Keripik"`!

Solusi standar industri untuk masalah ini adalah teknik **Debounce**.

---

## 1. Konsep Dasar Debounce

**Debounce** adalah teknik menunda eksekusi suatu fungsi sampai pengguna **berhenti melakukan aksi** selama jeda waktu tertentu (*delay*).

```text
Pengguna mengetik:  K ── e ── r ── i ── p ── i ── k ────── (berhenti 400ms) ──► REQUEST API!
                                                     ▲
                                          Timer di-reset di tiap huruf
```

Setiap kali pengguna mengetik huruf baru, timer lama **dibatalkan** dan timer baru dinyalakan. Hanya ketika pengguna benar-benar berhenti mengetik selama (misalnya) 400 milidetik, barulah request pencarian ke server dikirim.

---

## 2. Membuat Custom Hook `useDebouncedValue`

Di React, pola timer dengan pembatalan (*cleanup*) ini diimplementasikan dengan sangat elegan menggunakan `useState` dan `useEffect`.

Buat file `src/hooks/useDebouncedValue.ts`:

```ts
import { useEffect, useState } from 'react'

/**
 * Menunda pembaruan nilai sampai pengguna berhenti mengetik selama `delayMs`.
 * Digunakan agar aplikasi tidak membanjiri API dengan request di setiap ketukan keyboard.
 */
export function useDebouncedValue<T>(value: T, delayMs: number): T {
  const [debouncedValue, setDebouncedValue] = useState<T>(value)

  useEffect(() => {
    // 1. Pasang timer baru setiap kali `value` atau `delayMs` berubah
    const timeoutId = setTimeout(() => {
      setDebouncedValue(value)
    }, delayMs)

    // 2. Fungsi Cleanup: BATALKAN timer lama jika `value` berubah lagi
    //    sebelum durasi `delayMs` tercapai!
    return () => {
      clearTimeout(timeoutId)
    }
  }, [value, delayMs])

  return debouncedValue
}
```

### Bagaimana Hook Ini Bekerja di Balik Layar?
1. Saat user mengetik huruf pertama `"K"`, `useEffect` berjalan dan memasang `setTimeout` untuk 400ms ke depan.
2. Sebelum 400ms habis, user mengetik huruf kedua `"e"`.
3. React menjalankan **cleanup function** dari render sebelumnya (`clearTimeout(timeoutId)`), sehingga timer huruf `"K"` dibatalkan sebelum sempat tereksekusi.
4. React memasang timer baru 400ms untuk `"Ke"`.
5. Proses ini berulang sampai user berhenti mengetik. Barulah `setDebouncedValue` terpanggil!

---

## 3. Arsitektur UX: Dua Tingkat Nilai Pencarian

Agar pengalaman pengguna (*User Experience*) tetap terasa sangat responsif, kita membedakan **dua nilai**:

1. **`urlFilters.q` (Nilai Langsung / Real-time):**
   Nilai ini dihubungkan langsung ke atribut `value` elemen `<input>`. Huruf yang diketik langsung muncul di layar tanpa ada jeda atau lag sedikit pun.
2. **`activeFilters.q` (Nilai Debounce):**
   Nilai hasil olahan `useDebouncedValue(urlFilters.q, 400)`. Nilai inilah yang kita teruskan ke hook API `useProducts`.

```text
┌────────────────────────┐
│     <input value>      │ ◄─── Terhubung ke urlFilters.q (Instan, tidak lag)
└───────────┬────────────┘
            │
            ▼ useDebouncedValue(..., 400)
┌────────────────────────┐
│      activeFilter      │ ◄─── Dikirim ke API (Hanya 1 request setelah jeda 400ms)
└────────────────────────┘
```

Pengguna merasa inputnya sangat cepat (*smooth*), sementara server dan jaringan tetap sangat hemat!

---

## Latihan Mandiri (30 Menit)

1. **Eksperimen Konsol Jeda:**
   Pasang `console.log('Debounce terpicu dengan nilai:', debouncedValue)` di dalam `useEffect`. Ketik sebuah kalimat panjang secara cepat di form, amati di tab Console DevTools bahwa log hanya tercetak satu kali setelah kamu berhenti mengetik.
2. **Uji Performa Latensi:**
   Ubah jeda waktu dari 400ms menjadi 1000ms (1 detik), lalu coba rasakan perbedaannya. Kenapa 300ms - 500ms dianggap sebagai *sweet spot* (titik ideal) untuk debounce pencarian web?

---

## Cek Pemahaman

1. Mengapa fungsi `clearTimeout(timeoutId)` wajib ditaruh di bagian `return` dari `useEffect`?
2. Apa yang akan terjadi jika kita lupa menyertakan cleanup function tersebut?
3. Apa perbedaan konsep antara **Debounce** dan **Throttle**?

---

**Lanjut ke:** `03b-url-search-params-dan-server-query.md` (State di URL & Server-side Query)
