# Desain Berbasis Konfigurasi (Config-Driven Design) & 4 Preset Tema
> **MISI CILIK: Selamatkan Lingkungan!**  
> Struktur objek `GAME_CONFIG`, diferensiasi konten Kelompok A & B, mekanisme Live Theme Switcher, dan spesifikasi 4 tema lomba.

---

## 1. Filosofi Desain: Config-Driven Architecture

Dalam ajang kompetisi media pembelajaran, kondisi lapangan sering kali menuntut perubahan tema mendadak sesuai undian panitia atau instruksi dewan juri. 

Untuk mengantisipasi hal tersebut, seluruh data permainan dipisahkan secara tegas dari logika presentasi/tampilan:
* **Logika Aplikasi (`Engine`):** Mengatur alur state (0 s/d 5), audio synthesizer, speech manager, event handler, dan animasi.
* **Konfigurasi Konten (`GAME_CONFIG`):** Menyimpan seluruh judul, teks narasi, daftar item, alasan edukatif, kategori sampah, pertanyaan kuis berjenjang, dan video pengantar.
* **Hierarki Judul Aplikasi:**
  * **Judul Payung:** `MISI CILIK: SELAMATKAN LINGKUNGAN!`
  * **Judul Sub-Tema Dinamis:** Menyesuaikan preset yang aktif (contoh: `SELAMATKAN TAMAN CERIA!`, `SELAMATKAN PANTAI & LAUT!`, `SELAMATKAN KEBUN BINATANG!`, `SELAMATKAN KELASKU!`).

Ketika nilai dalam `GAME_CONFIG` diubah (melalui preset juri), seluruh antarmuka melakukan *re-render* otomatis dalam waktu kurang dari 0.5 detik tanpa memuat ulang (*reload*) halaman.

---

## 2. Struktur Objek `GAME_CONFIG` (Dengan Skema Diferensiasi)

Struktur objek standar yang dideklarasikan di bagian paling atas skrip JavaScript:

```javascript
const GAME_CONFIG = {
  judulPayung: "MISI CILIK: SELAMATKAN LINGKUNGAN!",
  judulSubTema: "SELAMATKAN TAMAN CERIA!",
  subJudul: "Media Pembelajaran Digital Interaktif Anak TK Kelompok A/B",
  maskot: { nama: "Ara si Lebah Ceria", ikon: "🐝" },
  videoSrc: "assets/video/cerita_taman.mp4",

  // Tahap 1: Panggilan Misi
  tahap1_panggilan: {
    judul: "Tahap 1: Panggilan Misi",
    narasi: "Halo teman-teman! Aku Ara. Lihatlah, Taman Ceria kita sedang sedih karena penuh sampah dan bunganya layu...",
    pertanyaanA: [ // 🐥 Kelompok A: Observasi Konkret
      "Apa saja benda yang membuat taman menjadi kotor?",
      "Bagaimana perasaan tanaman jika kekurangan air?",
      "Siapa anak hebat yang mau ikut membantu Ara membersihkan taman?"
    ],
    pertanyaanB: [ // 🦉 Kelompok B: Analisis Sebab-Akibat
      "Mengapa sampah bisa sampai menumpuk dan berserakan di taman ini?",
      "Apa akibatnya bagi tanaman dan lebah jika sampah dibiarkan berhari-hari?",
      "Bagaimana cara kita mengajak orang lain agar tidak membuang sampah sembarangan?"
    ]
  },

  // Tahap 2: Detektif Sampah
  tahap2_detektif: {
    judul: "Tahap 2: Misi Detektif Sampah",
    instruksi: "Sentuh sampah yang dipilih, lalu masukkan ke tempat sampah yang tepat ya!",
    tong1: { label: "Sampah Organik", subLabel: "Alami / Sisa Makanan", warna: "hijau", ikon: "🍏" },
    tong2: { label: "Sampah Anorganik", subLabel: "Plastik & Kaleng", warna: "kuning", ikon: "🧴" },
    items: [
      { 
        id: 1, 
        nama: "Kulit Pisang", 
        ikon: "🍌", 
        kategori: "organik", 
        alasan: "Kulit pisang mudah membusuk dan bisa menjadi pupuk kompos alami untuk tanaman!" 
      },
      { 
        id: 2, 
        nama: "Botol Plastik", 
        ikon: "🧴", 
        kategori: "anorganik", 
        alasan: "Botol plastik butuh ratusan tahun untuk hancur dan mencemari tanah jika tidak didaur ulang!" 
      },
      { 
        id: 3, 
        nama: "Daun Kering", 
        ikon: "🍂", 
        kategori: "organik", 
        alasan: "Daun kering berasal dari alam dan bisa menyuburkan tanah saat terurai." 
      },
      { 
        id: 4, 
        nama: "Kaleng Minuman", 
        ikon: "🥫", 
        kategori: "anorganik", 
        alasan: "Kaleng logam tidak bisa membusuk sendiri dan harus dilebur kembali di pabrik daur ulang." 
      },
      { 
        id: 5, 
        nama: "Sisa Apel", 
        ikon: "🍎", 
        kategori: "organik", 
        alasan: "Sisa buah adalah bahan organik alami yang disenangi cacing tanah untuk menggemburkan tanah." 
      },
      { 
        id: 6, 
        nama: "Kantong Kresek", 
        ikon: "🛍️", 
        kategori: "anorganik", 
        alasan: "Kantong kresek plastik tipis mudah tertiup angin dan menyumbat saluran air bila dibuang sembarangan." 
      }
    ],
    kuisSiram: {
      pertanyaan: "Tanaman masih haus! Pilih benda untuk menyiram tanaman:",
      pilihanBenar: { nama: "Penyiram Air", ikon: "🚿" },
      pilihanSalah: [
        { nama: "Api", ikon: "🔥" },
        { nama: "Batu", ikon: "🪨" }
      ]
    }
  },

  // Tahap 3: Tantangan Cerdas
  tahap3_cerdas: {
    judul: "Tahap 3: Tantangan Cerdas",
    kuisHitung: {
      pertanyaan: "Wah, bunga matahari mulai mekar! Ayo hitung bersama, ada berapa bunga matahari di taman?",
      ikonBenda: "🌻",
      // Kelompok A: 1-5
      jumlahBenarA: 5,
      pilihanA: [3, 4, 5],
      // Kelompok B: 1-10
      jumlahBenarB: 10,
      pilihanB: [8, 9, 10]
    },
    kuisUrutan: {
      pertanyaan: "Ayo susun urutan tumbuhnya tanaman dari awal sampai berbunga!",
      penjelasanB: "Biji yang ditanam memerlukan air dan sinar matahari untuk tumbuh menjadi tunas, lalu berbunga indah!",
      langkah: [
        { id: 1, labelA: "1. Tanam Biji", labelB: "Tanam Biji", ikon: "🌰" },
        { id: 2, labelA: "2. Tumbuh Tunas", labelB: "Tumbuh Tunas", ikon: "🌱" },
        { id: 3, labelA: "3. Siram Air", labelB: "Siram Air", ikon: "🚿" },
        { id: 4, labelA: "4. Bunga Mekar", labelB: "Bunga Mekar", ikon: "🌷" }
      ]
    }
  },

  // Tahap 4: Aksi Nyata
  tahap4_aksiNyata: {
    judul: "Tahap 4: Aksi Nyata Penyelamat Lingkungan!",
    durasiTimerDetik: 60,
    checklistA: [ // 🐥 Kelompok A: 2 Aksi Konkret Dasar
      { teks: "Mengambil sampah di sekitar dan membuang ke tempat sampah", ikon: "🗑️" },
      { teks: "Ikut menyiram atau merawat tanaman bersama Ibu Guru", ikon: "🚿" }
    ],
    checklistB: [ // 🦉 Kelompok B: 3 Aksi Mandiri Kolaboratif
      { teks: "Mengambil dan memilah sampah organik vs anorganik di sekitar", ikon: "🗑️" },
      { teks: "Merawat tanaman sekolah dan mengingatkan teman menjaga kebersihan", ikon: "🚿" },
      { teks: "Bekerja sama dan merapikan kembali peralatan setelah beraktivitas", ikon: "🤝" }
    ]
  },

  // Tahap 5: Misi Berhasil
  tahap5_berhasil: {
    judul: "HORE! MISI BERHASIL!",
    narasi: "Terima kasih Penyelamat Cilik! Sekarang lingkungan kita sudah bersih, segar, dan indah. Kalian semua anak hebat!"
  }
};
```

---

## 3. Spesifikasi 4 Preset Sub-Tema Dadakan

Di dalam kode aplikasi, disediakan koleksi `THEME_PRESETS` yang dapat diaktifkan seketika melalui antarmuka:

### 🌻 Preset 1 (Default): Taman Ceria
* **Sub-Tema:** `SELAMATKAN TAMAN CERIA!`
* **Maskot:** `Ara si Lebah` (🐝) | Video: `assets/video/cerita_taman.mp4`
* **Latar Belakang:** Pemandangan rumput hijau dan hamparan bunga asri.
* **Misi Sampah:** Memisahkan kulit pisang, daun kering, apel vs. botol plastik, kaleng, kresek.
* **Tantangan Sains:** Menghitung 5 bunga (Kelompok A) atau 10 bunga (Kelompok B) & menyusun siklus pertumbuhan tanaman.

---

### 🌊 Preset 2: Pantai & Laut Bersih (Selamatkan Biota Laut)
* **Sub-Tema:** `SELAMATKAN PANTAI & LAUT!`
* **Maskot:** `Lulu si Lumba-lumba` (🐬) | Video: `assets/video/cerita_pantai.mp4`
* **Latar Belakang:** Pasir pantai kuning cerah dan laut biru berombak.
* **Misi Sampah:**
  * *Organik:* Rumput laut (`🌿`), cangkang kerang (`🐚`), kayu apung (`🪵`).
  * *Anorganik:* Sedotan plastik (`🥤`), botol kaca (`🍾`), jaring ikan bekas (`🕸️`).
* **Mini-Kuis Penyelamatan:** Memilih alat membebaskan penyu terjerat (`✂️ Gunting`).
* **Tantangan Sains:** Menghitung bintang laut (`⭐`) & menyusun siklus penyu (Telur → Menetas tukik → Merayap ke ombak → Berenang bebas).

---

### 🦁 Preset 3: Kebun Binatang Ceria (Sayangi Satwa Liar)
* **Sub-Tema:** `SELAMATKAN KEBUN BINATANG!`
* **Maskot:** `Mimi si Monyet Cerdik` (🐵) | Video: `assets/video/cerita_kebun_binatang.mp4`
* **Latar Belakang:** Kawasan safari asri dengan pepohonan rindang.
* **Misi Sampah:**
  * *Organik:* Kulit kacang (`🥜`), batang pisang (`🍌`), daun bambu (`🎍`).
  * *Anorganik:* Bungkus makanan ringan (`🍿`), botol sirup plastik (`🍼`), baterai bekas (`🔋`).
* **Mini-Kuis Penyelamatan:** Memilih pakan sehat untuk satwa gajah (`🥕 Wortel & Buah Segar`).
* **Tantangan Sains:** Menghitung satwa anak singa (`🦁`) & menyusun siklus kupu-kupu safari (Telur → Ulat → Kepompong → Kupu-kupu).

---

### 🏫 Preset 4: Kelasku Bersih & Rapi (Lingkungan Sekolahku)
* **Sub-Tema:** `SELAMATKAN KELASKU!`
* **Maskot:** `Budi si Pelajar Cilik` (🎒) | Video: `assets/video/cerita_kelas.mp4`
* **Latar Belakang:** Ruang kelas TK yang rapi dengan ornamen edukasi ceria.
* **Misi Sampah:**
  * *Organik:* Sisa roti bekal (`🍞`), serutan pensil kayu (`✏️`), kulit jeruk (`🍊`).
  * *Anorganik:* Wadah mika plastik (`📦`), spidol rusak (`🖊️`), selotip plastik (`🩹`).
* **Mini-Kuis Penyelamatan:** Memilih alat membersihkan papan tulis (`🧽 Penghapus Papan Tulis`).
* **Tantangan Sains:** Menghitung buku cerita (`📚`) & menyusun rutinitas pagi (Bangun tidur → Mandi & sikat gigi → Sarapan sehat → Belajar ceria di kelas).

---

## 4. Mekanisme Live Theme Switcher

1. Pengguna membuka modal sudut kanan atas `"📋 Panel Juri & Editor Tema"`.
2. Pengguna memilih Tab 2 `"🎨 Ubah Tema Cepat"`.
3. Mengklik salah satu tombol preset (misal: `"🌊 Pantai & Laut"`).
4. Fungsi `applyPreset(namaPreset)` dijalankan:
   * Menyalin nilai preset ke objek aktif `GAME_CONFIG`.
   * Memperbarui tautan video pengantar (`videoSrc`).
   * Memperbarui palet tema dan teks judul secara dinamis.
   * Menjalankan `renderAllScreens()` untuk memperbarui seluruh kontainer layar.
5. Permainan seketika siap digunakan dalam format sub-tema baru tanpa *page reload*.
