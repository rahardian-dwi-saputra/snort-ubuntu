# Deteksi Serangan DDOS
Serangan distributed denial-of-service (DDoS) adalah upaya jahat untuk mengganggu lalu lintas normal server, layanan, atau jaringan yang ditargetkan dengan membanjiri target atau infrastruktur di sekitarnya dengan membanjirnya lalu lintas Internet.

## Konfigurasi Rule untuk ICMP Flood Attack
- Buka file konfigurasi rule local snort
```sh
gedit /etc/snort/rules/local.rules
```
- Tambahkan rule berikut ini lalu tekan tombol Save
```sh
alert icmp any any -> $HOME_NET any (msg:"ICMP flood"; sid:1000001; rev:1; classtype:icmp-event; detection_filter:track by_dst, count 50, seconds 3;)
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20ddos/ddos%201.JPG)

- Jalankan snort
```sh
snort -A console -q -c /etc/snort/snort.conf -i enp0s3
```
- Lakukan serangan DOS dari sisi Attacker dengan membanjiri paket icmp
```sh
hping3 --faster --icmp -p 80 -V 192.168.100.12
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20ddos/ddos%202.JPG)

- Hasil pemantauan snort

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20ddos/ddos%203.JPG)

## Konfigurasi Rule untuk SYN Flood Attack
- Buka file konfigurasi rule local snort
```sh
gedit /etc/snort/rules/local.rules
```
- Tambahkan rule berikut ini lalu tekan tombol Save
```sh
alert tcp any any -> $HOME_NET any (msg: "Possible TCP SYN Flood attack detected"; sid: 1000002; rev:1; detection_filter:track by_dst, count 20, seconds 3;)
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20ddos/ddos%204.JPG)

- Jalankan snort
```sh
snort -A console -q -c /etc/snort/snort.conf -i enp0s3
```
- Lakukan serangan DOS dari sisi Attacker dengan membanjiri paket SYN
```sh
hping3 --rand-source -p 80 -S --faster 192.168.100.12
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20ddos/ddos%205.JPG)

- Hasil pemantauan snort

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20ddos/ddos%206.JPG)

## Konfigurasi Rule untuk UDP Flood Attack
- Buka file konfigurasi rule local snort
```sh
gedit /etc/snort/rules/local.rules
```
- Tambahkan rule berikut ini lalu tekan tombol Save
```sh
alert udp any any -> $HOME_NET any (msg:"UDP Flooding Attack"; sid:1000003; rev:2; detection_filter:track by_dst, count 10, seconds 30;)
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20ddos/ddos%207.JPG)

- Jalankan snort
```sh
snort -A console -q -c /etc/snort/snort.conf -i enp0s3
```
- Lakukan serangan DOS dari sisi Attacker dengan membanjiri paket UDP
```sh
hping3 --rand-source --faster --udp -p 53 192.168.100.12
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20ddos/ddos%208.JPG)

- Hasil pemantauan snort

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20ddos/ddos%209.JPG)

## Konfigurasi Rule untuk Land Attack
- Buka file konfigurasi rule local snort
```sh
gedit /etc/snort/rules/local.rules
```
- Tambahkan rule berikut ini lalu tekan tombol Save
```sh
alert tcp $HOME_NET any <> $HOME_NET any (msg:"Land Attack Detected";sid:1000004;rev:3;)
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20ddos/ddos%2010.JPG)

- Jalankan snort
```sh
snort -A console -q -c /etc/snort/snort.conf -i enp0s3
```
- Lakukan serangan DOS dari sisi Attacker dengan membanjiri paket UDP
```sh
hping3 -a 192.168.100.12 --faster -S -p 22 192.168.100.12
```

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20ddos/ddos%2011.JPG)

- Hasil pemantauan snort

![alt text](https://github.com/rahardian-dwi-saputra/snort-ubuntu/blob/main/assets/deteksi%20ddos/ddos%2012.JPG)