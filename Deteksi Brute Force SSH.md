# Deteksi Serangan Brute Force pada SSH
Serangan brute force SSH adalah teknik peretasan yang melibatkan percobaan berulang kali kombinasi nama pengguna dan kata sandi yang berbeda hingga penyerang mendapatkan akses ke server jarak jauh.

## Konfigurasi Rule
- Buka file konfigurasi rule local snort
```sh
gedit /etc/snort/rules/local.rules
```
- Tambahkan rule berikut ini lalu tekan tombol Save
```sh
alert tcp $EXTERNAL_NET any -> $HOME_NET 22 (msg:"Possible SSH brute forcing!"; flags: S+; threshold: type both, track by_src, count 5, seconds 30; sid:1000007; rev: 1;)
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20brute%20force%20SSH%20login/brute%20force%20ssh%201.JPG)

- Jalankan snort
```sh
snort -A console -q -c /etc/snort/snort.conf -i enp0s3
```
- Brute force SSH dengan tool `hydra` dari sisi Attacker
```sh
hydra -l ubuntu -P /usr/share/seclists/Passwords/darkweb2017-top100.txt 192.168.100.12 ssh
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20brute%20force%20SSH%20login/brute%20force%20ssh%202.JPG)

- Hasil pemantauan snort

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20brute%20force%20SSH%20login/brute%20force%20ssh%203.JPG)