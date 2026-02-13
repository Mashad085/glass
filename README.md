# Glass ISC DHCP - Web Interface

Modern web interface untuk manajemen dan monitoring server ISC DHCP.

> **Note**: Proyek ini merupakan modifikasi dan pengembangan lebih lanjut dari [Akkadius/glass-isc-dhcp](https://github.com/Akkadius/glass-isc-dhcp) dengan berbagai perbaikan dan penyesuaian.

## ✨ Fitur Utama

- ✅ **Dashboard Real-time** - Monitor status server DHCP secara live
- ✅ **Manajemen Lease** - Lihat, cari, dan kelola lease DHCP dengan mudah
- ✅ **Konfigurasi Visual** - Interface grafis untuk konfigurasi DHCP
- ✅ **Log Monitoring** - Pantau log server DHCP secara real-time
- ✅ **Responsive Design** - Akses dari desktop maupun perangkat mobile
- ✅ **Multi-server Support** - Kelola beberapa server DHCP sekaligus

## 📋 Prasyarat

- Ubuntu/Debian Linux
- Server ISC DHCP yang berjalan
- Node.js (versi LTS direkomendasikan)
- Hak akses root/administrator

## 🚀 Instalasi Cepat

### 1. Persiapan Sistem
```bash
sudo su
apt update -y
apt install curl git -y
```

### 2. Install Node.js via NVM
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
source ~/.bashrc
nvm --version
nvm install --lts
nvm use --lts
```

### 3. Clone dan Setup Aplikasi
```bash
cd /opt
git clone https://github.com/Mashad085/glass
unzip Glass-ISC-main.zip
cd Glass-ISC-main
mkdir -p logs
chmod u+x ./bin/*
```

### 4. Install Dependencies dan Jalankan
```bash
npm install
npm start
```

## ⚙️ Konfigurasi

### File Konfigurasi Utama
Edit file `config/config.json` untuk menyesuaikan pengaturan:
```json
{
  "port": 3000, (tidak terpakai)
  "dhcpConfigPath": "/etc/dhcp/dhcpd.conf",
  "leaseFilePath": "/var/lib/dhcp/dhcpd.leases",
  "logFilePath": "/var/log/syslog"
}
```

## 🖥️ Penggunaan

### Start Aplikasi
```bash
# Development mode
npm start

# Production mode (dengan PM2)
npm install -g pm2
PORT=3000 pm2 start ./bin/www --name dhcp-management
pm2 save
pm2 startup
pm2 save
```

### Akses Web Interface
Buka browser dan akses:
```
http://server-ip:3000
```

### Port Default
- **Web Interface**: Port 3000
- **API Endpoint**: `http://localhost:3000/api`

## 📊 Fitur API

Aplikasi menyediakan REST API untuk integrasi:

| Endpoint | Method | Deskripsi |
|----------|--------|-----------|
| `/api/leases` | GET | Daftar semua lease aktif |
| `/api/config` | PUT | Update konfigurasi DHCP |
| `/api/status` | GET | Status server DHCP |
| `/api/logs` | GET | Stream log real-time |

## 🔧 Troubleshooting

### Masalah Umum dan Solusi

1. **Port 3000 tidak dapat diakses**
   ```bash
   # Periksa firewall
   sudo ufw allow 3000/tcp
   
   # Periksa proses yang berjalan
   netstat -tulpn | grep :3000
   ```

2. **Permission denied pada log files**
   ```bash
   # Tambahkan user ke grup yang sesuai
   sudo usermod -a -G syslog $USER
   sudo chmod 644 /var/log/syslog
   ```

3. **Node.js tidak dikenali**
   ```bash
   # Reload shell configuration
   source ~/.bashrc
   source ~/.profile
   
   # Verifikasi instalasi
   node --version
   nvm current
   ```

### Log Files
- **Aplikasi Log**: `/opt/glass-isc-dhcp/logs/app.log`
- **Error Log**: `/opt/glass-isc-dhcp/logs/error.log`


## 📄 Lisensi

Proyek ini berdasarkan pada [Akkadius/glass-isc-dhcp](https://github.com/Akkadius/glass-isc-dhcp) dan dilisensikan di bawah [MIT License](LICENSE).
