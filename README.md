# Snort IDS
Snort menggunakan serangkaian aturan yang membantu menentukan aktivitas jaringan berbahaya dan menggunakan aturan tersebut untuk menemukan paket yang cocok dan menghasilkan peringatan bagi pengguna.

User manual Snort: http://manual-snort-org.s3-website-us-east-1.amazonaws.com/

## Arsitektur Lab

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/arsitektur%20lab.png)

## Requirement
- [Virtualbox](https://www.virtualbox.org/)
- [Ubuntu Desktop versi 22.04](https://ubuntu.com/download/desktop)
- [Kali Linux versi 2022.4](https://www.kali.org/get-kali/#kali-platforms)

## Instalasi Snort di Ubuntu
- Cek nama interface yang tersedia
```sh
ifconfig
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/snort%201.JPG)

- Lakukan update terlebih dahulu
```sh
sudo apt update
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/snort%202.JPG)

- Install Snort
```sh
sudo apt install snort
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/snort%203.JPG)

- Cek hasil instalasi snort
```sh
snort -V
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/snort%204.JPG)

- Buat file backup untuk konfigurasi snort
```sh
sudo cp /etc/snort/snort.conf /etc/snort/snort.conf.backup
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/snort%205.JPG)

## Konfigurasi Snort
- Masuk sebagai user root

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/snort%206.JPG)

- Buka file konfigurasi snort
```sh
nano /etc/snort/snort.conf
```
- Tambahkan IP network dibaris berikut

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/snort%207.JPG)

- Cek validasi konfigurasi snort
```sh
snort -T -c /etc/snort/snort.conf
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/snort%208.JPG)

- Jalankan snort
```sh
snort -A console -q -c /etc/snort/snort.conf -i enp0s3
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/snort%209.JPG)

- Lakukan port scanning dengan tool `nmap` di sisi Attacker
```sh
nmap <IP_target>
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/snort%2010.JPG)

- Log terdeteksi di snort. Tekan `Ctrl+C` untuk menghentikan snort

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/snort%2011.JPG)

## Simulasi Serangan
- [Deteksi serangan DDOS](Deteksi%20DDOS.md)
- [Deteksi SQL Injection](Deteksi%20SQL%20Injection.md)