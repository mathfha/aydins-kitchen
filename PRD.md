# Product Requirements Document (PRD)
## aydin’s Kitchen – Website Katalog & Pemesanan Kue Rumahan

---

## 1. Ringkasan Produk & Tujuan Bisnis

### 1.1 Latar Belakang
aydin’s Kitchen adalah usaha kue rumahan milik Winda Safitri yang berbasis di Gambut, Kabupaten Banjar (area layanan Gambut & Banjarmasin). Produk spesialisasi utama adalah kue ulang tahun berbahan dasar brownies (rich, fudgy, dan custom decor), di samping pesanan kue pendukung lainnya.

Saat ini interaksi penjualan terhambat oleh proses manual via WhatsApp: calon pembeli berulang kali menanyakan variasi desain, meminta contoh foto satu per satu, dan menanyakan estimasi harga. Hal ini membebani waktu pemilik toko dan sering membuat calon pembeli batal memesan karena respon lama.

### 1.2 Tujuan Produk
1. Menyediakan etalase visual (digital showcase) 30–50 foto kue terkurasi yang cepat, ringan, dan estetik di layar HP.
2. Memangkas friksi tanya-jawab awal dengan mencantumkan estimasi harga, ukuran, dan detail base brownies di setiap kue.
3. Mengarahkan konversi langsung ke WhatsApp dengan draf pesan otomatis berisi nama kue, link foto referensi, dan opsi pengiriman.

### 1.3 Key Performance Indicators (KPI)
| Metrik | Target Awal (Bulan ke-1) |
| :--- | :--- |
| **Mobile Page Speed (LCP)** | < 1.8 detik di jaringan 4G |
| **Google Lighthouse Performance** | Skor ≥ 90 di perangkat mobile |
| **Rasio Klik WA (Conversion Rate)** | ≥ 15% dari total unique visitor |
| **Efisiensi Chat WA** | Penurunan 80% pertanyaan "Minta foto contoh kue" |

---

## 2. Persona Pengguna & Skenario

### 2.1 Profil Persona
| Atribut | Persona 1: Rina (Mom Planner) | Persona 2: Fikri (Instant Gifter) |
| :--- | :--- | :--- |
| **Usia & Domisili** | 29 tahun, Banjarmasin Selatan | 23 tahun, Gambut |
| **Kebutuhan** | Cari kue ultah anak tema custom base brownies | Cari kue dadakan/simpel estetis untuk pacar |
| **Pain Point** | Capek scroll IG feed yang tercampur konten promo | Tidak tahu harga pasaran, takut kemahalan |
| **Perangkat** | Smartphone Android mid-range | Smartphone iPhone / Android |

### 2.2 Skenario Penggunaan Utama
1. Rina mengeklik link di bio Instagram aydin’s Kitchen.
2. Rina langsung melihat galeri foto masonry kue brownies ulang tahun.
3. Rina memfilter kategori "Brownies Ultah Karakter".
4. Mengetuk foto kue yang diminati: lightbox transisi mulus terbuka menampilkan detail diameter, harga mulai Rp 150.000, dan tekstur brownies.
5. Rina mengetuk tombol **"Pesan Desain Kue Ini"**.
6. Aplikasi WhatsApp terbuka dengan pesan terisi otomatis lengkap dengan nama kue dan link fotonya.

---

## 3. Sitemap & Arsitektur Informasi

Untuk menjaga scope realistis bagi 1 developer (mahasiswa) dan performa instan bagi pengunjung, website menggunakan arsitektur **Single Page Portfolio (SPA/SSG)** dengan URL State Modal:

```
[ Beranda: / ]
├── Header & Sticky Mini-Bar (Logo aydin's Kitchen, Status Buka/PO, Tombol Chat WA)
├── Hero Banner (Spesialisasi Kue Brownies Gambut & Banjarmasin, CTA Lihat Galeri)
├── Bar Filter Kategori (Semua, Brownies Ultah, Bento Cake, Kue Potong/Kering)
├── Galeri Interaktif Masonry Grid (30–50 Foto + Hover/Tap Preview)
│   └── [Modal Lightbox: /#cake-:id] (Shared element zoom, deskripsi, harga, CTA WA)
├── Alur & Syarat Pemesanan (H-2 / H-3, Pengiriman Ambil Sendiri / Kurir Lokal)
├── FAQ & Area Layanan (Gambut, Kertak Hanyar, Banjarmasin Kota)
└── Footer (Alamat Gambut, Jam Operasional, Instagram, WhatsApp)
```

---

## 4. Functional Requirements

### 4.1 Modul Halaman Beranda & Galeri

| ID | Fitur | User Story | Acceptance Criteria |
| :--- | :--- | :--- | :--- |
| **FR-01** | **Hero & Value Proposition** | Sebagai pengunjung, saya ingin langsung tahu spesialisasi aydin's Kitchen agar yakin memesan. | 1. Menampilkan headline jelas: spesialisasi kue ultah base brownies di Gambut & Banjarmasin.<br>2. Tombol CTA mengarah smooth-scroll ke galeri kue.<br>3. Badge info: "Sistem Made by Order / Pre-Order H-3". |
| **FR-02** | **Filter Kategori Dinamis** | Sebagai pengunjung, saya ingin menyaring kue berdasarkan jenis agar cepat menemukan yang dicari. | 1. Filter aktif: "Semua", "Brownies Ultah", "Bento Cake", "Kue Kering/Lainnya".<br>2. Transisi filter memakai animasi reorder halus tanpa refresh halaman.<br>3. Menampilkan indikator jumlah kue per kategori. |
| **FR-03** | **Masonry Card Interaktif** | Sebagai pengunjung, saya ingin melihat foto kue dengan proporsi estetik. | 1. Grid masonry 2 kolom (mobile) dan 3–4 kolom (desktop).<br>2. Menampilkan badge nama kue dan estimasi harga saat hover (desktop) atau tap (mobile).<br>3. Skeleton/blur-up placeholder saat gambar memuat. |
| **FR-04** | **Lightbox Shared-Element** | Sebagai pengunjung, saya ingin melihat detail foto ukuran penuh dan spesifikasi kue. | 1. Klik kartu memicu animasi zoom transisi dari posisi asal kartu.<br>2. Menampilkan: Foto resolusi penuh, Nama Kue, Base Cake (Brownies), Pilihan Ukuran, Kisaran Harga, dan Tombol "Pesan Desain Ini".<br>3. Bisa ditutup dengan tombol silang, klik luar modal, tombol Escape, atau swipe down di mobile. |
| **FR-05** | **Section Cara Pesan & Pengiriman** | Sebagai pembeli, saya ingin tahu cara ambil/kirim kue sebelum chat WA. | 1. Penjelasan opsi: Ambil sendiri di Gambut atau Diantar kurir lokal (Gambut/Banjarmasin).<br>2. Ketentuan pemesanan minimal H-2 atau H-3.<br>3. Peta embed simpel / petunjuk arah ke lokasi Gambut. |

---

## 5. Detail Spesifikasi Motion Galeri

| No | Komponen Motion | Perilaku & Spesifikasi Teknis | Durasi & Easing | Fallback (Mobile / Reduced Motion) |
| :--- | :--- | :--- | :--- | :--- |
| **1** | **Fade-up + Stagger** | Elemen kartu foto muncul bergantian saat discroll ke viewport. Stagger delay 50ms antar kartu bersebelahan. | Durasi: 350ms<br>Easing: `cubic-bezier(0.16, 1, 0.3, 1)` | Pada `prefers-reduced-motion`: instan muncul (opacity: 1) tanpa translate posisi. |
| **2** | **Masonry Grid Flow** | Penataan kolom seimbang otomatis berbasis rasio aspek asli foto (vertikal / square). | CSS `columns: 2` (Mobile) / `columns: 3` (Desktop) atau CSS Grid auto-fill | Tata letak statis 2 kolom tanpa layout shift saat foto selesai dimuat. |
| **3** | **Hover Zoom & Overlay** | Desktop: Kursor diarahkan ke kartu -> foto zoom 1.04x dan overlay gradient gelap + teks nama & harga muncul. | Durasi: 250ms<br>Easing: `ease-out` | Mobile: Teks nama dan harga selalu tampil semi-permanen di strip bawah kartu foto (tanpa perlu hover). |
| **4** | **Lightbox Shared Element** | Modal terbuka seolah-olah kartu foto meregang membesar memenuhi layar (FLIP / Framer Motion `layoutId`). | Durasi: 300ms<br>Easing: `cubic-bezier(0.2, 0.8, 0.2, 1)` | Fallback HP low-end: Modal fade-in biasa 150ms tanpa interpolasi geometri ukuran. |
| **5** | **Filter Beranimasi** | Kartu yang tidak sesuai kategori menghilang (scale down & fade out), kartu tersisa bergeser mulus mengisi ruang kosong. | Durasi: 300ms<br>Easing: `easeInOut` | Pada `prefers-reduced-motion`: Hide/show langsung via CSS `display: none` / `block`. |
| **6** | **Blur-up Image Loader** | Saat foto dimuat, tampilkan canvas/SVG blur resolusi ultra-rendah (10px) lalu bertransisi ke foto tajam. | Durasi: 400ms crossfade | Fallback: Background netral abu-abu pastel (`#F3EFEA`) sebelum foto selesai di-decode. |

---

## 6. Alur & Template Integrasi WhatsApp

### 6.1 Flow Diagram Logika Pemesanan
```
[User di Lightbox Kue] 
       │
       ▼
[Klik Tombol "Pesan Desain Ini via WA"]
       │
       ▼
[Script encode URI query string]
       │
       ▼
[Buka wa.me/+628XXXXXXXXXX?text=...]
       │
       ▼
[Chat WA aydin's Kitchen terbuka dengan data pesanan lengkap]
```

### 6.2 Format Pesan Otomatis (URL-Encoded)
Setiap tombol pemesanan menghasilkan pesan dengan format terstandarisasi:

```text
Halo Kak Winda (aydin's Kitchen), saya mau pesan kue dengan referensi berikut:

🎂 Nama Desain: [Nama Kue, contoh: Brownies Korean Minimalist]
🏷️ Kategori: [Contoh: Brownies Ultah]
💰 Estimasi Harga: [Contoh: Rp 165.000]
🔗 Link Foto: [https://aydinskitchen.com/#cake-04]

--- Form Pemesanan ---
• Tanggal Diperlukan: [Isi tanggal]
• Metode: [Ambil Sendiri di Gambut / Diantar ke Gambut atau Banjarmasin]
• Tulisan di Kue / Lilin: [Isi jika ada]

Apakah slot tanggal tersebut masih tersedia, Kak?
```

---

## 7. Non-Functional Requirements (NFR)

### 7.1 Performa & Optimasi Aset
- **LCP (Largest Contentful Paint)**: < 1.8 detik pada jaringan 4G seluler.
- **Ukuran File Foto**: Maksimal 80–120 KB per foto setelah kompresi CDN.
- **Format Gambar**: Otomatis menyajikan format AVIF (didukung Chrome/Safari modern) dengan fallback WebP.
- **Lazy Loading**: Gunakan `loading="lazy"` native browser dan `decoding="async"` untuk seluruh foto di bawah fold hero.

### 7.2 SEO Lokal (Gambut & Banjarmasin)
- **Target Kata Kunci**: "kue ulang tahun brownies banjarmasin", "cake brownies ultah gambut", "toko kue gambut".
- **Structured Data (Schema.org)**: Format JSON-LD tipe `Bakery` / `LocalBusiness` lengkap dengan area layanan (`areaServed: ["Gambut", "Banjarmasin"]`), koordinat, dan tautan kontak WA.
- **OpenGraph & Twitter Cards**: Gambar thumbnail 1200x630px menarik saat tautan website dibagikan di WhatsApp/Instagram Story.

### 7.3 Aksesibilitas (a11y) & Mobile-First
- Rasio kontras teks minimal 4.5:1 (WCAG AA).
- Seluruh foto memiliki atribut `alt` deskriptif (misal: "Kue ulang tahun brownies siram coklat lumer dengan hiasan stroberi").
- Navigasi modal lightbox dapat diakses keyboard (tombol `Tab`, `Escape`, `ArrowLeft`, `ArrowRight`).
- Target sentuh (touch target) tombol minimal 44x44px untuk kenyamanan jari di smartphone.

---

## 8. Rekomendasi Tech Stack & Solusi Update Katalog

### 8.1 Arsitektur Stack (Biaya Rp 0 / Murah, Ringan, 1 Orang Mahasiswa)

| Lapisan | Teknologi | Alasan Pemilihan |
| :--- | :--- | :--- |
| **Frontend Framework** | **Astro** (atau Next.js SSG) + **Tailwind CSS** | Astro menghasilkan HTML statis murni tanpa bloat JS, sangat kencang di HP lemot, hemat kuota hosting. |
| **Animasi & Motion** | **Framer Motion** (atau Motion One) | Solusi standar industri untuk shared-element transition (`layoutId`) dan masonry layout FLIP. |
| **Hosting & CI/CD** | **Vercel** atau **Netlify (Hobby Tier)** | 100% Gratis selamanya, otomatis rebuild saat data produk berubah, SSL gratis. Biaya hanya domain (`.com` ~Rp 150rb/thn). |
| **Image CDN** | **Cloudinary (Free Tier)** | Jatah 25 GB bandwidth/bln. Otomatis convert format (`f_auto`), kompres ukuran (`q_auto`), dan crop rasio aspek. |

### 8.2 Cara Kak Winda Update Foto & Produk Tanpa Koding
**Metode: Google Sheets + Deploy Hook (Paling Mudah & Zero-Cost)**
1. **Input Data**: Kak Winda cukup membuka Google Sheets dari HP/laptop.
2. Kolom sheet: `ID`, `Nama_Kue`, `Kategori`, `Estimasi_Harga`, `Deskripsi_Singkat`, `URL_Foto_Drive_atau_Cloudinary`, `Tampilkan_di_Web (TRUE/FALSE)`.
3. **Sinkronisasi**: Website membaca Google Sheets via Google Sheets API (atau diekspor sebagai CSV public).
4. **Trigger Build**: Menggunakan ekstensi Google Sheets sederhana atau tombol "Update Web" via Google Form yang menembak Deploy Hook Vercel/Netlify. Website ter-update dalam 45 detik.

---

## 9. Rencana Konten & Panduan Foto Produk

### 9.1 Skema Struktur Data Produk (JSON)
```json
{
  "id": "cake-01",
  "name": "Fudge Brownie Birthday Deluxe",
  "category": "Brownies Ultah",
  "priceStartingAt": 175000,
  "description": "Kue ulang tahun dengan base full fudgy brownies panggang premium, dilapisi dark chocolate ganache dan topping buah segar.",
  "dimensions": "Diameter 16 cm / 20 cm",
  "leadTime": "H-2",
  "imageUrl": "https://res.cloudinary.com/aydins/image/upload/v1/cakes/brownie-deluxe.jpg",
  "aspectRatio": "4:5",
  "featured": true
}
```

### 9.2 Panduan Pengambilan Foto untuk Kak Winda (SOP Rumahan)
1. **Pencahayaan**: Foto di dekat jendela antara jam 09.00 - 11.00 atau 15.00 - 16.30 (cahaya alami matahari tidak langsung). Jangan pakai flash HP.
2. **Latar Belakang (Background)**: Gunakan alas foto polos (papan kayu putih/cream, kain serbet bersih, atau kertas karton dove). Singkirkan barang dapur yang berserakan.
3. **Sudut Pengambilan (Angle)**:
   - *Sudut 45 Derajat*: Untuk memperlihatkan dekorasi atas dan ketebalan kue.
   - *Close-up Tekstur*: Perlihatkan shiny crust dan lumeran coklat brownies untuk menggugah selera.
4. **Kebersihan Lensa**: Selalu lap kaca kamera HP sebelum memotret.
5. **Kompresi**: Foto diunggah ke Google Drive/folder khusus, skrip build Cloudinary akan otomatis mengecilkan file ke format WebP 100KB.

---

## 10. Scope: MVP vs v2 vs Out-of-Scope

```
+------------------------------------------------------------------------+
| MVP (Fase 1 - Launching)                                               |
| - Katalog 30-50 foto responsif masonry                                |
| - Filter kategori instan (Brownies Ultah, Bento, dll)                  |
| - Lightbox shared-element dengan detail harga & spek                   |
| - Generator template WhatsApp otomatis                                 |
| - Update data via Google Sheets                                        |
| - Info pengiriman jelas area Gambut & Banjarmasin                     |
+------------------------------------------------------------------------+
                                  │
                                  ▼
+------------------------------------------------------------------------+
| v2 (Fase Pengembangan Lanjutan)                                        |
| - Custom Cake Configurator sederhana (pilih ukuran, tulisan, lilin)   |
| - Kalender indikator ketersediaan slot kuota order per hari            |
| - Ulasan & galeri testimoni pembeli yang terhubung ke Instagram        |
+------------------------------------------------------------------------+
                                  │
                                  ▼
+------------------------------------------------------------------------+
| TIDAK DIKERJAKAN (Sengaja Dihindari untuk Menjaga Fokus UMKM)          |
| - Payment Gateway (Midtrans/Xendit) -> Menghindari biaya admin & fee   |
| - Akun / Login Pembeli -> Memperpanjang alur pemesanan                 |
| - Keranjang Belanja Multi-item -> Karakteristik kue ultah dibeli per unit|
| - Hitung ongkir API ojek online otomatis -> Cukup kesepakatan via WA  |
+------------------------------------------------------------------------+
```

---

## 11. Timeline Pengerjaan (3 Minggu – 1 Developer Mahasiswa)

| Minggu / Fase | Fokus Pengerjaan | Target Deliverables |
| :--- | :--- | :--- |
| **Minggu 1 (Fase Setup & Fondasi)** | Setup project Astro + Tailwind, konfigurasi Google Sheets API & pipeline Cloudinary, finalisasi kurasi 30-50 foto awal. | Website kerangka statis jalan di lokal, data foto sukses terbaca dari spreadsheet. |
| **Minggu 2 (Fase UI & Motion Galeri)** | Slicing masonry layout, integrasi Framer Motion (fade-up, filter reorder, lightbox shared-element, blur-up). | Galeri interaktif berfungsi mulus di desktop & HP, performa 60 FPS. |
| **Minggu 3 (Fase Integrasi, QA & Rilis)** | Tombol pesan WA otomatis, info pengiriman Gambut/Banjarmasin, audit Lighthouse & SEO lokal, handover tutorial Sheets ke Kak Winda. | Deploy live ke Vercel dengan domain custom, serah terima ke pemilik toko. |

---

## 12. Manajemen Risiko & Rencana Mitigasi

| Risiko Potensial | Dampak | Rencana Mitigasi |
| :--- | :--- | :--- |
| **1. Foto mentah terlalu besar membuat web lemot** | Tinggi | Gunakan Cloudinary URL parameter `f_auto,q_auto,w_800` agar gambar otomatis dikompresi di awan sebelum diunduh pengunjung. |
| **2. Animasi lag di HP Android spek terjangkau** | Sedang | Manfaatkan CSS Hardware Acceleration (`will-change: transform`), matikan motion berat pada layar dengan lebar < 640px, sediakan query `prefers-reduced-motion`. |
| **3. Kak Winda salah ubah format di Google Sheets** | Sedang | Pasang "Data Validation" (dropdown) di Google Sheets dan siapkan nilai default (fallback) di kode jika ada cell kosong. |
| **4. Salah paham jangkauan kurir kue** | Sedang | Beri label tegas di navbar dan modal produk: *"Khusus Pengiriman Wilayah Gambut & Banjarmasin (Pick-up / Kurir Lokal)"*. |
| **5. Kuota free-tier Cloudinary / Vercel terlampaui** | Rendah | Untuk katalog 50 foto dan trafik 5.000 visitor/bulan, bandwidth yang terpakai hanya sekitar 3–5 GB (kuota gratis Cloudinary 25 GB/bulan). |
