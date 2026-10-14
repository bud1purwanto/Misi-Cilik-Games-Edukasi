# Desain Berbasis Konfigurasi (Config-Driven Design) & 4 Preset Tema
> **MISI CILIK: Selamatkan Taman Ceria!**  
> Struktur objek `GAME_CONFIG`, mekanisme Live Theme Switcher, dan spesifikasi 4 tema lomba.

---

## 1. Filosofi Desain: Config-Driven Architecture

Dalam ajang kompetisi media pembelajaran, kondisi lapangan sering kali menuntut perubahan tema mendadak sesuai undian panitia atau instruksi dewan juri. 

Untuk mengantisipasi hal tersebut, seluruh data permainan dipisahkan secara tegas dari logika presentasi/tampilan:
* **Logika Aplikasi (`Engine`):** Mengatur alur state, audio synthesizer, event handler, dan animasi.
* **Konfigurasi Konten (`GAME_CONFIG`):** Menyimpan seluruh judul, teks narasi, daftar item, ikon/emoji, kategori sampah, pertanyaan kuis, dan data rubrik juri.

Ketika nilai dalam `GAME_CONFIG` diubah (baik melalui script maupun via modal antarmuka pengguna), seluruh antarmuka melakukan *re-render* otomatis tanpa memuat ulang (*reload*) halaman.

---

## 2. Struktur Objek `GAME_CONFIG`

Struktur objek standar yang dideklarasikan di bagian paling atas skrip JavaScript:

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
    narasi: "Halo teman-teman! Aku Ara. Lihatlah, Taman Ceria kita sedang sedih karena banyak sampah berserakan dan bunganya layu...",
    pertanyaanDiskusi: [
      "Apa saja benda yang membuat taman menjadi kotor?",
      "Bagaimana perasaan tanaman jika tidak pernah disiram?",
      "Siapa yang mau ikut membantu Ara membersihkan taman?"
    ]
  },

  tahap2_detektif: {
    judul: "Tahap 2: Misi Detektif Sampah",
    instruksi: "Sentuh sampah yang dipilih, lalu masukkan ke tempat sampah yang tepat ya!",
    tong1: { label: "Sampah Organik", subLabel: "Alami / Sisa Makanan", warna: "hijau", ikon: "🍏" },
    tong2: { label: "Sampah Anorganik", subLabel: "Plastik & Kaleng", warna: "kuning", ikon: "🧴" },
    items: [
      { id: 1, nama: "Kulit Pisang", ikon: "🍌", kategori: "organik" },
      { id: 2, nama: "Botol Plastik", ikon: "🧴", kategori: "anorganik" },
      { id: 3, nama: "Daun Kering", ikon: "🍂", kategori: "organik" },
      { id: 4, nama: "Kaleng Minuman", ikon: "🥫", kategori: "anorganik" },
      { id: 5, nama: "Sisa Apel", ikon: "🍎", kategori: "organik" },
      { id: 6, nama: "Kantong Kresek", ikon: "🛍️", kategori: "anorganik" }
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
    judul: "Tahap 4: Aksi Nyata Penyelamat Lingkungan!",
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

## 3. Spesifikasi 4 Preset Tema Dadakan

Dalam kode aplikasi, disediakan koleksi `THEME_PRESETS` yang siap dipakai seketika:

### 🌻 Preset 1 (Default): Taman Ceria
* **Maskot:** `Ara si Lebah` (🐝)
* **Latar Belakang Visual:** Taman bermain rumput hijau, awan biru, bunga-bunga mekar.
* **Misi Sampah:** Memisahkan kulit pisang, daun kering, apel vs. botol plastik, kaleng, kresek.
* **Tantangan Sains:** Menghitung 5 bunga matahari & mengurutkan siklus tumbuh biji hingga mekar.

---

### 🌊 Preset 2: Pantai & Laut Bersih (Selamatkan Biota Laut)
* **Maskot:** `Lulu si Lumba-lumba` (🐬)
* **Latar Belakang Visual:** Pasir pantai kuning cerah dan laut biru berombak.
* **Misi Sampah:**
  * *Organik:* Rumput laut terdampar (`🌿`), cangkang kerang (`🐚`), sisa kayu lapuk (`🪵`).
  * *Anorganik:* Sedotan plastik (`🥤`), botol kaca (`🍾`), jaring plastik bekas (`🕸️`).
* **Mini-Kuis Penyelamatan:** Memilih benda untuk membebaskan penyu terjepit jaring (`✂️ Gunting` vs `🔥 Api` vs `🪨 Batu`).
* **Tantangan Sains:** Menghitung 5 bintang laut (`⭐`) & mengurutkan siklus penyu (Telur di pasir → Menetas tukik → Merayap ke ombak → Berenang bebas di samudra).

---

### 🦁 Preset 3: Kebun Binatang Ceria (Sayangi Satwa)
* **Maskot:** `Mimi si Monyet Cerdik` (🐵)
* **Latar Belakang Visual:** Hutan safari savana dengan kandang hewan asri.
* **Misi Sampah:**
  * *Organik:* Kulit kacang (`🥜`), batang pisang (`🍌`), daun bambu sisa panda (`🎍`).
  * *Anorganik:* Bungkus makanan ringan (`🍿`), botol sirup plastik (`🍼`), baterai bekas (`🔋`).
* **Mini-Kuis Penyelamatan:** Memilih makanan sehat untuk gajah (`🥕 Wortel & Buah` vs `🍬 Permen` vs `🪨 Batu`).
* **Tantangan Sains:** Menghitung 5 anak singa (`🦁`) & mengurutkan metamorfosis kupu-kupu safari (Telur → Ulat bulu → Kepompong → Kupu-kupu mekar).

---

### 🏫 Preset 4: Kelasku Bersih & Rapi (Lingkungan Sekolah)
* **Maskot:** `Budi si Pelajar Cilik` (🎒)
* **Latar Belakang Visual:** Ruang kelas TK yang penuh hiasan gantung warna-warni dan meja belajar.
* **Misi Sampah:**
  * *Organik:* Sisa roti bekal (`🍞`), serutan pensil kayu (`✏️`), kulit jeruk (`🍊`).
  * *Anorganik:* Wadah plastik mika (`📦`), spidol rusak (`🖊️`), selotip plastik bekas (`🩹`).
* **Mini-Kuis Penyelamatan:** Memilih alat untuk membersihkan papan tulis (`🧽 Penghapus Papan` vs `🪥 Sikat Gigi` vs `🥄 Sendok`).
* **Tantangan Sains:** Menghitung 5 buku cerita bergambar (`📚`) & mengurutkan rutinitas pagi (Bangun tidur → Mandi & gosok gigi → Sarapan → Masuk kelas TK dengan senyum).

---

## 4. Cara Kerja Live Theme Switcher

1. Guru membuka modal pojok kanan atas `"📋 Panel Juri & Editor Tema"`.
2. Guru memilih Tab `"🎨 Ubah Tema Cepat"`.
3. Guru mengklik salah satu tombol preset (misal: `"🌊 Pantai & Laut"`).
4. Fungsi `applyPreset(namaPreset)` dijalankan:
   * Menyalin nilai preset ke objek aktif `GAME_CONFIG`.
   * Memanggil fungsi render: `renderAllScreens()`.
   * Memperbarui warna aksen antarmuka (misal: warna hijau emerald berubah menjadi biru laut).
5. Seluruh state kembali siap dimainkan dalam hitungan 0.5 detik tanpa reload halaman browser.
