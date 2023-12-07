# Deteksi SQL Injection
SQL Injection (SQLi) adalah celah keamanan web yang memungkinkan penyerang mengintruksi query yang dibuat aplikasi untuk melihat data yang biasanya tidak dapat mereka ambil, misalnya data pengguna lain atau data lain apapun yang dapat diakses oleh aplikasi itu sendiri

## Identifikasi Error Based SQL Injection
- Penyerang biasanya menggunakan tanda kutip tunggal (') untuk mengidentifikasi kerentanan SQL Injection
- Buka file konfigurasi rule local snort
```sh
gedit /etc/snort/rules/local.rules
```
- Tambahkan rule berikut ini lalu tekan tombol Save
```sh
alert tcp any any -> $HOME_NET 80 (msg:"Error Based SQL Injection Detected"; content:"%27"; sid: 1000005; rev: 1;)
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20sql%20injection/sqli%201.JPG)

- Jalankan snort
```sh
snort -A console -q -c /etc/snort/snort.conf -i enp0s3
```
- Masukkan tanda kutip tunggal (') pada web DVWA

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20sql%20injection/sqli%202.JPG)

- Hasil pemantauan snort

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20sql%20injection/sqli%203.JPG)

## Identifikasi Union Based SQL Injection
- Penyerang biasanya menggunakan operator `UNION` untuk menggabungkan 2 query atau lebih di SQL Injection
- Buka file konfigurasi rule local snort
```sh
gedit /etc/snort/rules/local.rules
```
- Tambahkan tanda `#` untuk menonaktifkan rule sebelumnya lalu tambahkan rule berikut ini dan tekan tombol Save
```sh
alert tcp any any -> $HOME_NET 80 (msg: "UNION SELECT SQL Injection"; content:"union";  nocase; sid:1000006; rev: 1;)
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20sql%20injection/sqli%204.JPG)

- Jalankan snort
```sh
snort -A console -q -c /etc/snort/snort.conf -i enp0s3
```
- Masukkan query injeksi berikut ini pada web DVWA
```sh
q' UNION SELECT user, password FROM users #
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20sql%20injection/sqli%205.JPG)

- Hasil pemantauan snort

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20sql%20injection/sqli%206.JPG)