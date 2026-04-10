# QC Inspection Web App

> **[ID]** Sistem Inspeksi Quality Control berbasis web — mobile-first, installable (PWA), barcode scanner, validasi real-time.
>
> **[EN]** Web-based Quality Control Inspection System — mobile-first, installable (PWA), barcode scanner, real-time validation.

**Live Demo:** [ird.svian.dev](https://ird.svian.dev)

---

## Screenshots

<p align="center">
  <img src="screenshots/login.png" width="200" alt="Login" />
  <img src="screenshots/dashboard.png" width="200" alt="Dashboard" />
  <img src="screenshots/std-create.png" width="200" alt="Create STD" />
</p>
<p align="center">
  <img src="screenshots/inspection.png" width="200" alt="Inspection" />
  <img src="screenshots/history.png" width="200" alt="History" />
  <img src="screenshots/export.png" width="200" alt="Export CSV" />
</p>

---

## Overview

**[ID]**
QC Inspection adalah aplikasi web untuk proses pengecekan kualitas produk di lini produksi. Didesain mobile-first agar bisa digunakan langsung di lapangan menggunakan smartphone, dengan fitur scan barcode untuk memuat checksheet otomatis. Mendukung instalasi sebagai PWA sehingga tampil layaknya aplikasi native.

**[EN]**
QC Inspection is a web application for product quality checking on the production line. Designed mobile-first for field use on smartphones, featuring barcode scanning to auto-load checksheets. Supports PWA installation for a native app-like experience.

---

## Features / Fitur

### Barcode Scanner
- **[ID]** Scan No IRD langsung dari kamera smartphone. Sistem otomatis memuat Standard (checksheet) yang sesuai. Tersedia juga input manual dan pemilihan dari daftar.
- **[EN]** Scan IRD number directly from smartphone camera. System auto-loads the matching Standard (checksheet). Manual input and list selection also available.

### 5 Pcs Measurement Input
- **[ID]** Setiap item mendukung hingga 5 pengukuran per sample. Range dan Average dihitung otomatis. Minimal 1 pcs wajib diisi.
- **[EN]** Each item supports up to 5 measurements per sample. Range and Average calculated automatically. Minimum 1 pcs required.

### Inspection Types / Tipe Pengecekan
- **Numeric** — Bilateral (`10 ±0.15 mm`), Min Only (`6.3 min`), Max Only (`50 max`)
- **Non-Numeric** — Visual check with OK/NG per sample (5 pcs)

### Real-Time Validation / Validasi Real-Time
- **[ID]** Setiap nilai langsung divalidasi: OK (hijau), NG (merah + suara + vibrasi).
- **[EN]** Every value instantly validated: OK (green), NG (red + sound alert + vibration).

### Drawing Illustration / Ilustrasi Drawing
- **[ID]** Gambar drawing sticky di atas layar saat input nilai. Nomor item sesuai gambar.
- **[EN]** Drawing image sticks to top of screen during input. Item numbers match the drawing.

### Auto-Save Draft
- **[ID]** Inspeksi tersimpan otomatis. Berpindah halaman lalu kembali — langsung lanjut dari posisi terakhir.
- **[EN]** Inspection auto-saved. Switch pages and come back — resume from where you left off.

### History & Export / Riwayat & Export
- **[ID]** Riwayat inspeksi dengan filter dan search. Export ke CSV (Excel) dengan filter tanggal, zona waktu WIB.
- **[EN]** Inspection history with filters and search. Export to CSV (Excel) with date range filter, WIB timezone.

### Installable (PWA)
- **Android:** Chrome > Menu > Add to Home Screen
- **iOS:** Safari > Share > Add to Home Screen

---

## Role-Based Access / Hak Akses

| Feature / Fitur               | Admin | Engineer | Operator | Viewer |
|-------------------------------|:-----:|:--------:|:--------:|:------:|
| Create / Edit / Delete STD    | V     | V        | -        | -      |
| Upload Drawing                | V     | V        | -        | -      |
| Perform Inspection            | V     | V        | V        | -      |
| View All History              | V     | V        | -        | V      |
| View Own History              | V     | V        | V        | V      |
| Export CSV                    | V     | V        | V        | V      |
| Manage Users                  | V     | -        | -        | -      |

---

## Tech Stack

| Layer      | Technology                              |
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

## Data Model

```
User             — User management with 4 roles (Admin/Engineer/Operator/Viewer)
Std              — Standard / Checksheet (Customer, Part Name, Part No, Spec/Dimension)
StdItem          — Check items per STD (Numeric / Non-Numeric, tolerance, inspection tool)
Inspection       — Inspection result (IRD No, Batch No, overall status)
InspectionResult — Per-item detail (5 measurements, Range, Average, OK/NG status)
```

---

## User Flow / Alur Penggunaan

### 1. Setup Checksheet (Admin / Engineer)
- **[ID]** Buat Standard: isi Customer, Part Name, Part No, Spec/Dimension. Tambah item pengecekan (numerik dengan toleransi, atau visual check). Upload gambar drawing.
- **[EN]** Create Standard: fill in Customer, Part Name, Part No, Spec/Dimension. Add check items (numeric with tolerance, or visual check). Upload drawing image.

### 2. Inspection / Inspeksi (Operator)
- **[ID]** Scan barcode atau pilih STD dari daftar. Isi No Batch, input nilai per item. Validasi otomatis OK/NG. Simpan.
- **[EN]** Scan barcode or select STD from list. Fill Batch No, input values per item. Auto-validation OK/NG. Save.

### 3. Monitoring (Viewer / Admin)
- **[ID]** Pantau riwayat inspeksi, filter status, search, lihat detail, export CSV.
- **[EN]** Monitor inspection history, filter by status, search, view details, export CSV.

---

## Deployment

- **Platform:** Vercel
- **Database:** Neon PostgreSQL (Vercel integration)
- **Storage:** Vercel Blob (illustration images)
- **PWA:** Service Worker auto-generated at build time

---

## Contact / Kontak

Developed by **Septa Viandra**

- GitHub: [github.com/septaviandra](https://github.com/septaviandra)
- Live Demo: [ird.svian.dev](https://ird.svian.dev)
