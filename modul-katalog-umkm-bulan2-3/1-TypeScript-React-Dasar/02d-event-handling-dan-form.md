# 2.0d Event Handling & Form — Interaksi Pengguna di React

## Tujuan Sesi Ini

Memahami cara menangani interaksi pengguna (mengetik, mengklik, mengirim formulir) di React, menguasai pola **Controlled Component** (formulir terkontrol), dan menerapkan teknik satu fungsi pengelola (*handler*) untuk menangani banyak kolom input formulir sekaligus.

---

## Aktivitas Terbimbing di Kelas (Blok 1, 10-15 Menit)

Mentor akan memandu demonstrasi singkat:
- Perbedaan penanganan event HTML klasik (`onclick="fn()"`) dengan React SyntheticEvent (`onClick={fn}`).
- Mengapa `event.preventDefault()` wajib dipanggil pada event `onSubmit`.
- Cara kerja *Controlled Component*: nilai input diatur sepenuhnya oleh state React melalui atribut `value` dan event `onChange`.
- Menggunakan computed property name JavaScript `[name]: value` untuk menghemat kode handler formulir.

*(Bahan bacaan pendalaman opsional: Modul React Bootcamp Bab 2.1 tentang Event Handling dan Forms).*

---

## Ringkasan Konsep Kunci & Analogi

### 1. Apa itu Controlled Component?

> **Analogi Sehari-hari:**  
> - **Input HTML Biasa (Uncontrolled):** Seperti mobil dengan mode autopilot sendiri. Pengguna mengetik huruf, dan elemen DOM menyimpannya sendiri di memorinya tanpa memberi tahu siapa pun. Komponen React tidak tahu apa isi teksnya sampai form disubmit.  
> - **Formulir Terkontrol (Controlled):** Seperti **setir kemudi di tangan sopir handal**. Setiap kali jari pengguna menekan tuts keyboard (event `onChange`), React membaca huruf tersebut, menyimpannya di memori state, lalu React yang menuliskan kembali huruf tersebut ke dalam kotak teks (`value={state}`). React memegang kendali mutlak atas apa yang boleh dan tidak boleh tampil di layar!

### 2. Mengapa Butuh `event.preventDefault()`?

> **Analogi Rem Tangan:**  
> Sejak era awal web tahun 1990-an, perilaku bawaan formulir HTML saat tombol kirim (*submit*) ditekan adalah: mengumpulkan data, mengirimkan ke server, dan **memuat ulang (*reload*) seluruh halaman web dari nol**.  
> Di aplikasi SPA modern, kita tidak ingin halaman berkedip putih atau mereload ulang! Memanggil `event.preventDefault()` ibarat **menarik tuas rem tangan**: kita menghentikan kebiasaan kuno browser dan mengambil alih pengiriman data lewat JavaScript asinkron.

### 3. Trik Sakti: Satu Handler untuk Seluruh Input

Jika sebuah formulir memiliki 6 kolom input, kita tidak perlu membuat 6 fungsi `handleChangeName`, `handleChangePrice`, dll.  
Kita cukup memanfaatkan atribut `name` pada elemen input dan fitur *computed property name* JavaScript `[name]: value`:

```tsx
function handleChange(event: ChangeEvent<HTMLInputElement | HTMLTextAreaElement>) {
  const { name, value } = event.target
  // Memperbarui properti objek state yang namanya cocok dengan atribut name input
  setValues((current) => ({ ...current, [name]: value }))
}
```

---

## Latihan Interaktif: Form Input Produk Sederhana

Perhatikan komponen di bawah. Lengkapi bagian `// TODO:` agar formulir dapat mencatat input pengguna dan menampilkannya secara langsung:

```tsx
// src/components/SimpleFormPreview.tsx
import { useState } from 'react'
import type { ChangeEvent, FormEvent } from 'react'

interface SimpleFormValues {
  productName: string
  merchantName: string
}

function SimpleFormPreview() {
  const [formValues, setFormValues] = useState<SimpleFormValues>({
    productName: '',
    merchantName: '',
  })

  function handleChange(event: ChangeEvent<HTMLInputElement>) {
    const { name, value } = event.target
    // TODO 1: Perbarui state formValues secara aman menggunakan spread operator
    setFormValues((prev) => ({ ...prev, [name]: value }))
  }

  function handleSubmit(event: FormEvent<HTMLFormElement>) {
    // TODO 2: Hentikan perilaku bawaan reload halaman browser
    event.preventDefault()
    alert(`Data terkirim: ${formValues.productName} dari ${formValues.merchantName}`)
  }

  return (
    <div className="preview-container">
      <form onSubmit={handleSubmit}>
        <div>
          <label htmlFor="productName">Nama Barang:</label>
          <input
            id="productName"
            name="productName"
            value={formValues.productName}
            onChange={handleChange}
            placeholder="Contoh: Madu Hutan"
            required
          />
        </div>

        <div>
          <label htmlFor="merchantName">Nama UMKM:</label>
          <input
            id="merchantName"
            name="merchantName"
            value={formValues.merchantName}
            onChange={handleChange}
            placeholder="Contoh: Berkah Tani"
            required
          />
        </div>

        <button type="submit">Kirim Data</button>
      </form>

      {/* Pratinjau langsung isi formulir */}
      <div className="live-preview" style={{ marginTop: '16px', background: '#f7fafc', padding: '12px' }}>
        <h4>Pratinjau Nyata:</h4>
        <p>Produk: {formValues.productName || '(belum diisi)'}</p>
        <p>Penjual: {formValues.merchantName || '(belum diisi)'}</p>
      </div>
    </div>
  )
}

export default SimpleFormPreview
```

---

## Analisis Bug & Prediksi (Aktivitas Blok 2)

Diskusikan bersama rekan pairing:

1. **Temukan Bug:**  
   Seorang rekan mengetik kode input berikut:
   ```tsx
   <input value={name} />
   ```
   Saat ia mencoba mengetikkan huruf apa pun di keyboard laptopnya di dalam kotak input tersebut, hurufnya **sama sekali tidak mau bertambah atau berubah**. Jelaskan mengapa hal itu terjadi!
2. **Prediksi Dampak Lupa Rem Tangan:**  
   Jika baris `event.preventDefault()` di fungsi `handleSubmit` dihapus, apa yang terjadi pada URL browser dan apa yang terjadi pada state aplikasi saat tombol submit diklik?

---

## Tugas Mandiri (Blok 3, Estimasi 20-30 Menit)

Kerjakan secara mandiri di kelas. Simpan hasilnya di:  
`tugas/squad-<nomor>/<nama-kamu>/tugas_02d.md`

### Instruksi Pengerjaan

1. Buat berkas baru sesuai path di atas.
2. Tuliskan identitas diri (Nama, Squad, Tanggal).
3. Buat sebuah rancangan komponen form umpan balik pelanggan bernama `CustomerFeedbackForm.tsx`:
   - State formulir memiliki 2 kolom: `customerName` (string) dan `rating` (string berisi pilihan nilai "5", "4", "3", "2", "1").
   - Gunakan satu fungsi `handleChange` untuk menangani perubahan pada `<input type="text">` dan `<select>`.
   - Tangani submit formulir dengan `event.preventDefault()` dan tampilkan teks terima kasih di bawah formulir setelah submit berhasil.
   - Tuliskan kode lengkap komponen tersebut di dalam dokumen tugas.
4. Jawab 2 pertanyaan pemahaman:
   - Apa yang dimaksud dengan istilah *Controlled Component* di React? Sebutkan dua atribut penting yang membuat sebuah input menjadi controlled!
   - Jelaskan bagaimana sintaks `[name]: value` pada JavaScript mempermudah kita saat membuat form dengan puluhan kolom input!
5. Ajukan Pull Request ke repositori squad.

### Contoh Format Hasil (`tugas_02d.md`)

```markdown
# Tugas Mandiri 02d — Event Handling & Form
Nama: Anisa Rahma
Squad: Squad 3
Tanggal: 12 November 2026

## 1. Kode Komponen CustomerFeedbackForm
```tsx
import { useState } from 'react'
import type { ChangeEvent, FormEvent } from 'react'

interface FeedbackValues {
  customerName: string
  rating: string
}

function CustomerFeedbackForm() {
  const [values, setValues] = useState<FeedbackValues>({
    customerName: '',
    rating: '5',
  })
  const [submittedMessage, setSubmittedMessage] = useState<string | null>(null)

  function handleChange(event: ChangeEvent<HTMLInputElement | HTMLSelectElement>) {
    const { name, value } = event.target
    setValues((prev) => ({ ...prev, [name]: value }))
  }

  function handleSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault()
    setSubmittedMessage(`Terima kasih atas ulasan bintang ${values.rating} dari ${values.customerName}!`)
    setValues({ customerName: '', rating: '5' })
  }

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <label>
          Nama Pelanggan:
          <input
            name="customerName"
            value={values.customerName}
            onChange={handleChange}
            required
          />
        </label>

        <label>
          Rating Kepuasan:
          <select name="rating" value={values.rating} onChange={handleChange}>
            <option value="5">Bintang 5 - Sangat Puas</option>
            <option value="4">Bintang 4 - Puas</option>
            <option value="3">Bintang 3 - Cukup</option>
          </select>
        </label>

        <button type="submit">Kirim Ulasan</button>
      </form>

      {submittedMessage && <p role="status">{submittedMessage}</p>}
    </div>
  )
}

export default CustomerFeedbackForm
```

## 2. Jawaban Pertanyaan Pemahaman
1. *Controlled Component* adalah elemen formulir HTML yang nilainya dikendalikan dan disimpan langsung di dalam state React, bukan dibiarkan dikelola sendiri oleh memori DOM browser. Dua atribut kunci penentunya adalah `value` (yang disambungkan ke variabel state) dan `onChange` (yang memanggil fungsi setter state saat ada input baru).
2. Sintaks `[name]: value` memanfaatkan fitur *computed property name*. Dengan memberikan atribut `name` pada tiap elemen input yang nilainya sama persis dengan nama properti di objek state, kita cukup menulis satu fungsi `handleChange` universal untuk menangani semua input berapapun jumlahnya.
```

---

Lanjut ke: **02e-form-tambah-produk.md** (Slice 2)
