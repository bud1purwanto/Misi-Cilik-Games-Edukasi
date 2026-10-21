# MISI CILIK: Selamatkan Lingkungan! 🌍🌱
> **Media Pembelajaran Digital Interaktif Berbasis Web untuk Anak TK (Diferensiasi Kelompok A & B)**  
> Disusun untuk Kategori Karya Media Pembelajaran Digital — **Lomba PORSENI XV IGTKI-PGRI Jawa Timur**

---

## 📌 Ikhtisar Proyek

**MISI CILIK: Selamatkan Lingkungan!** adalah aplikasi media pembelajaran digital interaktif berbasis peramban web (*HTML5 Single-Page Application*) dengan filosofi *Offline-First* dan *Single-File Deliverable* (`index.html`). Dirancang khusus untuk karakteristik perkembangan kognitif, motorik, bahasa, dan sosial-emosional anak usia dini (4–6 tahun) sesuai prinsip Kurikulum Merdeka Fase Fondasi.

### ✨ Fitur Unggulan Utama:
1. **Diferensiasi Pembelajaran Fase Fondasi (Kelompok A & B):**
   * `🐥 Kelompok A (Usia 4–5 Tahun)`: Fokus observasi konkret, 4 item sampah terfokus, membilang mandiri 1–5 tanpa bocoran angka, kartu urutan bernomor visual, dan 2 checklist aksi terbimbing.
   * `🦉 Kelompok B (Usia 5–6 Tahun)`: Fokus analisis sebab-akibat, 6 item sampah lengkap dengan alasan ilmiah edukatif, membilang mandiri 1–10, urutan sains mandiri tanpa nomor + narasi sains komprehensif, dan 3 checklist aksi kolaboratif.
2. **Objek Numerasi Spesifik Sesuai Sub-Tema (Bebas Bocoran Angka):**
   * Menghilangkan instruksi yang membocorkan angka target.
   * Objek hitung otomatis berganti dinamis: Bunga Matahari (`🌻`), Bintang Laut (`⭐`), Hewan Safari (`🦁`), atau Peralatan Sekolah (`📚`).
3. **Pemisahan Antarmuka Dual-Mode (Mode Anak vs Mode Guru):**
   * **Mode Anak:** Tampilan permainan bersih, ceria, tombol besar, minim distraksi teks teknis, fokus pada petualangan.
   * **Mode Guru / Juri:** Panel kontrol kokpit lengkap memuat Live Theme Switcher 4 tema, lembar asesmen autentik, dan panduan kurikulum & SOP presentasi.
4. **Asesmen Autentik Berbasis Bukti Pengamatan Guru (*Evidence-Based Assessment*):**
   * Predikat (BB, MB, BSH, BSB) tidak diberikan otomatis buta, melainkan dipilih langsung oleh guru berdasarkan bukti perilaku nyata anak saat berdiskusi, memilah sampah, berhitung mandiri, dan bergotong royong.
5. **Rekapitulasi Portofolio Murid (Local Storage):**
   * Data nama anak, kelompok usia, sub-tema, 5 bintang emas, foto aksi nyata, dan nilai rubrik 6 aspek tersimpan otomatis di memori peramban tanpa memerlukan koneksi internet.
6. **Kemandirian Penuh (*Zero External Dependency*):**
   * Efek suara prosedural Web Audio API murni (tanpa file mp3 eksternal).
   * Narasi suara AI Web Speech API (`id-ID`) ramah anak.
   * Kamera aksi nyata `getUserMedia` dengan *safe fallback* otomatis.

---

## 🗂️ Peta Dokumentasi Proyek

Dokumentasi proyek telah ditata secara modular dalam direktori [`docs/`](file:///c:/Users/User/Documents/Personal%20Project/Games/docs) dengan pembagian kategori berikut:

```
c:\Users\User\Documents\Personal Project\Games\
│
├── README.md                                 # Panduan umum & navigasi proyek
├── AGENTS.md                                 # Aturan global wajib bagi setiap AI Agent / Developer
│
└── docs/
    ├── 01_rules/                             # Aturan Permainan & Regulasi Lomba
    │   ├── game_rules.md                     # Mekanisme gameplay 6 state, diferensiasi A/B & skoring
    │   └── competition_rules.md              # Kriteria penilaian juri PORSENI, diferensiasi & SOP 5 menit
    │
    ├── 02_kurikulum/                         # Muatan Edukasi & Pedagogi PAUD
    │   ├── kurikulum_paud.md                 # CP, TP Terukur, Diferensiasi A & B, dan Rubrik Berbasis Bukti
    │   └── naskah_alur_cerita.md             # Naskah cerita, dialog TTS, panduan diskusi A/B & 4 sub-tema
    │
    ├── 03_architecture/                      # Desain Perangkat Lunak & Sistem
    │   ├── system_architecture.md            # Mesin status, Dual-Mode UX, local storage, & event lifecycle
    │   ├── config_driven_design.md           # Spesifikasi objek GAME_CONFIG, 4 sub-tema & Live Switcher
    │   └── audio_and_hardware.md             # Web Audio API sintetis, Web Speech TTS, & Webcam
    │
    ├── 04_development_rules/                 # Standar Rekayasa & Desain
    │   ├── development_guidelines.md         # Aturan berkas tunggal index.html, zero-build, & offline-first
    │   └── ui_ux_tk_standards.md             # Ergonomi ramah anak TK, sistem 2-klik, Dual-Mode, & animasi CSS
    │
    └── archive/                              # Arsip berkas acuan awal
        └── spesifikasi_game_misi_cilik_antigravity_prompt.md
```

---

## 🚀 Panduan Akses Cepat Dokumen

| Kategori | Dokumen | Ringkasan Isi |
| :--- | :--- | :--- |
| **Aturan Game** | [game_rules.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/01_rules/game_rules.md) | Logika interaksi Layar 0 hingga 5, diferensiasi A/B, sistem 2-klik, perolehan 5 bintang. |
| **Regulasi Lomba** | [competition_rules.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/01_rules/competition_rules.md) | Rubrik penilaian PORSENI, justifikasi 3 pilar AI, SOP presentasi juri 5 menit & checklist pra-lomba. |
| **Kurikulum PAUD** | [kurikulum_paud.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/02_kurikulum/kurikulum_paud.md) | CP, TP Terukur, Diferensiasi Kelompok A & B, serta matriks rubrik asesmen berbasis bukti observasi. |
| **Naskah & Narasi** | [naskah_alur_cerita.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/02_kurikulum/naskah_alur_cerita.md) | Dialog maskot, transkrip TTS Bahasa Indonesia, numerasi tanpa bocoran angka, & naskah 4 sub-tema. |
| **Arsitektur Sistem** | [system_architecture.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/03_architecture/system_architecture.md) | Diagram komponen, Dual-Mode UX, finite state machine, struktur penyimpanan Local Storage murid. |
| **Config & Sub-Tema** | [config_driven_design.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/03_architecture/config_driven_design.md) | Skema objek `GAME_CONFIG`, hierarki judul dinamis, diferensiasi item sampah, dan 4 preset sub-tema. |
| **Audio & Hardware** | [audio_and_hardware.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/03_architecture/audio_and_hardware.md) | Sintesis audio SFX prosedural Web Audio, Web Speech API, & Webcam cermin aksi. |
| **Standar Teknis** | [development_guidelines.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/04_development_rules/development_guidelines.md) | Spesifikasi `index.html` tunggal, zero build step, no placeholder policy. |
| **Desain TK UX** | [ui_ux_tk_standards.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/04_development_rules/ui_ux_tk_standards.md) | Target sentuh $\ge 72\text{px}$, sistem 2-klik proyektor, Dual-Mode antarmuka, animasi keyframe CSS. |

---

## 🛠️ Ringkasan Spesifikasi Teknis

* **Bentuk Berkas:** 1 Berkas Mandiri `index.html` (*Single-File Application*).
* **Teknologi Utama:** HTML5, Tailwind CSS (via CDN), Custom CSS Keyframes, Vanilla JavaScript (ES6+).
* **Audio Engine:** Web Audio API (`AudioContext`) untuk SFX prosedural + Web Speech API (`speechSynthesis`) untuk suara narasi Bahasa Indonesia.
* **Periferal:** MediaDevices API (`getUserMedia`) untuk kamera bukti aksi nyata (dengan izin pengguna & safe fallback).
* **Penyimpanan:** Web Storage API (`localStorage`) untuk pencatatan portofolio hasil belajar murid.
* **Dependencies Eksternal:** **Nol (Zero External Assets Required)** untuk eksekusi offline penuh.
