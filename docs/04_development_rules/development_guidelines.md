# Pedoman & Standar Rekayasa Kode (Development Guidelines)
> **MISI CILIK: Selamatkan Taman Ceria!**  
> Standar penulisan kode, kemandirian berkas, zero-build policy, dan prinsip *offline-first*.

---

## 1. Prinsip Utama Rekayasa (Core Engineering Principles)

```
┌────────────────────────────────────────────────────────┐
│  PRINSIP #1: SINGLE-FILE DELIVERY (1 index.html)       │
│  PRINSIP #2: ZERO EXTERNAL BUILD STEP (No Node / Vite) │
│  PRINSIP #3: OFFLINE-FIRST BY DEFAULT                  │
│  PRINSIP #4: ZERO PLACEHOLDER / COMPLETE CODE ONLY     │
└────────────────────────────────────────────────────────┘
```

1. **Kemandirian Berkas Tunggal (`Single-File index.html`):**
   * Seluruh struktur markup HTML5, styling CSS kustom + Tailwind CSS, serta logika Vanilla JavaScript wajib terangkum utuh dalam satu berkas `index.html`.
   * Guru maupun juri cukup melakukan *double-click* berkas `index.html` pada peramban apa pun (Chrome, Edge, Firefox) untuk langsung menjalankannya.
2. **Tanpa Ketergantungan Kompilasi (*Zero Build Step*):**
   * Tidak boleh menggunakan bundler (Webpack, Vite, Rollup, Parcel) atau manajer paket (npm/yarn/pnpm).
   * Kode harus siap dieksekusi secara langsung oleh engine browser (*standard ES6+ Vanilla JS*).
3. **Kemandirian Aset (*Zero Dependency Failure*):**
   * Tidak diperbolehkan mengandalkan berkas media eksternal (misal: `assets/audio/ting.mp3` atau `assets/img/bee.png`) sebagai ketergantungan wajib.
   * Ikon dan karakter menggunakan SVG terintegrasi (*inline SVG*) dan representasi emoji Unicode modern.
   * Efek audio dihasilkan oleh Web Audio API terprogram (*procedural synthesis*).
4. **Anti-Placeholder (*No Truncated / Stub Code*):**
   * Seluruh fungsi harus diimplementasikan secara tuntas. Tidak boleh ada komentar penunda kerja seperti `// TODO: tambahkan tahap selanjutnya nanti` atau blok yang dipotong `... (kode lainnya sama) ...`.

---

## 2. Standar Struktur Berkas `index.html`

Berkas `index.html` ditata dalam urutan baku berikut:

```html
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>MISI CILIK: Selamatkan Taman Ceria!</title>
  
  <!-- 1. Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  
  <!-- 2. Custom CSS & Keyframe Animations -->
  <style>
    /* Keyframes: bounce-slow, float, wiggle, pulse-glow, confetti */
  </style>
</head>
<body class="bg-gradient-to-b from-sky-200 via-emerald-100 to-amber-100 font-sans select-none overflow-x-hidden">

  <!-- 3. Header Global (Sticky Top) -->
  <header id="global-header"> ... </header>

  <!-- 4. Kontainer Utama Layar Permainan (State 0 s/d 5) -->
  <main id="app-container">
    <section id="screen-0"> ... </section>
    <section id="screen-1" class="hidden"> ... </section>
    <section id="screen-2" class="hidden"> ... </section>
    <section id="screen-3" class="hidden"> ... </section>
    <section id="screen-4" class="hidden"> ... </section>
    <section id="screen-5" class="hidden"> ... </section>
  </main>

  <!-- 5. Modal Panel Juri & Live Editor Tema -->
  <div id="jury-modal" class="hidden"> ... </div>

  <!-- 6. Canvas Pendukung (Confetti & Webcam Snapshot) -->
  <canvas id="confetti-canvas" class="pointer-events-none fixed inset-0 z-50 hidden"></canvas>

  <!-- 7. Logika Aplikasi (Vanilla JavaScript) -->
  <script>
    // A. GAME_CONFIG & THEME_PRESETS
    // B. Web Audio Engine (Synthesizer SFX & BGM)
    // C. Web Speech Engine (TTS id-ID)
    // D. State Manager & Screen Transitions
    // E. Game Mechanics (Pilah Sampah, Berhitung, Urutan, Timer, Kamera)
    // F. Jury Panel & Theme Switcher Controller
    // G. Inisialisasi Aplikasi (DOM Ready)
  </script>
</body>
</html>
```

---

## 3. Aturan Penulisan Logika JavaScript

* **Modular Namespace / Objek:** Hindari variabel liar di lingkup global (*polluted global scope*). Satukan fungsionalitas dalam objek manajer, contoh:
  * `AudioManager`: bertanggung jawab atas osilator audio dan volume.
  * `SpeechManager`: bertanggung jawab atas sintesis suara TTS Bahasa Indonesia.
  * `GameState`: menyimpan skor, jumlah bintang aktif, status tahap, dan daftar sampah yang sudah dipilah.
  * `ThemeManager`: menangani pergantian tema dadakan.
* **Penanganan Kesalahan (*Error Resilience*):**
  * Seluruh pemanggilan fitur browser yang membutuhkan izin pengguna (`getUserMedia`, `speechSynthesis`, `AudioContext`) wajib dibungkus dalam blok `try...catch` atau pemeriksaan kapabilitas.
  * Pastikan interaksi pertama pengguna (klik `"Mulai Misi"`) digunakan untuk membuka kunci (*resume*) `AudioContext` sesuai kebijakan peramban modern (*autoplay restriction*).
