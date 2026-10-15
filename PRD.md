# PRODUCT REQUIREMENTS DOCUMENT (PRD)

## Portal Donasi Panti Asuhan — Donasi Online dengan Laporan Dana yang Transparan

**STATUS: DISETUJUI (APPROVED)**

| | |
| --- | --- |
| **Nama Produk** | Portal Donasi Panti Asuhan — Donasi Online dengan Laporan Dana yang Transparan |
| **Versi Dokumen** | v1.0 (Final Approved) |
| **Disusun oleh** | Tim Pengembang Web |
| **Untuk** | Portal Donasi Panti Asuhan / Klien |
| **Tanggal** | 13 Oktober 2026 |
| **Dokumen Terkait** | Wireframe `donasi-panti.html` (1 gambar mockup browser) dan Kartu Spesifikasi Teknis HTML/CSS/JS (1 gambar) |

---

# 1. Ringkasan Produk (Overview)

Penggalangan donasi panti asuhan sering terkendala kepercayaan: donatur tidak tahu siapa yang mencatat donasinya dan untuk apa dana bulan lalu digunakan. Tanpa sapaan nama yang personal dan tanpa laporan penggunaan dana yang terbuka di halaman yang sama, donatur ragu untuk mengirim donasi online.

Solusi yang dibangun adalah website satu halaman statis `donasi-panti.html` berbasis HTML5 dan CSS3 dengan interaktivitas JavaScript vanilla murni. Sistem terdiri dari dua modul utama: (1) Form Donasi di kolom kiri sebagai jalur input, dan (2) Tabel Laporan Dana · September di kolom kanan sebagai bukti transparansi akuntabilitas keuangan. Cakupan siklus yang ditangani adalah prompt nama saat halaman pertama dibuka → nama terisi otomatis ke form (default `Hamba Allah` jika dikosongkan/dibatalkan) → input nominal donasi → validasi minimal Rp 10.000 → tolak submit dengan `alert()` dan indikator merah jika kurang dari batas minimal, atau terima submit dengan konfirmasi jika memenuhi syarat, seluruhnya tanpa refresh halaman.

# 2. Tujuan & Sasaran (Goals)

- Menyapa donatur secara personal sejak halaman pertama dibuka melalui `prompt()` nama dengan fallback `Hamba Allah`.
- Memudahkan donatur mengirim donasi melalui satu form sederhana (Nama Donatur + Nominal Donasi + tombol Kirim Donasi).
- Menegakkan batas donasi minimal Rp 10.000 secara konsisten dengan penolakan submit dan notifikasi yang jelas.
- Menyediakan laporan penggunaan dana bulan lalu yang transparan (Tanggal · Rincian · Nominal) di halaman yang sama.
- Menyusun form dan tabel bersebelahan secara mendatar menggunakan `.wadah { display: flex; gap: 24px; }` dengan jarak lega agar alur donasi dan verifikasi laporan terbaca dalam satu pandang.

# 3. Pengguna & Peran (Users & Roles)

- **Pengunjung / Donatur Umum :** satu-satunya peran. Dapat mengisi prompt nama saat halaman dibuka, melihat/mengubah Nama Donatur dan Nominal Donasi pada form, menekan tombol Kirim Donasi, melihat pesan validasi dan dialog peringatan, serta membaca tabel Laporan Dana. Tidak ada login, tidak ada hak khusus.

# 4. Ruang Lingkup (Scope)

## 4.1 Termasuk (MVP)

- Dialog `prompt()` saat halaman pertama dibuka dengan teks persis `Masukkan nama donatur (kosongkan jika Hamba Allah)` dan tombol Batal / OK.
- Aturan fallback: jika prompt dikosongkan atau dibatalkan, nama = `Hamba Allah`.
- Form Donasi (`<form>`) dengan field Nama Donatur (terisi otomatis dari prompt), field Nominal Donasi, teks indikator validasi `Minimal Rp 10.000`, dan tombol `Kirim Donasi`.
- Validasi ambang minimal Rp 10.000 dengan dua skenario (< Rp 10.000 dan ≥ Rp 10.000).
- Penolakan submit (`event.preventDefault()`) + `alert()` jika Nominal < 10.000.
- Indikator visual error: border merah pada input nominal dan teks merah `Minimal Rp 10.000`.
- Tabel Laporan Dana · September menggunakan `<table>`, `<thead>`, dan `<tbody>` dengan kolom Tanggal · Rincian · Nominal dan 3 baris tetap:
  1. `05 Sep` | `Sembako` | `Rp 2.000.000`
  2. `12 Sep` | `Pendidikan` | `Rp 1.500.000`
  3. `20 Sep` | `Kesehatan` | `Rp 1.000.000`
- Wadah pembungkus form dan tabel menggunakan kelas CSS `.wadah { display: flex; gap: 24px; }`.

## 4.2 Di Luar Lingkup Awal / Fase Lanjutan

- Integrasi gateway pembayaran payment processor (Midtrans / Xendit / QRIS dinamis).
- Otentikasi dan login donatur / admin panti asuhan.
- Basis data persisten di backend / cloud database.

# 5. Asumsi & Batasan (Assumptions & Constraints)

- Teknologi murni HTML5 dan CSS3 untuk struktur dan tampilan, ditambah JavaScript vanilla untuk logika tanpa ketergantungan library/framework luar.
- Berkas utama `donasi-panti.html` dan `style.css`, serta `index.html` sebagai mirror.
- Dialog awal memakai `prompt("Masukkan nama donatur (kosongkan jika Hamba Allah)")` yang muncul tepat saat halaman pertama selesai dimuat.
- Jika prompt bernilai string kosong `""` atau pengguna menekan Batal (`null`), nama fallback adalah `Hamba Allah`.
- Batas minimal donasi adalah Rp 10.000. Jika input di bawah Rp 10.000, submit form ditolak, input nominal bergaris tepi merah, dan muncul dialog `alert()`.
- Form memakai elemen semantic `<form>` dan tabel memakai `<table>`, `<thead>`, `<tbody>`.
- Wadah form dan tabel menggunakan selector `.wadah` dengan deklarasi `display: flex; gap: 24px;`.
- Tombol `Kirim Donasi` berlatar teal gelap, teks putih, berukuran penuh (full-width) di dalam card form.

# 6. Kebutuhan Fungsional (Functional Requirements)

## 6.1 Pengunjung — Prompt Nama Awal

| **ID** | **Kebutuhan Fungsional** | **Prioritas** |
| --- | --- | --- |
| **PRM-1** | Sistem memunculkan dialog `prompt("Masukkan nama donatur (kosongkan jika Hamba Allah)")` saat halaman pertama dibuka. | **Wajib** |
| **PRM-2** | Sistem menyediakan tombol Batal dan OK pada dialog prompt sesuai standar peramban. | **Wajib** |
| **PRM-3** | Sistem menetapkan `nama = "Hamba Allah"` jika prompt dikosongkan atau dibatalkan. | **Wajib** |
| **PRM-4** | Sistem mengisi elemen input Nama Donatur (`#nama-donatur`) secara otomatis dengan nilai nama tersebut. | **Wajib** |

## 6.2 Pengunjung — Form Donasi

| **ID** | **Kebutuhan Fungsional** | **Prioritas** |
| --- | --- | --- |
| **FRM-1** | Pengguna dapat melihat dan mengubah Nama Donatur pada form. | **Wajib** |
| **FRM-2** | Pengguna dapat menginputkan nominal donasi pada form (contoh `Rp 5.000` atau angka numerik). | **Wajib** |
| **FRM-3** | Sistem menampilkan teks validasi keterangan `Minimal Rp 10.000` di bawah field nominal. | **Wajib** |
| **FRM-4** | Pengguna dapat menekan tombol `Kirim Donasi` untuk memproses donasi. | **Wajib** |

## 6.3 Pengunjung — Validasi Nominal Minimal dan Hasil

| **ID** | **Kebutuhan Fungsional** | **Prioritas** |
| --- | --- | --- |
| **VLD-1** | Sistem menahan reload form saat disubmit (`event.preventDefault()`). | **Wajib** |
| **VLD-2** | Jika Nominal < 10.000, sistem menolak submit, memberi border merah pada field nominal, menampilkan warna merah pada teks `Minimal Rp 10.000`, dan memunculkan dialog `alert("Donasi gagal: Nominal donasi minimal Rp 10.000")`. | **Wajib** |
| **VLD-3** | Jika Nominal ≥ 10.000, sistem menghapus status error, menampilkan dialog `alert("Terima kasih, [Nama]! Donasi sejumlah [Nominal] berhasil dikirim.")`, dan mereset form. | **Wajib** |

## 6.4 Pengunjung — Tabel Laporan Dana

| **ID** | **Kebutuhan Fungsional** | **Prioritas** |
| --- | --- | --- |
| **LPR-1** | Sistem menampilkan tabel laporan penggunaan dana bulan lalu di samping form donasi. | **Wajib** |
| **LPR-2** | Sistem menyusun tabel dengan judul `Laporan Dana · September` dan kolom `Tanggal`, `Rincian`, `Nominal`. | **Wajib** |
| **LPR-3** | Sistem menyajikan 3 baris tetap: `05 Sep` (Sembako, Rp 2.000.000), `12 Sep` (Pendidikan, Rp 1.500.000), dan `20 Sep` (Kesehatan, Rp 1.000.000). | **Wajib** |
| **LPR-4** | Tabel wajib mengimplementasikan struktur semantic `<table>`, `<thead>`, dan `<tbody>`. | **Wajib** |

# 7. Alur Pengguna Utama (Key User Flows)

## 7.1 Skenario Awal — Halaman Pertama Dibuka (Prompt Nama)

1. Pengguna membuka halaman `donasi-panti.html`.
2. Browser menampilkan dialog `prompt("Masukkan nama donatur (kosongkan jika Hamba Allah)")`.
3. Pengguna menekan OK tanpa mengetik apa-apa (atau mengisi nama, misal "Budi", lalu OK).
4. Jika kosong/Batal, sistem menetapkan nilai `"Hamba Allah"`.
5. Field input `Nama Donatur` pada Form Donasi langsung terisi nilai tersebut.

## 7.2 Skenario Gagal — Nominal < Rp 10.000 (Tolak Submit)

1. Pengguna memasukkan nominal di bawah Rp 10.000 (misalnya `5000` atau `Rp 5.000`).
2. Pengguna menekan tombol `Kirim Donasi`.
3. Handler JavaScript membatalkan submit standar (`event.preventDefault()`).
4. Sistem memeriksa nilai nominal dan menemukan nominal < 10.000.
5. Sistem menambahkan kelas CSS error pada field nominal (border merah) dan menyorot teks `Minimal Rp 10.000` menjadi merah menyala.
6. Sistem memunculkan browser `alert()` yang menegaskan nominal minimal adalah Rp 10.000. Pengguna tetap berada pada halaman donasi.

## 7.3 Skenario Sukses — Nominal ≥ Rp 10.000

1. Pengguna memasukkan nominal Rp 10.000 atau lebih (misal `50000`).
2. Pengguna menekan tombol `Kirim Donasi`.
3. Sistem memvalidasi nominal ≥ 10.000.
4. Sistem menghapus kelas CSS error dan memunculkan notifikasi sukses `alert("Terima kasih, [Nama Donatur]! Donasi Anda sebesar [Nominal] telah kami terima.")`.

# 8. Model Data (High-Level)

| **Entitas** | **Field Utama** | **Keterangan** |
| --- | --- | --- |
| **Donasi** | nama_donatur, nominal | Data transien di memori browser. Default `nama_donatur` = `Hamba Allah`. Batas `nominal` minimal = 10000. |
| **LaporanDana** | tanggal, rincian, nominal | Data statis bulan September (05 Sep Sembako Rp 2.000.000, 12 Sep Pendidikan Rp 1.500.000, 20 Sep Kesehatan Rp 1.000.000). |

# 9. Kebutuhan Non-Fungsional (Non-Functional Requirements)

- **Ketepatan Visual & Arsitektur :** Sesuai 100% dengan wireframe `donasi-panti.html` dan kartu spesifikasi teknis.
- **Layout Bersebelahan :** Menggunakan kelas `.wadah` dengan aturan CSS `.wadah { display: flex; gap: 24px; }`.
- **Kompatibilitas :** Berjalan mulus di semua browser modern tanpa pustaka pihak ketiga.
- **Performa Instan :** Bobot file ultra-ringan, tidak memerlukan jaringan eksternal / CDN tambahan.

# 10. Glosarium

- **prompt() :** Fungsi modal dialog JavaScript bawaan untuk menerima teks dari pengguna.
- **Hamba Allah :** Nilai default donatur jika pengguna memilih anonim atau mengosongkan prompt.
- **wadah :** Kontainer flexbox pembungkus kartu Form Donasi dan Tabel Laporan Dana.
