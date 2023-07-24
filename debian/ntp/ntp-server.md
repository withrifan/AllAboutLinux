konfigurasi ntp server

- apt install chrony
- nano /etc/chrony/chrony.conf
- server 0.id.pool.ntp.org
  server 1.id.pool.ntp.org
  server 2.id.pool.ntp.org
  server 3.id.pool.ntp.org

allow 192.168.1.0/24

- systemctl restart chrony
- chronyc sources
- ufw allow 123/udp

konfigurasi ntp server

- apt install ntp ntpdate
- nano /etc/ntp.conf
  server 127.127.1.0
  fudge 127.127.1.0 stratum 1
  dan tambahkan pada cryptographically authenticated
  restrict 192.168.10.0 mask 255.255.255.0 nomodify notrap
- systemctl restart ntp
- pengujian ketik ntpq -p

konfigurasi ntp server

- apt install ntp ntpdate
- nano /etc/ntp.conf
  server 127.127.1.0
  fudge 127.127.1.0 stratum 1
  dan tambahkan pada cryptographically authenticated
  restrict 192.168.10.0 mask 255.255.255.0 nomodify notrap
- systemctl restart ntp
- pengujian ketik ntpq -pn
- ntpdate -u 192.168.10.1 (diatur di client, ip nya server)

konfigurasi ntp server

- apt install ntpd
- nano /etc/ntp.conf
  beri tanda # pada pool 0 sampai pool 3
  dan tambahkan
  server 127.127.1.0
  fudge 127.127.1.0 stratum 1
  pada cryptographically
  tambahkan restrict 192.168.10.0 mask 255.255.255.0 nomodify notrap
- systemctl restart ntp

konfigurasi ntp

- apt install ntp ntpdate
- nano /etc/ntp.conf
  server 127.127.1.0
  fudge 127.127.1.0 stratum 1
  dan tambahkan pada cryptographically authenticated
  restrict 192.168.10.0 mask 255.255.255.0 nomodify notrap
- systemctl restart ntp
- pengujian ketik ntpq -p

- apt install ntp
- nano /etc/ntp.conf
  beri # pada pool 0 1 2 3
  server 127.127.1.0
  fudge 127.127.1.0 stratum 1
  restrict 192.168.2.0 mask 255.255.255.0 nomodify notrap
