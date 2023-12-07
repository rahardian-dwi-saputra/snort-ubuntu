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


- Jalankan snort
```sh
snort -A console -q -c /etc/snort/snort.conf -i enp0s3
```

- Masukkan tanda kutip tunggal (') pada web DVWA

- Hasil pemantauan snort

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

- Jalankan snort
```sh
snort -A console -q -c /etc/snort/snort.conf -i enp0s3
```

- Masukkan query injeksi berikut ini pada web DVWA
```sh
q' UNION SELECT user, password FROM users #
```

- Hasil pemantauan snort