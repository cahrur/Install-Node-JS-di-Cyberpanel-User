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
