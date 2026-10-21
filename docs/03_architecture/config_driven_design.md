# Desain Berbasis Konfigurasi (Config-Driven Design) & 4 Preset Tema
> **MISI CILIK: Selamatkan Lingkungan!**  
> Struktur objek `GAME_CONFIG`, diferensiasi konten Kelompok A (4 item) vs Kelompok B (6 item), objek numerasi spesifik tema, dan pemisahan Mode Anak vs Mode Guru.

---

## 1. Filosofi Desain: Config-Driven Architecture

Dalam ajang kompetisi media pembelajaran, kondisi lapangan sering kali menuntut perubahan tema mendadak sesuai undian panitia atau instruksi dewan juri. 

Untuk mengantisipasi hal tersebut, seluruh data permainan dipisahkan secara tegas dari logika presentasi/tampilan:
* **Logika Aplikasi (`Engine`):** Mengatur alur state (0 s/d 5), audio synthesizer, speech manager, event handler, dan animasi.
* **Konfigurasi Konten (`GAME_CONFIG`):** Menyimpan seluruh judul, teks narasi, daftar item sampah A & B, alasan edukatif, nama dan ikon objek numerasi spesifik tema, pertanyaan kuis berjenjang, dan video pengantar.
* **Hierarki Judul Aplikasi:**
  * **Judul Payung:** `MISI CILIK: SELAMATKAN LINGKUNGAN!`
  * **Judul Sub-Tema Dinamis:** Menyesuaikan preset yang aktif (`SELAMATKAN TAMAN CERIA!`, `SELAMATKAN PANTAI & LAUT!`, `SELAMATKAN KEBUN BINATANG!`, `SELAMATKAN KELASKU!`).
* **Pemisahan Mode Antarmuka (Dual-Mode):**
  * `childMode`: Tampilan permainan bersih, ceria, minim teks teknis, ramah anak.
  * `teacherMode`: Panel kontrol guru/juri, editor tema dadakan, lembar asesmen observasi autentik, dan rekap portofolio Local Storage.

---

## 2. Struktur Objek `GAME_CONFIG` (Revisi Lengkap)

Struktur objek standar yang dideklarasikan di skrip JavaScript:

```javascript
const GAME_CONFIG = {
  id: "taman",
  judulPayung: "MISI CILIK: SELAMATKAN LINGKUNGAN!",
  judulSubTema: "SELAMATKAN TAMAN CERIA!",
  subJudul: "Media Pembelajaran Digital Interaktif Anak TK Kelompok A/B",
  maskot: { nama: "Ara si Lebah Ceria", ikon: "🐝" },
  videoSrc: "assets/video/cerita_taman.mp4",

  // Tahap 1: Panggilan Misi
  tahap1: {
    judul: "Tahap 1: Panggilan Misi",
    narasi: "Halo teman-teman! Aku Ara. Lihatlah, tempat kita sedang sangat sedih karena penuh sampah dan tanamannya layu kehausan...",
    kondisiVisual: "Banyak Sampah & Kering",
    pertanyaanA: [ // 🐥 Kelompok A: Observasi Konkret
      "Apa saja benda yang membuat tempat ini jadi kotor?",
      "Bagaimana perasaan tanaman jika kekurangan air?",
      "Siapa anak hebat yang mau ikut membantu Ara membersihkan taman?"
    ],
    pertanyaanB: [ // 🦉 Kelompok B: Analisis Sebab-Akibat
      "Mengapa sampah bisa sampai menumpuk dan berserakan di tempat ini?",
      "Apa bahayanya bagi tanaman dan hewan jika sampah dibiarkan berhari-hari?",
      "Bagaimana cara kita mengajak orang lain agar tidak membuang sampah sembarangan?"
    ]
  },

  // Tahap 2: Detektif Sampah (Diferensiasi Item A vs B)
  tahap2: {
    judul: "Tahap 2: Misi Detektif Sampah",
    instruksi: "Sentuh sampah yang dipilih, lalu masukkan ke tempat sampah yang tepat ya!",
    tong1: { label: "Sampah Organik", subLabel: "Alami / Mudah Membusuk", warna: "hijau", ikon: "🍏" },
    tong2: { label: "Sampah Anorganik", subLabel: "Plastik & Kaleng", warna: "kuning", ikon: "🧴" },
    
    // 🐥 Kelompok A: 4 Item Sampah Konkret & Kontras Tinggi
    itemsA: [
      { id: 1, nama: "Kulit Pisang", ikon: "🍌", kategori: "organik" },
      { id: 2, nama: "Botol Plastik", ikon: "🧴", kategori: "anorganik" },
      { id: 3, nama: "Daun Kering", ikon: "🍂", kategori: "organik" },
      { id: 4, nama: "Kantong Kresek", ikon: "🛍️", kategori: "anorganik" }
    ],

    // 🦉 Kelompok B: 6 Item Sampah Lengkap + Alasan Ilmiah Sebab-Akibat
    itemsB: [
      { id: 1, nama: "Kulit Pisang", ikon: "🍌", kategori: "organik", alasan: "Kulit pisang mudah membusuk dan bisa menjadi pupuk kompos alami untuk menyuburkan tanah!" },
      { id: 2, nama: "Botol Plastik", ikon: "🧴", kategori: "anorganik", alasan: "Botol plastik butuh ratusan tahun untuk hancur dan mencemari tanah bila tidak didaur ulang!" },
      { id: 3, nama: "Daun Kering", ikon: "🍂", kategori: "organik", alasan: "Daun kering adalah bahan alami yang membantu menjaga kelembapan tanah saat terurai." },
      { id: 4, nama: "Kaleng Minuman", ikon: "🥫", kategori: "anorganik", alasan: "Kaleng logam tajam dan berbahaya bagi hewan serta harus didaur ulang di pabrik peleburan." },
      { id: 5, nama: "Sisa Apel", ikon: "🍎", kategori: "organik", alasan: "Sisa buah adalah makanan alami cacing tanah yang bertugas menggemburkan tanah kebun." },
      { id: 6, nama: "Kantong Kresek", ikon: "🛍️", kategori: "anorganik", alasan: "Kantong plastik tipis mudah tertiup angin dan menyumbat saluran air hingga memicu banjir." }
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
  tahap3: {
    judul: "Tahap 3: Tantangan Cerdas",
    kuisHitung: {
      // Objek & Teks Spesifik Tema (Bebas Bocoran Angka)
      namaBenda: "Bunga Matahari",
      ikonBenda: "🌻",
      instruksiHitung: "Wah, bunga matahari mulai mekar! Ayo sentuh dan hitung satu per satu, lalu tebak berapa jumlah bunganya!",
      // Kelompok A (1-5)
      jumlahBenarA: 5,
      pilihanA: [3, 4, 5],
      // Kelompok B (1-10)
      jumlahBenarB: 10,
      pilihanB: [8, 9, 10]
    },
    kuisUrutan: {
      pertanyaan: "Ayo susun urutan tumbuhnya tanaman dari awal sampai berbunga!",
      penjelasanB: "Biji yang ditanam memerlukan air dan sinar matahari untuk tumbuh menjadi tunas, hingga mekar menjadi bunga asri!",
      langkah: [
        { id: 1, labelA: "1. Tanam Biji", labelB: "Tanam Biji", ikon: "🌰" },
        { id: 2, labelA: "2. Tumbuh Tunas", labelB: "Tumbuh Tunas", ikon: "🌱" },
        { id: 3, labelA: "3. Siram Air", labelB: "Siram Air", ikon: "🚿" },
        { id: 4, labelA: "4. Bunga Mekar", labelB: "Bunga Mekar", ikon: "🌷" }
      ]
    }
  },

  // Tahap 4: Aksi Nyata
  tahap4: {
    judul: "Tahap 4: Aksi Nyata Penyelamat Lingkungan!",
    durasiTimerDetik: 60,
    checklistA: [ // 🐥 Kelompok A: 2 Aksi Terbimbing
      { teks: "Mengambil sampah di sekitar dan membuang ke tempat sampah", ikon: "🗑️" },
      { teks: "Ikut menyiram atau merawat tanaman bersama Ibu Guru", ikon: "🚿" }
    ],
    checklistB: [ // 🦉 Kelompok B: 3 Aksi Mandiri Kolaboratif
      { teks: "Mengambil dan memilah sampah organik vs anorganik di sekitar", ikon: "🗑️" },
      { teks: "Merawat lingkungan sekolah dan mengingatkan teman menjaga kebersihan", ikon: "🚿" },
      { teks: "Bekerja sama dan merapikan kembali peralatan setelah beraktivitas", ikon: "🤝" }
    ]
  },

  // Tahap 5: Misi Berhasil
  tahap5: {
    judul: "HORE! MISI BERHASIL!",
    narasi: "Terima kasih Penyelamat Cilik! Sekarang lingkungan kita sudah bersih, segar, dan indah. Kalian semua anak hebat!"
  }
};
```

---

## 3. Spesifikasi 4 Preset Sub-Tema Dadakan

Di dalam kode aplikasi, disediakan koleksi `THEME_PRESETS` yang siap dipakai seketika:

### 🌻 Preset 1 (Default): Taman Ceria
* **Sub-Tema:** `SELAMATKAN TAMAN CERIA!`
* **Maskot:** `Ara si Lebah` (🐝) | Video: `assets/video/cerita_taman.mp4`
* **Objek Numerasi:** **Bunga Matahari** (`🌻`)
* **Sampah Kelompok A (4 Item):** Pisang, Daun vs Botol, Kresek
* **Sampah Kelompok B (6 Item):** Pisang, Daun, Apel vs Botol, Kaleng, Kresek

---

### 🌊 Preset 2: Pantai & Laut Bersih (Selamatkan Biota Laut)
* **Sub-Tema:** `SELAMATKAN PANTAI & LAUT!`
* **Maskot:** `Lulu si Lumba-lumba` (🐬) | Video: `assets/video/cerita_pantai.mp4`
* **Objek Numerasi (Revisi):** **Bintang Laut** (`⭐`)
  * Instruksi: *"Wah, banyak bintang laut berkilau di pantai! Ayo sentuh dan hitung satu per satu, lalu tebak ada berapa jumlah semua bintang lautnya!"*
* **Sampah Kelompok A (4 Item):** Kulit Apel, Daun Kelapa vs Botol Plastik, Sedotan Plastik
* **Sampah Kelompok B (6 Item):** Rumput Laut, Cangkang Kerang, Kayu Apung vs Botol Plastik, Jaring Ikan Kusut, Sedotan Plastik (disertai alasan bahaya jeratan penyu)
* **Mini-Kuis Penyelamatan:** Memilih `✂️ Gunting` untuk membebaskan penyu terjerat jaring.
* **Tantangan Sains:** Mengurutkan siklus hidup penyu (Telur di pasir → Tukik menetas → Merayap ke ombak → Berenang bebas).

---

### 🦁 Preset 3: Kebun Binatang Ceria (Sayangi Satwa Safari)
* **Sub-Tema:** `SELAMATKAN KEBUN BINATANG!`
* **Maskot:** `Mimi si Monyet Cerdik` (🐵) | Video: `assets/video/cerita_zoo.mp4`
* **Objek Numerasi (Revisi):** **Hewan / Satwa Safari** (`🦁`)
  * Instruksi: *"Wah, hewan-hewan safari melompat riang! Ayo sentuh dan hitung satu per satu, lalu tebak ada berapa jumlah semua hewannya!"*
* **Sampah Kelompok A (4 Item):** Kulit Pisang, Daun Bambu vs Bungkus Snack, Botol Plastik
* **Sampah Kelompok B (6 Item):** Kulit Kacang, Batang Pisang, Daun Bambu vs Kemasan Plastik Snack, Botol Sirup, Baterai Bekas B3 (disertai alasan bahaya zat beracun bagi pencernaan hewan)
* **Mini-Kuis Penyelamatan:** Memilih `🥕 Wortel & Buah Segar` untuk pakan sehat satwa gajah.
* **Tantangan Sains:** Mengurutkan metamorfosis kupu-kupu safari (Telur → Ulat bulu → Kepompong → Kupu-kupu mekar).

---

### 🏫 Preset 4: Kelasku Bersih & Rapi (Lingkungan Sekolahku)
* **Sub-Tema:** `SELAMATKAN KELASKU!`
* **Maskot:** `Budi si Pelajar Cilik` (🎒) | Video: `assets/video/cerita_kelas.mp4`
* **Objek Numerasi (Revisi):** **Peralatan Sekolah / Buku** (`📚`)
  * Instruksi: *"Wah, banyak peralatan sekolah rapi di meja! Ayo sentuh dan hitung satu per satu, lalu tebak ada berapa jumlah peralatan sekolahnya!"*
* **Sampah Kelompok A (4 Item):** Kulit Jeruk, Kertas Bekas vs Gelas Plastik, Kotak Mika Plastik
* **Sampah Kelompok B (6 Item):** Serutan Pensil Kayu, Kertas Bekas, Kulit Jeruk vs Wadah Mika Plastik, Spidol Bekas Rusak, Selotip Plastik (disertai alasan kimia spidol)
* **Mini-Kuis Penyelamatan:** Memilih `🧽 Penghapus Papan Tulis` untuk membersihkan papan tulis.
* **Tantangan Sains:** Mengurutkan rutinitas pagi (Bangun tidur → Mandi & sikat gigi → Sarapan sehat → Masuk kelas dengan ceria).

---

## 4. Mekanisme Penerapan Tema & Dual-Mode

1. Pengguna membuka modal sudut kanan atas `"📋 Panel Juri & Editor"`.
2. Pengguna memilih Tab 2 `"🎨 Ubah Tema Cepat"`.
3. Mengklik tombol preset tema yang diinginkan.
4. Fungsi `applyPreset(namaPreset)` dijalankan:
   * Menyalin konfigurasi preset ke objek aktif `GAME_CONFIG`.
   * Menyesuaikan objek dan instruksi hitung numerasi (bunga matahari / bintang laut / hewan / alat sekolah).
   * Menyesuaikan item sampah Kelompok A (4 item) dan Kelompok B (6 item berargumen).
   * Memperbarui tautan video dan palet warna.
   * Menjalankan `renderAllScreens()` untuk memperbarui seluruh layar dalam hitungan <0.5 detik.
