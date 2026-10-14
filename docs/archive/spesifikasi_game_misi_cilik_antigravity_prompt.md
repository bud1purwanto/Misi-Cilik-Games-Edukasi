# Project Specification: MISI CILIK - Selamatkan Taman Ceria!
**Target Platform:** Web Browser (HTML5 Single-Page Application, Offline-First / Local Execution)  
**Target Audience:** Anak TK Kelompok A/B (Usia 4–6 Tahun) & Guru TK (Lomba PORSENI XV IGTKI-PGRI JATIM - Kategori Digital)

---

## 1. Instruksi untuk AI Agent (Antigravity)
Bangun aplikasi game edukasi interaktif berbasis web dalam **satu file `index.html` mandiri (Single-File HTML)** yang mencakup HTML5, Tailwind CSS (via CDN atau internal style), dan Vanilla JavaScript. Aplikasi harus langsung berjalan mulus saat dibuka di browser laptop tanpa memerlukan server backend, serta mudah dikustomisasi untuk pergantian tema mendadak saat lomba.

### Fitur Utama yang Wajib Ada:
1. **Arsitektur Config-Driven (`GAME_CONFIG`):** Semua teks judul, narasi, soal, emoji/path gambar, dan pengaturan tema harus diletakkan dalam satu objek konstanta JavaScript `GAME_CONFIG` di bagian atas script agar peserta lomba bisa mengganti tema hanya dalam 5 menit.
2. **Built-in Web Audio Synthesizer & Web Speech API (TTS Bahasa Indonesia):**
   - Gunakan `window.speechSynthesis` (bahasa `id-ID`) untuk membacakan setiap narasi dan instruksi secara otomatis dengan suara ramah anak, ditambah fallback file audio eksternal (`assets/audio/...`).
   - Gunakan `AudioContext` (Web Audio API) untuk menghasilkan *Sound Effects* (SFX) secara terprogram tanpa bergantung pada file luar: suara *Ting/Chime* saat jawaban benar, *Buzzer lembut* saat salah, suara *Pop* saat klik tombol, dan *Fanfare* saat menang.
   - Sediakan pemutar Backsound Ceria (menggunakan generator nada ceria Web Audio API atau tag `<audio loop>`).
3. **Visual & Animasi Ramah Anak TK:**
   - Tombol berukuran ekstra besar, warna pastel/cerah kontras tinggi, sudut membulat (`rounded-3xl`), dan font ramah anak.
   - Animasi CSS bergerak (mengambang/floating, memantul/bouncing, goyang/wiggle) pada karakter maskot, bunga, dan item game.
4. **Panel Kurikulum & Rubrik Juri (Modal Pop-up):**
   - Tombol khusus bagi Guru/Juri untuk menampilkan Capaian Pembelajaran (CP), Tujuan Pembelajaran (TP), Naskah Alur Cerita, Indikator 6 Aspek Perkembangan Anak, serta informasi pemanfaatan AI.

---

## 2. Struktur Objek Konfigurasi (`GAME_CONFIG`)
Buat objek JSON/JS di bagian atas tag `<script>` seperti struktur berikut agar mudah diedit saat penentuan tema dadakan di lokasi lomba:

```javascript
const GAME_CONFIG = {
  judulUtama: "MISI CILIK: Selamatkan Taman Ceria!",
  subJudul: "Media Pembelajaran Digital Interaktif Anak TK Kelompok A/B",
  maskot: { nama: "Ara si Lebah Ceria", ikon: "🐝" },
  kurikulum: {
    cp: "Nilai Agama & Budi Pekerti, Jati Diri, serta Dasar-Dasar Literasi, Matematika, Sains, Teknologi, Rekayasa, dan Seni.",
    tp: [
      "Anak mampu mengenal perilaku merawat lingkungan dan ciptaan Tuhan (NAM).",
      "Anak mampu memilah sampah organik dan anorganik (Kognitif).",
      "Anak mampu membilang benda 1-5 dan mengurutkan pertumbuhan tanaman (Numerasi).",
      "Anak mampu menyampaikan pendapat secara lisan (Bahasa).",
      "Anak mampu bekerja sama dan mempraktikkan aksi merawat tanaman (Sosial-Emosional & Fisik Motorik)."
    ]
  },
  tahap1_panggilan: {
    judul: "Tahap 1: Panggilan Misi",
    narasi: "Halo teman-teman! Aku Ara. Lihatlah, Taman Ceria kita sedang sedih karena banyak sampah berserakan dan bunganya layu. Yuk amati bersama Ibu Guru, kenapa ya tamannya bisa kotor?",
    pertanyaanDiskusi: [
      "Apa saja benda yang membuat taman menjadi kotor?",
      "Bagaimana perasaan tanaman jika tidak pernah disiram?",
      "Siapa yang mau ikut membantu Ara membersihkan taman?"
    ]
  },
  tahap2_detektif: {
    judul: "Tahap 2: Misi Detektif Sampah",
    instruksi: "Klik sampah yang dipilih, lalu masukkan ke tempat sampah yang tepat ya!",
    items: [
      { id: 1, nama: "Kulit Pisang", ikon: "🍌", kategori: "organik" },
      { id: 2, nama: "Botol Plastik", ikon: "🧴", kategori: "anorganik" },
      { id: 3, nama: "Daun Kering", ikon: "🍂", kategori: "organik" },
      { id: 4, nama: "Kaleng Minuman", ikon: "🥫", kategori: "anorganik" },
      { id: 5, nama: "Sisa Apel", ikon: "🍎", kategori: "organik" },
      { id: 6, nama: "Kantong Kresek", ikon: "🛍️", kategori: "anorganik" }
    ]
  },
  tahap3_cerdas: {
    judul: "Tahap 3: Tantangan Cerdas",
    kuisHitung: {
      pertanyaan: "Wah, bunga matahari mulai mekar! Ayo hitung bersama, ada berapa bunga matahari di taman?",
      ikonBenda: "🌻",
      jumlahBenar: 5,
      pilihan: [3, 4, 5]
    },
    kuisUrutan: {
      pertanyaan: "Ayo susun urutan tumbuhnya tanaman dari awal sampai berbunga!",
      urutanBenar: [
        { urutan: 1, label: "1. Tanam Biji", ikon: "🌰" },
        { urutan: 2, label: "2. Tumbuh Tunas", ikon: "🌱" },
        { urutan: 3, label: "3. Siram Air", ikon: "🚿" },
        { urutan: 4, label: "4. Bunga Mekar", ikon: "🌷" }
      ]
    }
  },
  tahap4_aksiNyata: {
    judul: "Tahap 4: Aksi Nyata Penyelamat Taman!",
    instruksi: "Sekarang giliran teman-teman beraksi di kelas atau halaman sekolah bersama Ibu Guru!",
    daftarAksi: [
      { teks: "Mengambil sampah di sekitar dan membuang ke tempatnya", ikon: "🗑️" },
      { teks: "Menyiram tanaman di taman sekolah dengan tertib", ikon: "🚿" },
      { teks: "Bergantian dan bekerja sama dengan teman", ikon: "🤝" }
    ],
    durasiTimerDetik: 60
  },
  tahap5_berhasil: {
    judul: "HORE! MISI BERHASIL!",
    narasi: "Terima kasih Penyelamat Cilik! Sekarang Taman Ceria sudah bersih, segar, dan penuh bunga warna-warni. Kalian semua anak hebat!"
  }
};
```

---

## 3. Rancangan Antarmuka & Alur Layar (6 State Layar)

### Komponen Global (Selalu Tampil di Bagian Atas):
- **Header Navigasi:**
  - Kiri: Nama Game & Indikator Tahap Aktif (Step 1 s/d 5).
  - Tengah: Perolehan Bintang Anak (`⭐ x 0` hingga `⭐ x 5`) dengan animasi lompat saat bertambah.
  - Kanan: Tombol `🔊 Suara Narasi`, Tombol `🎵 Musik`, dan Tombol `📋 Info Juri / CP-TP & Editor Tema`.

---

### Layar 0: Beranda (Home Screen)
- **Visual:** Latar belakang taman kartun yang cerah dengan animasi awan bergerak dan maskot `🐝 Ara` yang melambai-lambai.
- **Konten:**
  - Judul besar **"MISI CILIK: Selamatkan Taman Ceria!"**.
  - Tombol utama berukuran raksasa dengan animasi berdenyut: **"🚀 MULAI MISI SEKARANG!"**.
  - Tombol sekunder: **"⚙️ Ubah Tema Cepat (Mode Lomba)"** — membuka modal di mana guru bisa langsung mengganti judul, narasi, dan ikon dari layar tanpa mengedit kode!

---

### Layar 1: Tahap 1 — Panggilan Misi (Observasi & Bahasa)
- **Visual:** Simulasi video animasi interaktif (menggunakan Canvas/CSS Keyframe Scene) yang menampilkan Taman Kotor (banyak sampah berserakan, tanaman layu berwarna kecokelatan, langit agak mendung).
- **Fitur Interaktif:**
  - Tombol **"▶️ Putar Cerita Animasi"** yang memicu pergerakan visual di layar sekaligus membacakan narasi via AI Text-to-Speech (TTS).
  - **Kotak Diskusi Guru & Anak:** Menampilkan 3 kartu pertanyaan pemantik. Saat anak berhasil menjawab di kelas, guru mengklik tombol **"🗣️ Anak Sudah Berpendapat (+1 ⭐)"** untuk memberikan efek suara tepuk tangan.
  - Tombol lanjut ke Tahap 2.

---

### Layar 2: Tahap 2 — Misi Detektif (Pilah Sampah & Merawat Tanaman)
- **Visual:** Area taman dengan 6 item sampah yang mengambang. Di bagian bawah terdapat 2 Tempat Sampah Besar yang interaktif:
  1. **Tong Hijau (Sampah Organik / Alami 🍏🍂)**
  2. **Tong Kuning (Sampah Anorganik / Plastik & Kaleng 🧴🥫)**
- **Mekanisme Gameplay (Ramah Layar Sentuh & Mouse Proyektor):**
  - Mendukung **Drag-and-Drop** maupun **2-Click System** (Klik item sampah dulu hingga menyala, lalu klik Tong Sampah tujuan — sangat memudahkan anak TK saat maju ke depan laptop/proyektor).
- **Umpan Balik Evaluasi:**
  - **Jika Benar:** Suara *Ting!* ceria, animasi bintang terbang, sampah masuk ke tong, dan suara TTS *"Hebat! Itu sampah organik/anorganik!"*.
  - **Jika Salah:** Tong bergoyang pelan (*shake animation*), suara *Tetot* lembut, dan suara TTS *"Ups, coba perhatikan lagi ya!"*.
- Setelah semua sampah bersih, muncul sub-pilihan singkat: **"Tanaman masih haus! Pilih benda untuk menyiram tanaman:"** (Pilihan: 🚿 Penyiram Air [Benar] vs 🔥 Api vs 🪨 Batu).

---

### Layar 3: Tahap 3 — Tantangan Cerdas (Numerasi & Kognitif)
Terdiri dari 2 Sub-Tantangan di layar yang sama (bergantian secara tab/step):
1. **Sub-Tantangan A (Menghitung Bunga):**
   - Menampilkan bunga-bunga yang bermekaran di taman. Saat bunga diklik satu per satu oleh anak, muncul angka di atas bunga (`1, 2, 3, 4, 5`) disertai suara hitungan TTS Bahasa Indonesia!
   - Di bawahnya ada 3 tombol jawaban angka besar (`3`, `4`, `5`).
2. **Sub-Tantangan B (Mengurutkan Pertumbuhan Tanaman):**
   - Menampilkan 4 kartu acak (Tanam Biji, Tumbuh Tunas, Siram Air, Bunga Mekar).
   - Anak mengklik kartu secara berurutan dari langkah 1 hingga 4 untuk menyusunnya ke dalam kotak urutan.

---

### Layar 4: Tahap 4 — Aksi Nyata (Fisik-Motorik & Sosial-Emosional)
- **Visual:** Layar instruksi kegiatan fisik di dunia nyata dengan hitung mundur waktu (*Countdown Timer* besar 60 detik yang bisa diatur/di-skip oleh guru) dan musik penyemangat.
- **Fitur Interaktif:**
  - Daftar *Checklist* Aksi Nyata dengan ikon besar yang bisa dicentang satu per satu saat anak mempraktikkannya di kelas.
  - **Fitur Kamera Apresiasi Langsung (`getUserMedia` Webcam):** Tombol **"📸 Buka Kamera & Foto Aksi Anak"** agar wajah anak-anak yang sedang beraksi atau memegang alat peraga bisa tampil langsung di layar proyektor dan difoto sebagai bukti aksi nyata! (Sertakan fallback aman jika kamera tidak diizinkan).

---

### Layar 5: Tahap 5 — Misi Berhasil! (Transformasi & Evaluasi Akhir)
- **Visual:**
  - Efek hujan *Confetti* warna-warni di seluruh layar.
  - **Animasi Before-After Taman:** Taman yang tadinya kotor kini berubah menjadi **Taman Ceria** yang sangat indah, rumput hijau segar, bunga-bunga mekar bergoyang, pelangi di langit, dan kupu-kupu beterbangan.
  - Menampilkan **Sertifikat / Lencana Digital "Penyelamat Taman Cilik"** lengkap dengan foto tangkapan layar dari Tahap 4 (jika ada) dan total perolehan **5 Bintang Emas (⭐⭐⭐⭐⭐)**.
- **Evaluasi & Refleksi Guru:**
  - Kartu refleksi lisan: *"Bagaimana perasaan teman-teman melihat taman sudah bersih?"*
  - **Tabel Rubrik Observasi Cepat Guru:** Guru bisa langsung mengklik centang penilaian cepat untuk 6 aspek perkembangan (NAM, Kognitif, Bahasa, Sosek, Motorik, Literasi Digital) dan menekan tombol **"🖨️ Cetak / Simpan Hasil Evaluasi"**.

---

## 4. Fitur Tambahan Khusus Penilaian Juri PORSENI
Tambahkan tombol **"📋 Panel Juri & Editor Tema"** di pojok kanan atas yang membuka Modal berisi 2 Tab:
1. **Tab 1: Dokumen Naskah, CP/TP & Kriteria Lomba:**
   - Menampilkan kesesuaian media dengan Kurikulum Merdeka PAUD, alur naskah sistematis, serta penjelasan bagaimana AI digunakan dalam media ini (AI Voice TTS, AI Generative Config, dan AI Evaluasi).
2. **Tab 2: Editor Tema Dadakan (Live Theme Changer):**
   - Form input sederhana di mana peserta bisa langsung mengubah:
     - Judul Game & Nama Maskot
     - Preset Tema Sekali Klik:
       1. 🌻 **Tema Taman Ceria** (Default)
       2. 🌊 **Tema Pantai & Laut Bersih** (Selamatkan Biota Laut)
       3. 🦁 **Tema Kebun Binatang Ceria** (Sayangi Hewan)
       4. 🏫 **Tema Kelasku Bersih & Rapi** (Lingkungan Sekolah)
   - *Catatan Penting:* Sediakan **4 Preset Tema Lengkap** di dalam kode JavaScript sehingga saat hari-H lomba dan juri menentukan tema dadakan, guru bisa langsung memilih preset yang paling mendekati atau mengedit teks/emoji secara instan di layar tanpa menyentuh kode!

---

## 5. Kriteria Teknis Kode (Deliverable)
- Buat seluruh kode dalam **1 file `index.html`** yang lengkap, bersih, tanpa *placeholder* yang terpotong.
- Gunakan **Tailwind CSS CDN** untuk layout responsif dan tambahkan custom CSS untuk animasi `@keyframes` (floating, bounce, shake, confetti).
- Pastikan semua tombol memiliki efek suara dan umpan balik visual yang instan.