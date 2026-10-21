# AGENTS.MD — Panduan & Aturan Global AI Agent / Developer
> **Proyek:** MISI CILIK: Selamatkan Lingkungan! (Sub-Tema: Taman Ceria, Pantai & Laut, Kebun Binatang, Kelasku)  
> **Target:** Media Pembelajaran Digital Interaktif Anak TK (Lomba PORSENI XV IGTKI-PGRI Jatim)  
> **Status:** Wajib Dibaca & Dipatuhi oleh Setiap AI Agent / Developer Sebelum Menulis Kode

---

## 🚨 MANDAT UTAMA (MANDATORY INSTRUCTION)

Setiap AI Agent atau pengembang yang bekerja pada repositori ini **WAJIB MEMBACA DAN MEMATUHI** seluruh dokumen dalam direktori [`docs/`](file:///c:/Users/User/Documents/Personal%20Project/Games/docs) sebelum melakukan modifikasi, penambahan fitur, atau refaktorisasi kode.

Seluruh keputusan arsitektur, pemilihan aset, mekanisme interaksi, dan struktur kode **TIDAK BOLEH MENYIMPANG** dari dokumen-dokumen yang telah disepakati.

---

## 🗺️ Peta Wajib Baca (Documentation Reading Protocol)

Sebelum menyentuh berkas implementasi (`index.html`), agen wajib memahami modul-modul berikut:

| Urutan | Modul Dokumen | Fokus yang Wajib Dipahami |
| :---: | :--- | :--- |
| **1** | [docs/04_development_rules/development_guidelines.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/04_development_rules/development_guidelines.md) | **Standar Rekayasa:** Wajib 1 file `index.html`, zero-build step, offline-first, zero-placeholder. |
| **2** | [docs/04_development_rules/ui_ux_tk_standards.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/04_development_rules/ui_ux_tk_standards.md) | **Standar Desain TK:** Ukuran tombol $\ge 72\text{px}$, `rounded-3xl`, dual-input 2-klik, warna pastel, dan arsitektur Dual-Mode (Mode Anak vs Mode Guru). |
| **3** | [docs/03_architecture/config_driven_design.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/03_architecture/config_driven_design.md) | **Arsitektur Data:** Objek `GAME_CONFIG` sebagai *Single Source of Truth*, diferensiasi item sampah (4 item vs 6 item), objek numerasi 4 tema, & 4 Preset Tema Dadakan. |
| **4** | [docs/03_architecture/system_architecture.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/03_architecture/system_architecture.md) | **Mesin Status:** Alur 6 State Layar (State 0 hingga State 5), Dual-Mode UI, dan sistem asesmen autentik berbasis bukti pengamatan. |
| **5** | [docs/03_architecture/audio_and_hardware.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/03_architecture/audio_and_hardware.md) | **Audio & Kamera:** Web Audio API prosedural (tanpa file mp3 eksternal), Web Speech API (`id-ID`), & izin pengguna eksplisit webcam dengan fallback aman. |
| **6** | [docs/01_rules/game_rules.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/01_rules/game_rules.md) | **Aturan Main:** Logika gameplay tiap tahap, pemilahan sampah A vs B, numerasi bebas bocoran angka, & perolehan 5 Bintang. |
| **7** | [docs/01_rules/competition_rules.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/01_rules/competition_rules.md) | **Kriteria Lomba:** Rubrik penilaian juri PORSENI IGTKI, justifikasi 3 pilar AI, SOP presentasi 5 menit Mbak Ratih, & checklist uji pra-lomba. |
| **8** | [docs/02_kurikulum/kurikulum_paud.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/02_kurikulum/kurikulum_paud.md) & [naskah_alur_cerita.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/02_kurikulum/naskah_alur_cerita.md) | **Muatan Pedagogis:** CP, TP Terukur, 6 aspek perkembangan, asesmen berbasis bukti pengamatan (BB, MB, BSH, BSB), & naskah dialog TTS bebas bocoran angka. |

---

## ⚡ 7 ATURAN EMAS PENGEMBANGAN (7 GOLDEN RULES)

1. **Aturan Berkas Tunggal (`Single-File Deliverable`):**
   * Seluruh kode HTML5, CSS kustom, dan Vanilla JavaScript harus berada di satu berkas `index.html`.
   * Jangan memecah kode menjadi file `.js` atau `.css` terpisah yang membutuhkan server web lokal atau bundler.
2. **Kemandirian Penuh (*Offline-First & Zero External Assets*):**
   * Suara SFX (Ting, Buzzer, Pop, Fanfare, Tepuk Tangan) **WAJIB** dihasilkan lewat sintesis matematika Web Audio API (`AudioContext`). Dilarang keras menautkan link audio eksternal yang bisa gagal dimuat saat offline.
   * Ikon dan karakter wajib menggunakan Unicode Emoji atau SVG inline, bukan gambar eksternal yang rentan `404 Not Found`.
3. **Pemisahan Logika & Konten (*Config-Driven*):**
   * Jangan melakukan *hardcode* teks cerita, pertanyaan kuis, atau daftar sampah di dalam markup HTML atau fungsi JavaScript.
   * Seluruh data tampilan harus dibaca dari objek `GAME_CONFIG`.
4. **Kesiapan 4 Preset Tema Dadakan:**
   * Aplikasi wajib menyertakan 4 preset tema lengkap (Taman Ceria, Pantai & Laut Bersih, Kebun Binatang Ceria, Kelasku Bersih & Rapi) yang dapat diaktifkan dalam 1 kali klik melalui tombol `"📋 Panel Juri & Editor Tema"`.
5. **Ergonomi Ramah Anak TK (Usia 4–6 Tahun):**
   * Wajib menyediakan sistem interaksi **2-Klik (Click-to-Select, Click-to-Drop)** untuk memilah sampah selain drag-and-drop standar, agar nyaman digunakan pada proyektor sentuh.
   * Tombol besar (`rounded-3xl`), font ramah anak, dan animasi CSS keyframes lembut (`float`, `wiggle`, `shake`, `pulse`).
6. **Kebijakan Penguatan Positif (*Zero Punishment*):**
   * Tidak boleh ada layar *Game Over* atau suara yang menakutkan anak.
   * Jawaban salah direspons dengan getaran lembut dan kalimat penyemangat untuk mencoba kembali.
7. **Standar Kode Anti-Placeholder:**
   * Dilarang menghasilkan kode yang terpotong (*truncated code*), fungsi kosong bertanda `// TODO`, atau mengasumsikan kode lama tetap ada tanpa menulisnya secara lengkap.

---

## 🔍 Checklist Verifikasi Sebelum Menyelesaikan Tugas

Sebelum agen menyatakan tugas selesai, periksa hal-hal berikut:
- [ ] Apakah berkas `index.html` dapat dibuka langsung via *double-click* browser tanpa web server?
- [ ] Apakah selektor Kelompok A & Kelompok B berfungsi dan mendiferensiasi materi di seluruh 5 tahap?
- [ ] Apakah pilah sampah di Tahap 2 membedakan 4 item konkret (Kelompok A) vs 6 item ilmiah berargumen (Kelompok B)?
- [ ] Apakah objek numerasi di Tahap 3A sesuai tema (Pantai: bintang laut, Zoo: hewan, Kelas: peralatan sekolah, Taman: bunga matahari)?
- [ ] Apakah narasi instruksi numerasi bebas dari bocoran angka target sehingga anak menghitung mandiri?
- [ ] Apakah lembar asesmen guru di Tahap 5 memungkinkan pemilihan manual predikat BB, MB, BSH, BSB berbasis bukti observasi?
- [ ] Apakah antarmuka memisahkan Mode Anak (bersih & ceria) dari panel teknis guru/juri?
- [ ] Apakah suara SFX berbunyi tanpa membutuhkan koneksi internet?
- [ ] Apakah narasi Web Speech TTS Bahasa Indonesia berjalan lancar?
- [ ] Apakah sistem 2-klik pilah sampah berfungsi dengan umpan balik visual dan audio ramah anak?
- [ ] Apakah kamera webcam hanya aktif dengan izin pengguna dan memiliki fallback otomatis jika izin ditolak?
- [ ] Apakah tombol ubah sub-tema dapat mengganti seluruh konten secara instan?
- [ ] Apakah sertifikat kelulusan menampilkan badge kelompok, 5 bintang emas, dan rubrik evaluasi siap cetak?
- [ ] Apakah data rekapitulasi murid tersimpan di Local Storage dan dapat dikelola di Panel Juri?
