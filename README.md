# yasaglobal-website

Website company profile PT Yasa Global Internasional (https://yasaglobal.id).

## Struktur
- `site/index.html` — halaman website (satu file, tanpa build step)
- `Caddyfile` — web server + HTTPS otomatis, redirect `www` ke domain utama
- `Dockerfile`, `docker-compose.yml` — paket untuk dijalankan di VPS

## Alur perubahan
1. Edit `site/index.html`
2. Commit dan push ke `main`
3. Deploy ulang proyek Docker di VPS

## Status deploy
Saat ini website dilayani oleh Nginx langsung di VPS (di luar Docker).
Paket Docker di repo ini belum dijalankan; port 80/443 masih dipakai Nginx.
Migrasi ke Docker perlu menghentikan Nginx terlebih dahulu.

## Catatan
- Jangan simpan password, token, atau API key di repo ini.
- Rencana: `app.yasaglobal.id` (web app) dan `staging.yasaglobal.id` ditambahkan kemudian.
