# http-to-https-Nextcloud

# 🌐 Nextcloud Local Server Hardening & HTTPS Setup

Dokumentasi repositori ini berisi langkah-langkah *troubleshooting* dan konfigurasi untuk mengubah protokol **Nextcloud (Snap Version)** dari HTTP biasa menjadi HTTPS menggunakan *Self-Signed Certificate* pada Ubuntu Server lokal (`fufufafa`).

---

## 🛠️ Topologi & Detail Lab
* **OS Server:** Ubuntu Server (Host IP: `192.168.1.13`)
* **OS Client:** Kali Linux
* **Aplikasi:** Nextcloud (Installed via Snap)
* **Firewall:** UFW (Uncomplicated Firewall)

---

## 🚨 Kronologi Masalah (Troubleshooting Log)
1. **Port Conflict:** Terjadi bentrok pada port `80` antara Nginx Reverse Proxy dengan web server bawaan Nextcloud Snap.
2. **Infinite Redirect Loop:** Muncul pesan error *"The page isn't redirecting properly"* pada browser akibat miskonfigurasi pengalihan (*redirection*) antara Nginx dan aturan internal Nextcloud.
3. **Solusi Akhir:** Menonaktifkan layanan Nginx luar dan memanfaatkan modul SSL otomatis bawaan dari Nextcloud Snap agar sistem lebih stabil dan hemat konsumsi RAM.

---

## 🚀 Langkah-Langkah Konfigurasi (Step-by-Step)

### 1. Pembersihan Sisa Port & Service Nginx
Hentikan dan matikan layanan Nginx agar port `80` dan `443` bersih dari proses latar belakang:
```bash
sudo systemctl stop nginx
sudo systemctl disable nginx
sudo pkill -f nginx
