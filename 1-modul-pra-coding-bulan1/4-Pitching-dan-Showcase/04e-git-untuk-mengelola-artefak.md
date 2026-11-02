# 04e. Git untuk Mengelola Artefak: Membiasakan Workflow Kolaborasi

**Minggu 4: Pitching & Showcase | Sesi 5 (Jumat)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Repositori GitHub Squad Berisi Seluruh Artefak & Latihan Kode Bulan 1

---

## 1. Mengapa Ini Penting?

Banyak orang mengira Git hanya digunakan untuk menyimpan kode program. Ini salah kaprah!

Di tim rekayasa modern, **semua aset digital dikelola dengan Version Control (Git)**:
- Spesifikasi produk dan rencana fitur (*Product Backlog*).
- Diagram alur dan arsitektur data (file Markdown & Mermaid).
- Catatan riset wawancara pengguna dan slide presentasi.

Kamu sudah mempelajari dasar-dasar Git pada 2 bulan sebelumnya. Oleh karena itu, hari ini kita tidak mengulang teori perintah dasar dari nol, melainkan langsung mempraktikkan **alur kolaborasi tim profesional**: membuat cabang kerja (*branch*), menulis pesan commit yang informatif, membuat *Pull Request (PR)*, dan saling mereview dokumen sebelum digabungkan ke cabang utama (*main*).

Yang paling penting: hari ini kamu mengunggah **seluruh artefak tim, tugas mandiri, serta latihan kode JS dan HTML/CSS** yang telah kamu buat selama sebulan ini!

---

## 2. Alur Kerja Kolaborasi Git: Branch & Pull Request

```text
       (main branch - cabang utama stabil)
───●────────────────────────────────────────●─── (Hasil Dimerge)
    \                                      ▲
     \ git checkout -b fitur/...          │ Pull Request (Review Tim)
      ▼                                    │
       ●─────────────●─────────────────────●
       (commit 1)    (commit 2: latihan kode)
       (branch kerja milik anggota tim)
```

1. **Jangan bekerja langsung di `main`:** Cabang `main` adalah etalase resmi yang harus selalu bersih dan rapi.
2. **Bekerja di branch masing-masing:** Setiap anggota membuat branch fitur sendiri saat menambahkan artefak atau latihan kode.
3. **Review via Pull Request (PR):** Rekan setim membaca dokumen atau kode yang diunggah, memberikan persetujuan (*Approve*), lalu menggabungkannya (*Merge*) ke `main`.

---

## 3. Struktur Standar Repositori Squad Bulan 1

Setiap squad membuat satu repositori publik bersama di GitHub bernama `katalog-umkm-pra-coding-squad-[X]`.

Susunan folder resmi repositori:

```text
katalog-umkm-pra-coding/
├── README.md                          # Profil proyek, nama anggota squad, link slide
│
├── 1-ai-literacy/
│   ├── piagam-etika.md                # Piagam etika AI squad
│   ├── prompt-cheat-sheet.md          # Format R-C-I-C-O & few-shot
│   └── studi-kasus-umkm-asumsi.md     # Draf solusi UMKM berbasis asumsi
│
├── 2-computational-thinking/
│   ├── dekomposisi-proses.md          # 2 Alur proses bisnis UMKM
│   ├── pseudocode-dan-dryrun.md       # Logika diskon/ongkir & stok
│   ├── flowchart-sistem.md            # Flowchart WA & Tambah Produk
│   ├── erd-model-data.md              # ERD (ItemPesanan & data pembeli)
│   └── latihan-kode-diskon.js         # JEMBATAN KODE: Fungsi JS Minggu 2 (02b)
│
├── 3-desain-dan-bisnis/
│   ├── ux-review.md                   # Laporan review UX aplikasi nyata
│   ├── wireframe-3-halaman.png        # Foto/ekspor wireframe 3 halaman
│   ├── value-proposition-canvas.md    # Peta masalah vs solusi
│   ├── wawancara-umkm-nyata.md        # Catatan wawancara 1 UMKM sekitar
│   ├── persona-dan-prioritas.md       # Persona berbasis wawancara nyata
│   ├── rencana-fitur-backlog.md       # Backlog Slice 0-2 & Acceptance Criteria
│   └── wireframe-statis.html          # JEMBATAN KODE: HTML/CSS Minggu 3 (03b)
│
├── 4-pitching/
│   ├── user-flow-tervalidasi.md       # Diagram alur WhatsApp tervalidasi
│   ├── catatan-gladi-resik.md         # Evaluasi waktu & masukan I Like/Wish
│   └── pitch-deck-final.pdf           # File slide 7 halaman siap tampil
│
└── tugas-mandiri/                     # Folder kumpulan tugas individual
    ├── [nama-murid-1]/                # Berisi tugas_01a.md sampai tugas_04f.md
    ├── [nama-murid-2]/
    └── [nama-murid-3]/
```

---

## 4. Perintah Cepat Alur Branch & Pull Request

```bash
# 1. Pastikan repo lokal terhubung dan update dengan main terbaru
git checkout main
git pull origin main

# 2. Buat branch kerja baru
git checkout -b upload-artefak-[nama-kamu]

# 3. Masukkan file artefak atau latihan kode ke folder yang tepat
# Contoh: menambahkan latihan kode JS dan file tugas mandiri
git add 2-computational-thinking/latihan-kode-diskon.js
git add tugas-mandiri/[nama-kamu]/

# 4. Buat commit dengan pesan yang jelas
git commit -m "feat: menambahkan latihan kode JS fungsi diskon dan folder tugas mandiri"

# 5. Push branch kerja ke GitHub
git push origin upload-artefak-[nama-kamu]
```

Setelah push berhasil:
1. Buka repositori tim di web GitHub.
2. Klik tombol hijau **Compare & pull request**.
3. Tuliskan deskripsi singkat file apa saja yang kamu masukkan.
4. Minta rekan se-squad untuk mereview dan mengklik tombol **Merge pull request**.

---

## 5. Workshop Praktik Squad (60 Menit)

1. **Langkah 1 (Bagi Berkas yang Diunggah - 10 Menit):**
   - Anggota 1: Bertugas mengunggah folder `1-ai-literacy/` dan `2-computational-thinking/` (termasuk file kode `latihan-kode-diskon.js`).
   - Anggota 2: Bertugas mengunggah folder `3-desain-dan-bisnis/` (termasuk file kode `wireframe-statis.html` dan catatan wawancara UMKM nyata).
   - Anggota 3: Bertugas mengunggah folder `4-pitching/` (slide deck PDF dan user flow).
   - Semua anggota: Membuat sub-folder pribadi masing-masing di dalam `tugas-mandiri/` dan memasukkan file tugas individual (`tugas_01a` s/d `tugas_04e`).
2. **Langkah 2 (Eksekusi Branch & PR - 35 Menit):**  
   Setiap anggota wajib membuat branch masing-masing, push ke GitHub, dan membuat Pull Request. Anggota lain bertindak sebagai reviewer sebelum dimerge ke `main`.
3. **Langkah 3 (Sempurnakan README Utama - 15 Menit):**  
   Edit file `README.md` repositori squad agar memuat nama platform, nama 3 anggota, tautan ke slide presentasi, dan ringkasan struktur artefak.

---

## 6. Output Sesi

Tautan (*URL*) **Repositori GitHub Tim** yang sudah terisi lengkap seluruh artefak dari Minggu 1 sampai Minggu 4, commit latihan kode, serta folder tugas mandiri ketiga anggota tim.

---

## 7. Tugas Mandiri (Individual)

- **Sifat:** Individu (dikerjakan sendiri di luar jam kelas)
- **Target Waktu:** 25 menit
- **Nama File:** Simpan di folder pribadimu dalam repo squad dengan nama `tugas_04e.md`

### Instruksi:
1. Pastikan branch kerjamu di GitHub sudah berhasil dimerge ke branch `main`.
2. Buka riwayat commit (*commits history*) repositori tim di browser.
3. Catat di file `tugas_04e.md`:
   - Tautan URL Pull Request (PR) yang kamu buat hari ini.
   - Siapa rekan se-squad yang mereview dan meng-approve PR-mu.
   - Konfirmasi bahwa file latihan kode (`latihan-kode-diskon.js` atau `wireframe-statis.html`) dan folder tugas mandirimu sudah berada di dalam branch `main`.

### Contoh Hasil yang Diharapkan:
```markdown
# Tugas Mandiri 04e — Verifikasi Commit & Pull Request
Nama: [Nama Kamu]
Squad: Squad 3

## 1. Bukti Tautan Pull Request:
- URL PR: https://github.com/tribe-umkm/katalog-umkm-pra-coding-squad-3/pull/2
- Judul PR: "feat: upload artefak desain UX, file html wireframe statis, dan tugas mandiri"
- Di-review dan di-merge oleh: [Nama Rekan Squad]

## 2. Konfirmasi File Kode & Tugas:
- [x] File `wireframe-statis.html` sudah ada di folder `3-desain-dan-bisnis/` di branch main.
- [x] Folder `tugas-mandiri/[nama-saya]/` sudah memuat seluruh tugas harian dari Minggu 1 sampai Minggu 4.
```

---

## 8. Cek Pemahaman Diri

1. Mengapa bekerja di *branch* terpisah jauh lebih aman daripada semua anggota langsung melakukan push bersamaan ke branch *main*?
2. Mengapa artefak desain dan diagram alur penting disimpan di Git bersama dengan kode aplikasi?

---

Lanjut ke: **[04f-showcase-pitch-day.md](04f-showcase-pitch-day.md)**
