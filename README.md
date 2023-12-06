# Snort IDS
Snort menggunakan serangkaian aturan yang membantu menentukan aktivitas jaringan berbahaya dan menggunakan aturan tersebut untuk menemukan paket yang cocok dan menghasilkan peringatan bagi pengguna.

## Arsitektur Lab

## Requirement
- [Virtualbox](https://www.virtualbox.org/)
- [Ubuntu Desktop versi 22.04](https://ubuntu.com/download/desktop)
- [Kali Linux versi 2022.4](https://www.kali.org/get-kali/#kali-platforms)

## Instalasi Snort di Ubuntu
- Cek nama interface yang tersedia
```sh
ifconfig
```

- Lakukan update terlebih dahulu
```sh
sudo apt update
```

- Install Snort
```sh
sudo apt install snort
```

- Cek hasil instalasi snort
```sh
snort -V
```

- Buat file backup untuk konfigurasi snort
```sh
sudo cp /etc/snort/snort.conf /etc/snort/snort.conf.backup
```


## Konfigurasi Snort
- Masuk sebagai user root

- Buka file konfigurasi snort
```sh
nano /etc/snort/snort.conf
```
- Tambahkan IP network dibaris berikut


- Cek validasi konfigurasi snort
```sh
snort -T -c /etc/snort/snort.conf
```

- Jalankan snort
```sh
snort -A console -q -c /etc/snort/snort.conf -i enp0s3
```

- Lakukan port scanning dengan tool `nmap` di sisi Attacker
```sh
nmap <IP_target>
```

- Log terdeteksi di snort. Tekan `Ctrl+C` untuk menghentikan snort





- Name:
```sh
Smith'; select * from user_system_data; --
```

![alt text](https://github.com/rahardian-dwi-saputra/webgoat/blob/main/assets/wg%2010.JPG)

Password user Dave:
```sh
passW0rD
```

## Can you login as Tom?