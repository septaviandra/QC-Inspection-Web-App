# QC Inspection App

> Sistem Inspeksi Quality Control berbasis web — mobile-first, installable (PWA), barcode scanner, validasi real-time.

**Live Demo:** [ird.svian.dev](https://ird.svian.dev)

---

## Overview

QC Inspection adalah aplikasi web untuk proses pengecekan kualitas produk di lini produksi. Didesain mobile-first agar bisa digunakan langsung di lapangan menggunakan smartphone, dengan fitur scan barcode untuk memuat checksheet otomatis.

Aplikasi ini mendukung instalasi sebagai PWA (Progressive Web App) sehingga bisa diakses dari home screen Android/iOS layaknya aplikasi native.

---

## Fitur Utama

### Scan Barcode / QR Code
Scan No IRD langsung dari kamera smartphone. Sistem otomatis memuat Standard (checksheet) yang sesuai. Tersedia juga opsi input manual dan pemilihan dari daftar STD.

### Input Inspeksi 5 Pcs
Setiap item pengecekan mendukung hingga 5 pengukuran per sample. Range (max-min) dan Average dihitung otomatis. Minimal 1 pcs wajib diisi — fleksibel sesuai kebutuhan produksi.

### Tipe Pengecekan
- **Numerik** — Input angka dengan toleransi. Mendukung 3 tipe spec:
  - Bilateral (`10 ±0.15 mm`)
  - Min Only (`6.3 min`)
  - Max Only (`50 max`)
- **Non-Numerik** — Pengecekan visual dengan pilihan OK/NG per sample (5 pcs)

### Validasi Real-Time
Setiap nilai yang diinput langsung divalidasi terhadap spec:
- **OK** — border hijau
- **NG** — border merah + suara alert + vibrasi

### Ilustrasi Drawing
Upload gambar drawing/blueprint yang ditampilkan sticky di bagian atas layar saat operator mengisi nilai. Nomor item di form sesuai dengan nomor di gambar.

### Draft Otomatis
Inspeksi yang belum selesai tersimpan otomatis. Jika operator berpindah halaman lalu kembali, inspeksi dilanjutkan dari posisi terakhir.

### Riwayat & Export
- Riwayat inspeksi dengan filter status (OK/NG) dan search
- Detail hasil per item lengkap dengan pengukuran P1-P5
- Export ke CSV (Excel-compatible) dengan filter tanggal — waktu menggunakan zona WIB

### Multi-Role Access Control

| Fitur                         | Admin | Engineer | Operator | Viewer |
|-------------------------------|:-----:|:--------:|:--------:|:------:|
| Buat / Edit / Hapus STD       | V     | V        | -        | -      |
| Upload Ilustrasi Drawing      | V     | V        | -        | -      |
| Lakukan Inspeksi              | V     | V        | V        | -      |
| Lihat Semua Riwayat           | V     | V        | -        | V      |
| Lihat Riwayat Sendiri         | V     | V        | V        | V      |
| Export CSV                    | V     | V        | V        | V      |
| Kelola Pengguna               | V     | -        | -        | -      |

### Installable (PWA)
Bisa diinstall di **Android** (Chrome > Tambahkan ke layar utama) dan **iOS** (Safari > Add to Home Screen). Tampil layaknya aplikasi native tanpa address bar.

---

## Tech Stack

| Layer      | Teknologi                               |
|------------|-----------------------------------------|
| Framework  | Next.js 16 (App Router)                 |
| Database   | PostgreSQL (Neon, via Vercel)            |
| ORM        | Prisma                                  |
| Auth       | NextAuth.js v4 (JWT)                    |
| Storage    | Vercel Blob                             |
| PWA        | @ducanh2912/next-pwa + Workbox          |
| UI         | Tailwind CSS                            |
| Barcode    | html5-qrcode                            |
| Deploy     | Vercel                                  |

---

## Database Schema

```
User             — Manajemen pengguna dengan 4 role (Admin/Engineer/Operator/Viewer)
Std              — Standard / Checksheet (Customer, Part Name, Part No, Spec/Dimension)
StdItem          — Item pengecekan per STD (Numerik / Non-Numerik, toleransi, inspection tool)
Inspection       — Hasil inspeksi (No IRD, No Batch, status keseluruhan)
InspectionResult — Detail per item (5 pengukuran, Range, Average, status OK/NG)
```

---

## Alur Penggunaan

### 1. Setup Checksheet (Admin / Engineer)
Buat Standard dengan informasi Customer, Part Name, Part No, dan Spec/Dimension. Tambahkan item pengecekan — bisa numerik (dengan toleransi) atau non-numerik (visual check). Upload gambar drawing sebagai referensi.

### 2. Inspeksi (Operator)
Scan barcode atau pilih STD dari daftar. Isi No Batch, lalu input nilai pengukuran per item. Sistem langsung menampilkan status OK/NG dengan feedback visual dan audio. Simpan saat selesai.

### 3. Monitoring (Viewer / Admin)
Pantau hasil inspeksi dari menu Riwayat. Filter berdasarkan status atau cari berdasarkan No IRD / No Batch. Export data ke CSV untuk analisis lebih lanjut.

---

## Deployment

Aplikasi di-deploy di **Vercel** dengan:
- **Neon PostgreSQL** sebagai database (via Vercel Postgres integration)
- **Vercel Blob** untuk penyimpanan gambar ilustrasi
- **PWA Service Worker** di-generate otomatis saat build

---

## Kontak

Dikembangkan oleh **Septa Viandra**

- GitHub: [github.com/septaviandra](https://github.com/septaviandra)
- Live: [ird.svian.dev](https://ird.svian.dev)
