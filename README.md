# MISI CILIK: Selamatkan Taman Ceria! 🐝🌸
> **Media Pembelajaran Digital Interaktif Berbasis Web untuk Anak TK Kelompok A/B**  
> Disusun untuk Kategori Karya Media Pembelajaran Digital — **Lomba PORSENI XV IGTKI-PGRI Jawa Timur**

---

## 📌 Ikhtisar Proyek

**MISI CILIK** adalah aplikasi permainan edukasi interaktif berbasis peramban web (*HTML5 Single-Page Application*) dengan pendekatan *Offline-First* dan *Single-File Delivery* (`index.html`). Dirancang khusus untuk karakteristik perkembangan kognitif, motorik, dan bahasa anak usia dini (4–6 tahun) serta memberikan instrumen pembelajaran praktis bagi guru di kelas.

Aplikasi ini mengusung arsitektur **Config-Driven (`GAME_CONFIG`)**, memungkinkan guru/peserta lomba mengganti tema, narasi, dan aset permainan hanya dalam waktu hitungan menit saat menghadapi penentuan tema dadakan di lokasi lomba.

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
    │   ├── game_rules.md                     # Mekanisme gameplay 6 state, input & skoring
    │   └── competition_rules.md              # Kriteria penilaian juri PORSENI & justifikasi AI
    │
    ├── 02_kurikulum/                         # Muatan Edukasi & Pedagogi PAUD
    │   ├── kurikulum_paud.md                 # Penyelarasan Kurikulum Merdeka (CP, TP, 6 Aspek)
    │   └── naskah_alur_cerita.md             # Naskah cerita, dialog TTS & pertanyaan pemantik
    │
    ├── 03_architecture/                      # Desain Perangkat Lunak & Sistem
    │   ├── system_architecture.md            # Diagram alur sistem, state machine & event lifecycle
    │   ├── config_driven_design.md           # Spesifikasi GAME_CONFIG & 4 preset tema dadakan
    │   └── audio_and_hardware.md             # Web Audio API (SFX sintetis), TTS, & WebCam
    │
    ├── 04_development_rules/                 # Standar Rekayasa & Desain
    │   ├── development_guidelines.md         # Aturan single-file, zero build, & offline-first
    │   └── ui_ux_tk_standards.md             # Standar desain antarmuka ramah anak usia 4-6 tahun
    │
    └── archive/                              # Arsip berkas acuan awal
        └── spesifikasi_game_misi_cilik_antigravity_prompt.md
```

---

## 🚀 Panduan Akses Cepat Dokumen

| Kategori | Dokumen | Ringkasan Isi |
| :--- | :--- | :--- |
| **Aturan Game** | [game_rules.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/01_rules/game_rules.md) | Logika interaksi Layar 0 hingga Layar 5, sistem 2-klik, deteksi benar/salah. |
| **Regulasi Lomba** | [competition_rules.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/01_rules/competition_rules.md) | Rubrik penilaian PORSENI, lembar evaluasi juri, dan pemanfaatan AI. |
| **Kurikulum PAUD** | [kurikulum_paud.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/02_kurikulum/kurikulum_paud.md) | Capaian Pembelajaran (CP), Tujuan Pembelajaran (TP), dan 6 Aspek Perkembangan. |
| **Naskah & Narasi** | [naskah_alur_cerita.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/02_kurikulum/naskah_alur_cerita.md) | Dialog maskot *Ara si Lebah*, naskah audio TTS, panduan diskusi guru. |
| **Arsitektur Sistem** | [system_architecture.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/03_architecture/system_architecture.md) | Diagram alur data, komponen UI global, alur transisi state layar. |
| **Config & Tema** | [config_driven_design.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/03_architecture/config_driven_design.md) | Struktur JSON `GAME_CONFIG`, fitur Live Editor & 4 Preset Tema Lomba. |
| **Audio & Hardware** | [audio_and_hardware.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/03_architecture/audio_and_hardware.md) | SFX sintetis prosedural Web Audio API, Web Speech API, & Webcam aksi nyata. |
| **Standar Teknis** | [development_guidelines.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/04_development_rules/development_guidelines.md) | Spesifikasi `index.html` tunggal, Tailwind CDN, Vanilla JS tanpa bundler. |
| **Desain TK UX** | [ui_ux_tk_standards.md](file:///c:/Users/User/Documents/Personal%20Project/Games/docs/04_development_rules/ui_ux_tk_standards.md) | Ukuran target sentuh, warna kontras pastel, keyframe animasi CSS anak. |

---

## 🛠️ Ringkasan Spesifikasi Teknis

* **Bentuk Berkas:** 1 Berkas Mandiri `index.html` (*Single-File Application*).
* **Teknologi Utama:** HTML5, Tailwind CSS (via CDN), Custom CSS Keyframes, Vanilla JavaScript (ES6+).
* **Audio Engine:** Web Audio API (`AudioContext`) untuk SFX prosedural + Web Speech API (`speechSynthesis`) untuk suara narasi Bahasa Indonesia.
* **Periferal:** MediaDevices API (`getUserMedia`) untuk kamera foto bukti aksi nyata (disertai sistem *fallback* aman).
* **Dependencies Eksternal:** **Nol (Zero External Assets Required)** untuk eksekusi offline penuh.
