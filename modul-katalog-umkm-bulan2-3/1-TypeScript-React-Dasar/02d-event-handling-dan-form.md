# 2.0d Event Handling & Form — Interaksi User di React

## Tujuan sesi ini

Paham cara menangani **interaksi user** (klik, ketik, submit) di React, dan menerapkan pola **controlled component** untuk form — persiapan sebelum membuat form tambah produk di Slice 2.

## Bacaan wajib sebelum sesi

**Bab 2.1 — Event Handling dan Forms** (modul React): SyntheticEvent, controlled components, form handling, multiple inputs, validasi sederhana.

## Ringkasan konsep (dari bab 2.1)

### Event Handling di React

Event di React mirip HTML, tapi ada perbedaan:

```tsx
// HTML biasa
<button onclick="handleClick()">Klik</button>

// React — camelCase, fungsi langsung (bukan string)
<button onClick={handleClick}>Klik</button>
```

Beberapa event yang sering dipakai:

| Event | Kapan dipicu |
|---|---|
| `onClick` | Elemen diklik |
| `onChange` | Nilai input berubah |
| `onSubmit` | Form di-submit |
| `onFocus` / `onBlur` | Input dapat/kehilangan fokus |
| `onMouseEnter` / `onMouseLeave` | Mouse masuk/keluar elemen |

### SyntheticEvent

React membungkus event browser asli dengan **SyntheticEvent** supaya konsisten di semua browser. Untuk TypeScript, kita bisa memberi tipe spesifik:

```tsx
import type { ChangeEvent, FormEvent } from 'react'

function handleChange(event: ChangeEvent<HTMLInputElement>) {
  console.log(event.target.value)
}

function handleSubmit(event: FormEvent<HTMLFormElement>) {
  event.preventDefault()  // Mencegah reload halaman
  // ...proses data
}
```

### Controlled Component — Form yang Dijinakkan

Di HTML biasa, `<input>` menyimpan nilainya sendiri. Di React, kita **mengambil alih** dengan menyimpan nilai di state:

```tsx
function NameInput() {
  const [name, setName] = useState('')

  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
    />
  )
}
```

Ini disebut **controlled component** — React yang jadi "sumber kebenaran" untuk nilai input, bukan DOM.

### Satu Handler untuk Banyak Input

Kalau form punya banyak field, buat satu handler yang memanfaatkan `name` attribute:

```tsx
interface FormValues {
  name: string
  email: string
}

function MyForm() {
  const [values, setValues] = useState<FormValues>({ name: '', email: '' })

  function handleChange(event: ChangeEvent<HTMLInputElement>) {
    const { name, value } = event.target
    setValues((current) => ({ ...current, [name]: value }))
  }

  return (
    <form>
      <input name="name" value={values.name} onChange={handleChange} />
      <input name="email" value={values.email} onChange={handleChange} />
    </form>
  )
}
```

**Trik `[name]: value`** = computed property name di JavaScript. `name` berasal dari atribut `name` di `<input>`, jadi satu fungsi `handleChange` bisa mengurus semua input sekaligus.

### preventDefault — Kenapa Wajib di Form?

```tsx
function handleSubmit(event: FormEvent<HTMLFormElement>) {
  event.preventDefault()  // ← WAJIB
  // Tanpa ini, browser akan reload halaman (perilaku bawaan HTML form)
}
```

## Latihan (sebelum masuk Slice 2)

1. **Input + Preview:** buat komponen dengan satu `<input>` untuk nama. Di bawahnya, tampilkan "Halo, {nama}!" yang berubah langsung saat mengetik.

2. **Multi-input form:** buat form dengan 3 field (nama, harga, deskripsi) menggunakan pola satu `handleChange`. Tampilkan preview hasilnya di bawah form (belum perlu submit ke mana-mana).

3. **Submit handler:** tambahkan tombol "Simpan" dan `onSubmit` handler yang `console.log` isi form saat submit. Pastikan halaman **tidak reload**.

4. **Disable saat submit:** buat tombol "Simpan" disabled selama 2 detik setelah klik (simulasi menunggu server). Pakai `setTimeout` di handler.

## Cek pemahaman

- Apa yang dimaksud "controlled component"? Kenapa lebih baik dari membiarkan DOM menyimpan nilai sendiri?
- Kenapa `event.preventDefault()` penting di form React?
- Bagaimana cara menangani beberapa `<input>` dengan satu fungsi `handleChange`?

## Kesalahan umum

| Gejala | Sebab | Solusi |
|---|---|---|
| Ketik di input tapi tidak berubah | `onChange` tidak diisi, atau `value` tidak terhubung ke state | Pastikan `value={state}` dan `onChange` memanggil setter |
| Ketik di satu input, semua input berubah | Atribut `name` di input tidak diisi atau salah | Pastikan `name` cocok dengan key di state object |
| Halaman reload saat submit | Lupa `event.preventDefault()` | Tambahkan di awal `handleSubmit` |

## Kaitkan ke rujukan

**Bab 2.1** modul React membahas event handling lebih lengkap, termasuk controlled vs uncontrolled components dan validasi input sederhana.

---

Lanjut ke: **02e-form-tambah-produk.md** (Slice 2)
