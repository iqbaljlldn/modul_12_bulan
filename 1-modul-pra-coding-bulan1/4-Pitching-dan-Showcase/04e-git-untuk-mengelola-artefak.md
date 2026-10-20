# 04e. Git untuk Mengelola Artefak: Membiasakan Workflow Kolaborasi

**Minggu 4: Pitching & Showcase | Sesi 5 (Jumat)**  
**Target Waktu:** 90 - 120 Menit  
**Output Sesi:** Repositori GitHub Squad Berisi Seluruh Artefak Bulan 1 yang Terorganisir

---

## 1. Mengapa Ini Penting?

Banyak orang mengira Git hanya digunakan untuk menyimpan kode program (seperti JavaScript atau Python). Ini salah kaprah!

Di tim rekayasa modern, **semua aset digital dikelola dengan Version Control (Git)**:
- Spesifikasi produk (*Product Requirement Document*).
- Diagram arsitektur dan flowchart (file Markdown / Mermaid).
- Dokumentasi API dan catatan rapat teknis.

Dengan Git:
1. Tidak ada lagi tragedi file bernama: `pitch-deck-final-v2-revisi-beneran-final-bgt.pdf`.
2. Setiap perubahan tercatat siapa penulisnya, kapan diubah, dan apa alasannya (*commit message*).
3. Yang paling penting: **kamu membiasakan jarimu memakai Git terminal hari ini**, sehingga saat mulai ngoding React di Bulan 2, alur `git add`, `git commit`, `git push`, dan `Pull Request` sudah menjadi memori otot (*muscle memory*).

---

## 2. Siklus Kerja Git Sederhana (3 Area)

```text
┌──────────────────────┐      git add       ┌──────────────────────┐    git commit    ┌──────────────────────┐
│  Working Directory   │ ─────────────────► │     Staging Area     │ ───────────────► │    Commit History    │
│ (File di komputermu) │                    │ (Siap dibungkus)     │                  │ (Tercatat permanen)  │
└──────────────────────┘                    └──────────────────────┘                  └──────────────────────┘
                                                                                                 │
                                                                                                 │ git push
                                                                                                 ▼
                                                                                      ┌──────────────────────┐
                                                                                      │   GitHub (Remote)    │
                                                                                      │ (Bisa diakses tim)   │
                                                                                      └──────────────────────┘
```

---

## 3. Struktur Repositori Artefak Bulan 1

Setiap squad membuat satu repositori bersama di GitHub bernama `katalog-umkm-pra-coding-squad-[X]`.

Struktur folder wajib di dalam repositori:

```text
katalog-umkm-pra-coding/
├── README.md                          # Ringkasan proyek, profil squad, & link slide
├── 1-ai-literacy/
│   ├── piagam-etika.md
│   ├── prompt-cheat-sheet.md
│   └── studi-kasus-umkm.md
├── 2-computational-thinking/
│   ├── dekomposisi-pseudocode.md
│   ├── flowchart-fitur.md
│   └── erd-model-data.md
├── 3-desain-dan-bisnis/
│   ├── ux-review.md
│   ├── wireframe-3-halaman.png
│   ├── value-proposition-canvas.md
│   └── persona-dan-backlog.md
└── 4-pitching/
    ├── user-flow-tervalidasi.md
    ├── catatan-gladi-resik.md
    └── pitch-deck-final.pdf
```

---

## 4. Perintah Terminal Git Esensial Hari Ini

```bash
# 1. Menghubungkan folder lokal ke repositori GitHub tim
git clone https://github.com/organisasi-tribe/katalog-umkm-pra-coding-squad-1.git
cd katalog-umkm-pra-coding-squad-1

# 2. Membuat branch kerja sendiri (jangan langsung ganggu main!)
git checkout -b fitur/tambah-erd-minggu2

# 3. Menambahkan file dokumen baru ke staging
git add 2-computational-thinking/erd-model-data.md

# 4. Menyimpan catatan commit yang jelas dan profesional
git commit -m "docs: menambahkan diagram ERD 4 entitas katalog UMKM"

# 5. Mengirim branch ke GitHub
git push origin fitur/tambah-erd-minggu2
```

Setelah itu, buka halaman GitHub repo tim kalian:
1. Klik tombol **Compare & pull request**.
2. Minta rekan se-squad untuk membaca dan mereview dokumen.
3. Klik **Merge pull request** ke branch `main`.

---

## 5. Workshop Praktik Squad (60 Menit)

1. **Langkah 1 (Setup Repo Bersama - 15 Menit):**  
   Driver squad membuat repo di GitHub dan mengundang 2 anggota lainnya sebagai kolaborator (*Collaborators*).
2. **Langkah 2 (Bagi Tugas Upload - 30 Menit):**  
   - Anggota 1 bertugas membuat branch dan mengunggah artefak Minggu 1 (AI Literacy).
   - Anggota 2 bertugas membuat branch dan mengunggah artefak Minggu 2 (CT & Diagram).
   - Anggota 3 bertugas membuat branch dan mengunggah artefak Minggu 3 & 4 (Desain, Bisnis, Slide).
3. **Langkah 3 (Review & Merge Bersama - 15 Menit):**  
   Setiap anggota wajib mereview dan meng-approve Pull Request rekan setimnya sebelum dimerge ke `main`.
4. **Langkah 4 (Sempurnakan README Utama):**  
   Tulis file `README.md` utama yang memuat ringkasan nama platform, visi, nama anggota tim, dan daftar link ke seluruh artefak di atas.

---

## 6. Output Sesi

Tautan (*URL*) **Repositori GitHub Publik Squad** yang berisi seluruh artefak lengkap dari Minggu 1 sampai Minggu 4, dengan riwayat commit rapi dari ketiga anggota tim.

---

## 7. Cek Pemahaman Diri

1. Mengapa pesan commit yang jelas seperti *"docs: menambahkan wireframe form merchant"* jauh lebih baik daripada *"update"* atau *"tugas"*?
2. Apa gunanya menggunakan *Pull Request (PR)* alih-alih semua orang langsung push ke branch `main` secara bersamaan?

Lanjut ke: **[04f-showcase-pitch-day.md](file:///home/iqbaal/gelombang-3/modul 12 bulan/modul-pra-coding-bulan1/4-Pitching-dan-Showcase/04f-showcase-pitch-day.md)**
