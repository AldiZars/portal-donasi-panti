# Portal Donasi Panti Asuhan

Donasi online dengan laporan dana yang transparan.

**Live Demo:** https://portal-donasi-panti.vercel.app

## Fitur
- Prompt nama donatur saat halaman dibuka (default: Hamba Allah)
- Form donasi: Nama Donatur + Nominal Donasi + tombol Kirim Donasi
- Validasi nominal minimal Rp 10.000 (tolak submit + alert)
- Tabel Laporan Dana September (Tanggal, Rincian, Nominal)
- Layout `.wadah { display: flex; gap: 24px }`

## Struktur
```
PRD.md
donasi-panti.html
index.html
style.css
vercel.json
```

## Cara Jalankan
Buka `donasi-panti.html` di browser, atau serve lokal:
```bash
python3 -m http.server 8000
```
