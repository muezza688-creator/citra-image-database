# Database Gambar Chatbot Citra

Katalog Citra Bukit Etam berisi **64 aset**: 2 foto aktual, 27 halaman desain eksterior, dan 35 halaman desain interior. Sampul, daftar isi dan penutup yang tidak diperlukan dikeluarkan. Gambar berasal dari lampiran pengguna; tidak ada gambar AI tambahan.

## Isi

- `public/data/catalog.json`: metadata lengkap, kategori, kata kunci, sumber halaman, ukuran dan hash gambar.
- `public/api/images.json`: salinan katalog statis untuk integrasi sederhana.
- `public/images/`: 64 gambar JPEG.
- `public/thumbnails/`: pratinjau untuk galeri.
- `netlify/functions/images.mjs`: pencarian dengan filter dan pagination.
- `katalog-gambar.csv`: indeks untuk pengelolaan manual.

## Netlify

Jika isi folder ini dijadikan repositori langsung, Netlify membaca `netlify.toml`: publish `public`, Functions `netlify/functions`. Tidak memerlukan kunci API atau layanan database tambahan.

Jika repositori berisi `citra-bundle.zip`, konfigurasi di akar repositori akan mengekstraknya ke `site` saat build; publish `site/public` dan Functions `site/netlify/functions`.

Unggah folder `public` saja melalui Netlify Drop untuk galeri, gambar dan JSON statis. Pencarian `/api/images` memerlukan deploy melalui Git/build atau CLI yang menyertakan Functions.

## Integrasi chatbot

Lihat `public/panduan-chatbot.md`. Endpoint setelah deploy:

```text
GET /data/catalog.json
GET /api/images?q=malam&kind=photo_actual&limit=2
GET /api/images?room=kamar-anak&kind=design_render
GET /api/images?category=denah&limit=6&page=1
```

Katalog memakai `image_path` relatif terhadap akar situs. API pencarian mengembalikan `image_url` absolut. Setiap hasil mencantumkan label foto aktual/desain dan sumber halaman PDF.

Interior Mr Ismail adalah referensi desain. Jangan menganggap furnitur, material, dimensi dokumen, harga, ketersediaan unit atau isi paket penjualan berlaku untuk semua unit. Tanggal pemotretan kedua foto belum dikonfirmasi.

## Verifikasi lokal

Node.js 22 atau lebih baru, tanpa instalasi dependensi:

```text
npm run check
npm run preview
```

Buka `http://localhost:4173` untuk galeri dan contoh API. Pratinjau lokal menyimulasikan handler; deploy Netlify tetap perlu diverifikasi setelah publikasi.

Konfigurasi mengikuti [dokumentasi Netlify Functions](https://docs.netlify.com/build/functions/get-started/) dan [konfigurasi berbasis berkas](https://docs.netlify.com/build/configure-builds/file-based-configuration/).

Hak gambar dan desain mengikuti pemilik sumber masing-masing. Kredit Diary Design Studio dipertahankan untuk dokumen interior.
