# yasaglobal-website

Website company profile PT Yasa Global Internasional — https://yasaglobal.id

Satu halaman statis (`site/index.html`), tanpa build step.

## Struktur
- `site/index.html` — halaman website
- `deploy/nginx-yasaglobal.conf` — konfigurasi dasar Nginx (dokumentasi)

## Infrastruktur
| Item | Nilai |
|---|---|
| VPS | Hostinger KVM 2, Ubuntu 26.04 LTS (srv2137916.hstgr.cloud) |
| Web server | Nginx, file di `/var/www/yasaglobal/` |
| HTTPS | Let's Encrypt via Certbot, perpanjangan otomatis |
| DNS | Hostinger (record A: `@`, `www`, `app`, `staging` -> IP VPS) |
| Firewall (Hostinger) | `web-server-basic`: hanya port 22, 80, 443 terbuka |
| Docker | Proyek `yims` (PostgreSQL 16 + Redis 7), tidak dipublikasikan ke luar |

## Mengubah isi website
1. Edit `site/index.html`, commit, push ke `main`.
2. Salin ke server:
   ```bash
   scp site/index.html root@IP_VPS:/var/www/yasaglobal/index.html
   ```

## Aturan
- Jangan menyimpan password, token, atau API key di repo ini.
- Port baru (misalnya untuk web app) harus ditambahkan dulu ke firewall Hostinger.

## Rencana
- Deploy otomatis dari GitHub (butuh SSH key khusus deploy sebagai GitHub secret).
- `app.yasaglobal.id` untuk web app dengan login dan database, `staging.` untuk uji coba.
- Email `cs@yasaglobal.id` (menunggu pilihan penyedia: Zoho gratis atau Hostinger).
