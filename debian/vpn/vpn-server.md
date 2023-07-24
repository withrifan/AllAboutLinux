konfigurasi vpn

- apt install pptd
- nano /etc/pptpd.conf
  hapus tanda # pada localip dan remoteip
- nano /etc/ppp/chap-secrets
  buat 2 user dan password untuk client vpnnya
- systemctl restart pptpd

konfigurasi vpn

- apt install pptpd
- nano /etc/pptpd.conf
  localip 192.168.10.2
  remoteip 192.168.2.3-100,192.168.2.254
- nano /etc/ppp/pptpd-options
  hapus # domain dan ganti domainnya
  di bagian bawah tambahkan
  ms-dns 192.168.10.2
  nobsdcomp
- nano /etc/ppp/chap-secrets
  tambahkan clientnya tkj dan secretnya tkjvpn
- systemctl restart pptpd
