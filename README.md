# yasaglobal-website

Website company profile PT Yasa Global Internasional — https://yasaglobal.id

Satu halaman statis (`site/index.html`), tanpa build step.

## Struktur
- `site/index.html` — halaman website. Semua isi folder `site/` ikut terdeploy.
- `deploy/nginx-yasaglobal.conf` — konfigurasi dasar Nginx (dokumentasi)
- `deploy/autodeploy/docker-compose.yml` — deploy otomatis dari GitHub ke server

## Alur mengubah website
1. Edit `site/index.html` (atau minta Claude mengeditnya).
2. Commit dan push ke branch `main`.
3. Dalam sekitar 1 menit server mengambil perubahan dan website ter-update otomatis.

Tidak ada langkah `scp` atau login ke server.

## Cara kerja deploy otomatis
Sebuah container kecil di server (`yasaglobal-autodeploy`) mengecek branch `main`
tiap 60 detik. Kalau ada commit baru, isi folder `site/` disalin ke webroot Nginx.

Pengaman:
- Kalau `site/index.html` kosong atau hilang, deploy dilewati dan website lama tetap tayang.
- Tidak butuh SSH key atau secret; repo harus publik.
- Karena repo publik, **jangan pernah menaruh password, token, atau API key di repo ini.**

## Membatalkan perubahan (rollback)
```bash
git revert <commit>
git push origin main
```
Website kembali ke versi sebelumnya dalam sekitar 1 menit.

## Rencana
- Email `cs@yasaglobal.id`
- Web app dengan login dan database di subdomain `app.`
- Subdomain `staging.` untuk uji coba sebelum rilis
