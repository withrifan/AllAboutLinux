konfigurasi proxy server

- apt install squid
- systemctl status squid
- cp /etc/squid/squid.conf{,.original}
- nano /etc/squid/squid.conf
- cari http_port 3128
- # http_access deny all
- cache_mgr debiansatu.com
- visible_hostname debiansatu
- hilangkan tanda pagar didepan cache_dir ufs /var/spool/squid 100 16 256
- dan cache_mem 256mb
- cari acl connect method connect
- tambah acl local src 192.168.1.0/24
  acl bloklist dstdomain "/etc/squid/domain.txt"
  acl blokkey url_regex -i "/etc/squid/wordlist.txt"
  acl download urlpath_regex \.mp3$\.mp4$\.mkv$\.3gp$\.avi$

http \_access deny bloklist
http_access deny blokkey
http_access deny download
http_access allow local

- nano /etc/squid/domain.txt
- isi dengan domain yg ingin diblokir .facebook.com
- nano /etc/squid/wordlist.txt
- isi dengan admin, local
- tambah firewall nat
  iptables -t nat -A PREROUTING -i enp0s8 -p tcp -s 192.168.1.0/24 -m tcp --dport 80 -j REDIRECT --to-port 3128
  iptables -t nat -A PREROUTING -i enp0s8 -p udp -s 192.168.1.0/24 -m udp --dport 80 -j REDIRECT --to-port 3128
- systemctl restart squid

konfigurasi proxy server

- apt install squid3
- nano /etc/squid/squid.conf
  pada #Default:
  cache_mgr webmaster ganti menjadi cache_mgr admin@proxy.debianlima.com
  lalu pada #Default:
  visible_hostname is used if no specific ID is set.
  ganti menjadi visible_hostname debian
  lalu pada http_access deny all tambahkan #
  lalu pada acl CONNECT method CONNECT
  di bawahnya tambahkan
  #Blok situs
  acl situs dstdomain "/etc/squid/situs.txt"
  http_access deny situs
  #Blok kata kunci
  acl katakunci url_regex -i "/etc/squid/katakunci.txt"
  http_access deny katakunci
  #Blok download
  acl download urlpath_regex \.mp4$ \.iso$
  #izinkan user
  acl user src 192.168.10.0/24
  http_access allow user
- nano /etc/squid/situs.txt
  masukkan domain yang ingin diblokir
- nano /etc/squid/katakunci.txt
  masukkan kata kunci yang ingin diblokir
- systemctl restart squid

konfigurasi proxy

- apt install squid3
- nano /etc/squid/squid.conf
  pada #Default:
  cache_mgr webmaster ganti menjadi cache_mgr admin@proxy.debianlima.com
  lalu pada #Default:
  visible_hostname is used if no specific ID is set.
  ganti menjadi visible_hostname debian
  lalu pada http_access deny all tambahkan #
  lalu pada acl CONNECT method CONNECT
  di bawahnya tambahkan
  acl situs dstdomain "/etc/squid/situs.txt"
  http_access deny situs
  acl user src 192.168.2.0/24
  http_access deny user
- nano /etc/squid/situs.txt
  masukkan domain yang ingin diblokir
- systemctl restart squid
