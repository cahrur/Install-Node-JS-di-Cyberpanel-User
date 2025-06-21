# Instalasi Node.js di CyberPanel User (Tanpa Akses Sudo)

Panduan ini menjelaskan cara menginstal Node.js versi 20.17.0 pada akun user CyberPanel tanpa akses `sudo` (non-root).

## 1. Buat SSH User
Pastikan kamu sudah membuat user dan bisa mengakses server via SSH.

## 2. Download dan Ekstrak Node.js
```bash
cd ~
curl -O https://nodejs.org/dist/v20.17.0/node-v20.17.0-linux-x64.tar.xz
tar -xf node-v20.17.0-linux-x64.tar.xz
mv node-v20.17.0-linux-x64 nodejs

```


## 3. Daftarkan Path
```bash
echo 'export PATH=$HOME/nodejs/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

## 4. Tambahkan ke .profile
``` bash
nano ~/.profile
```

## 5. Tambahkan Baris Ini di Bagian Bawah File:
``` bash
# Menambahkan direktori Node.js ke PATH
export PATH="$HOME/nodejs/bin:$PATH"
```

## 6. Simpan dan Keluar
Untuk nano: Tekan Ctrl+X, lalu Y, lalu Enter

## 7. Muat Ulang .profile ATAU Log Out/Log In Kembali:
``` bash
source ~/.profile
```

## 8. Cek Versi Node
``` bash
node -v
```

## 9. Instalasi PM2 (Process Manager)
``` bash
npm install pm2
```

## 10. Instalasi PM2 (Process Manager)
Agar perintah pm2 bisa diakses langsung dari terminal tanpa perlu mengetik path lengkapnya (~/node_modules/.bin/pm2).
``` bash
# Tambahkan baris ini ke file ~/.bashrc Anda
echo 'export PATH="$HOME/node_modules/.bin:$PATH"' >> ~/.bashrc
source ~/.bashrc # Muat ulang .bashrc
```
## 11. Menjalankan pm2
``` bash
# Ganti backend sesuai nama yang dikehendaki
pm2 start npm --name backend -- run start
```
## 12. Menyimpan Konfigurasi Proses
Ini akan membuat snapshot dari proses yang sedang berjalan
dan menyimpannya ke file dump yang akan digunakan PM2 saat startup
``` bash
pm2 save
```
## 13. Agar Otomatis Jalan Ketika Server di Restart
##### Buat Skrip Startup PM2
##### PM2 dapat menghasilkan skrip startup yang disesuaikan dengan sistem inisialisasi server Anda (misalnya systemd untuk sebagian besar distribusi Linux modern seperti Ubuntu 16+, CentOS 7+, Debian 7+, dll.).
``` bash
pm2 startup
```
Output dari perintah ini akan terlihat seperti ini (contoh untuk systemd di Ubuntu, bisa sedikit berbeda tergantung sistem Anda):
``` bash
[PM2] Init System found: systemd
[PM2] To setup the Startup Script, copy/paste the following command:
sudo env PATH=$PATH:/home/namadomain/nodejs/bin /home/namadomain/nodejs/lib/node_modules/pm2/bin/pm2 startup systemd -u usernameakun --hp /home/namadomain
```
##### - Ganti <usernameakun> dengan username yang sedang Anda gunakan.
##### - Ganti namadomain sesuai domain yang anda pakai.
##### - Perintah ini meminta Anda untuk menjalankan dengan sudo atau root.
## 14. Salin dan Jalankan Perintah sudo yang Dihasilkan
Salin seluruh baris perintah sudo yang dihasilkan dari output pm2 startup di atas, lalu tempel dan jalankan di terminal dengan akses sudo.
``` bash
sudo env PATH=$PATH:/home/namadomain/nodejs/bin /home/namadomain/nodejs/lib/node_modules/pm2/bin/pm2 startup systemd -u usernameakun --hp /home/namadomain
```
Perintah ini akan:
##### - Mendeteksi sistem init Anda (misalnya systemd).
##### - Membuat file service (misalnya pm2-yourusername.service di systemd).
##### - Mengaktifkan service tersebut agar dimulai saat boot.





