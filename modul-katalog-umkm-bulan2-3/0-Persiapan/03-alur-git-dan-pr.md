# 0.3 Alur Git & Pull Request

Kamu sudah tahu Git dasar dari pre-class (commit, push). Di sini kita tambahkan alur kerja tim: **branch → Pull Request (PR) → review → merge**.

## Kenapa tidak langsung push ke `main`

`main` adalah kode yang harus selalu bisa jalan. Kalau semua orang push langsung ke `main`, kode gampang rusak dan sulit tahu siapa mengubah apa. Solusinya: kerja di **branch sendiri**, baru digabung ke `main` lewat PR setelah direview.

## Alur lengkap

```text
1. git checkout -b feat/nama-slice     (buat branch baru)
2. ...ngoding...
3. git add . && git commit -m "..."    (commit kecil, sering)
4. git push -u origin feat/nama-slice  (push branch)
5. Buka Pull Request di GitHub/GitLab ke `main`
6. Minta 1 orang review (pasangan/squad lain)
7. Kalau ada komentar → revisi → commit lagi → push (PR otomatis update)
8. Setelah di-approve → KAMU sendiri yang merge
```

## Penamaan branch

```text
feat/nama-fitur     → contoh: feat/slice-0-katalog-tampil
fix/nama-bug        → contoh: fix/harga-negatif
docs/nama-dokumen   → contoh: docs/readme-cara-jalan
```

## Isi Pull Request

Starter sudah punya template otomatis, isi jujur:

```text
Apa yang dibuat?
Cara mencobanya?
Bagian mana yang masih bikin bingung / minta perhatian reviewer?
```

Pertanyaan ketiga **bukan tanda kamu gagal** — justru bagian paling penting. Reviewer bisa fokus ke situ, dan itu bahan belajar buat kamu berdua.

## Cara review yang baik (checklist singkat)

Saat jadi reviewer, cek:
- [ ] Kode bisa dijalankan sesuai "Cara mencobanya" di PR
- [ ] `npm run build` dan `npm run lint` lolos (biasanya sudah otomatis, tapi cek juga manual)
- [ ] Nama variabel/fungsi jelas
- [ ] Ada penanganan untuk kondisi kosong/error kalau slice-nya menyangkut data

Komentar review ditulis **spesifik dan sopan**. Bandingkan:

- ❌ "Kodenya jelek."
- ✅ "Bagian `handleSubmit` ini bisa dipecah jadi fungsi kecil biar lebih mudah dibaca — mau coba?"

## PR kecil itu wajib, bukan saran

Target: reviewer bisa membaca PR-mu dalam **±15 menit**. Kalau satu PR berisi seluruh Slice 0-2 sekaligus, itu terlalu besar — pecah jadi beberapa PR.

## Kalau ada conflict

Conflict artinya ada perubahan yang bertumpuk di baris yang sama. Ini normal di kerja tim, bukan tanda kamu salah. Selesaikan **di branch-mu sendiri** (`git pull origin main` lalu selesaikan conflict) sebelum minta review lagi. Kalau bingung, ini alasan bagus untuk pairing.

## Cek pemahaman

- Kenapa yang merge adalah pembuat PR sendiri, bukan reviewer?
- Apa yang terjadi kalau kamu push commit baru ke branch yang PR-nya sudah dibuka?

Lanjut ke: **04-format-minta-bantuan.md**
