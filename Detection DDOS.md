# Deteksi Serangan DDOS
Serangan distributed denial-of-service (DDoS) adalah upaya jahat untuk mengganggu lalu lintas normal server, layanan, atau jaringan yang ditargetkan dengan membanjiri target atau infrastruktur di sekitarnya dengan membanjirnya lalu lintas Internet.

## Konfigurasi Rule
- Buka file konfigurasi rule local snort
```sh
gedit /etc/snort/rules/local.rules
```
- Tambahkan rule berikut ini lalu tekan tombol Save
```sh
alert icmp any any -> $HOME_NET any (msg:"ICMP flood"; sid:1000001; rev:1; classtype:icmp-event; detection_filter:track by_dst, count 50, seconds 3;)
```


- Jalankan snort
```sh
snort -A console -q -c /etc/snort/snort.conf -i enp0s3
```

- Lakukan serangan DOS dari sisi Attacker dengan membanjiri paket icmp
```sh
hping3 --faster --icmp -p 80 -V 192.168.100.12
```

- Hasil pemantauan snort