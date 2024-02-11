# Iptables
Perintah Iptables untuk mengizinkan port/service yang diperlukan dan memblokir semua port yang tidak diperlukan.
## Input Rules
Rules untuk mengelola trafik yang masuk ke Linux Server 

### Mengizinkan input dari interface Loopback

    iptables -A INPUT -i lo -j ACCEPT

### Mengizinkan input dari trafik yang sudah ada & terkait

    iptables -A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT

### Mengizinkan trafik input untuk protokol ICMP (ping)
    
    iptables -A INPUT -p icmp -j ACCEPT

### Mengizinkan trafik input untuk service DNS dengan port udp & tcp
    
    iptables -A INPUT -p udp --dport 53 --sport 1024:65535 -j ACCEPT
    iptables -A INPUT -p tcp  --dport 53 --sport 1024:65535 -j ACCEPT

### Mengizinkan trafik input passive port yang digunakan untuk FTP server

    iptables -A INPUT -p tcp -m multiport --dports 49152:65534 -j ACCEPT

### Mengizinkan trafik input untuk service HTTP & HTTPS
    
    iptables -A INPUT -p tcp --dport 80 -j ACCEPT
    iptables -A INPUT -p tcp --dport 443 -j ACCEPT
    
    # Bisa digabung menjadi 1 rule
    iptables -A INPUT -p tcp -m multiport --dports 80,443 -j ACCEPT

### Mengizinkan trafik input untuk service SSH

    iptables -A INPUT -p tcp --dport 22 -j ACCEPT

    # Mengubah port SSH
    iptables -A INPUT -p tcp --dport 2222 -j ACCEPT

### Mengizinkan trafik input untuk service FTP

    iptables -A INPUT -p tcp --dport 21 -j ACCEPT

    # Mengubah port FTP
    iptables -A INPUT -p tcp --dport 21211 -j ACCEPT

### Mengizinkan trafik input untuk service Samba

    iptables -A INPUT -p tcp --dport 137 -j ACCEPT
    iptables -A INPUT -p tcp --dport 138 -j ACCEPT
    iptables -A INPUT -p tcp --dport 139 -j ACCEPT
    iptables -A INPUT -p tcp --dport 445 -j ACCEPT

### Mengizinkan trafik input untuk service SMTP, IMAP, dan POP3 (Mail server)

    iptables -A INPUT -p tcp --dport 25 -j ACCEPT
    iptables -A INPUT -p tcp --dport 143 -j ACCEPT
    iptables -A INPUT -p tcp --dport 110 -j ACCEPT

### Mengizinkan trafik input untuk service DHCP

    iptables -A INPUT -p udp --dport 67 -j ACCEPT
    iptables -A INPUT -p udp --dport 68 -j ACCEPT

### Mengizinkan trafik input untuk service MariaDB/MySQL

    iptables -A INPUT -p tcp --dport 3306 -j ACCEPT

### Rules blokir trafik yang masuk ke server

    iptables -A INPUT -j DROP
    iptables -A INPUT -p icmp -s 192.168.1.2 -j DROP
    iptables -A INPUT -p icmp -s 192.168.1.0/24 -j DROP
    iptables -A INPUT -p tcp --dport 22 -m iprange --src-range 192.168.1.2-192.168.1.5 -j DROP

### Spesifik Input Rules
Misalkan mengizinkan trafik input dari suatu network tertentu untuk mengakses SSH server

    iptables -A INPUT -p tcp -s 192.168.1.2 --dport 22 -j ACCEPT
    iptables -A INPUT -p tcp -s 192.168.1.0/24 --dport 22 -j ACCEPT
    iptables -A INPUT -p tcp --dport 22 -m iprange --src-range 192.168.1.6-192.168.1.254 -j ACCEPT

---

## Output Rules

Rules untuk mengelola trafik yang keluar dari Linux Server 

### Mengizinkan output dari interface Loopback

    iptables -A OUTPUT -o lo -j ACCEPT

### Mengizinkan output dari trafik yang sudah ada

    iptables -A OUTPUT -m conntrack --ctstate ESTABLISHED -j ACCEPT

### Mengizinkan trafik output protokol ICMP (ping)
    
    iptables -A OUTPUT -p icmp -j ACCEPT

### Mengizinkan trafik output service DNS dengan port udp & tcp
    
    iptables -A OUTPUT -p udp --dport 53 --sport 1024:65535 -j ACCEPT
    iptables -A OUTPUT -p tcp  --dport 53 --sport 1024:65535 -j ACCEPT

### Mengizinkan trafik output passive port yang digunakan untuk FTP server

    iptables -A OUTPUT -p tcp -m multiport --sports 49152:65534 -j ACCEPT

### Mengizinkan trafik output service HTTP & HTTPS
    
    iptables -A OUTPUT -p tcp --sport 80 -j ACCEPT
    iptables -A OUTPUT -p tcp --sport 443 -j ACCEPT
    
    # Bisa digabung menjadi 1 rule
    iptables -A OUTPUT -p tcp -m multiport --sports 80,443 -j ACCEPT

### Mengizinkan trafik output service SSH

    iptables -A OUTPUT -p tcp --sport 22 -j ACCEPT

    # Mengubah port SSH
    iptables -A OUTPUT -p tcp --sport 2222 -j ACCEPT

### Mengizinkan trafik output service FTP

    iptables -A OUTPUT -p tcp --sport 21 -j ACCEPT

    # Mengubah port FTP
    iptables -A OUTPUT -p tcp --sport 21211 -j ACCEPT

### Mengizinkan trafik output service Samba

    iptables -A OUTPUT -p tcp --sport 137 -j ACCEPT
    iptables -A OUTPUT -p tcp --sport 138 -j ACCEPT
    iptables -A OUTPUT -p tcp --sport 139 -j ACCEPT
    iptables -A OUTPUT -p tcp --sport 445 -j ACCEPT

### Mengizinkan trafik output service DHCP

    iptables -A OUTPUT -p udp --sport 67 -j ACCEPT
    iptables -A OUTPUT -p udp --sport 68 -j ACCEPT

### Mengizinkan trafik output service SMTP, IMAP, dan POP3 (Mail server)

    iptables -A OUTPUT -p tcp --sport 25 -j ACCEPT
    iptables -A OUTPUT -p tcp --sport 143 -j ACCEPT
    iptables -A OUTPUT -p tcp --sport 110 -j ACCEPT

### Mengizinkan trafik output service MariaDB/MySQL

    iptables -A OUTPUT -p tcp --sport 3306 -j ACCEPT

### Memblokir semua trafik yang keluar dari server

    iptables -A OUTPUT -j DROP

---

## NAT
Konfigurasi NAT pada iptables, agar client-client dari Linux server bisa terkoneksi dengan internet.

    # NAT menggunakan output interface
    iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE

    # NAT untuk spesifik network client
    iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -o enp0s3 -j MASQUERADE

---

## Show Rules
Perintah untuk melihat rules yang sudah diterapkan pada iptables

    iptables -L
    iptables -nvL
    iptables -L --line-numbers
    iptables -nvL -t nat
    iptables -nvL -t nat --line-numbers

---

## Delete Rules
Perintah untuk menghapus semua rules pada iptables

    iptables -X
    iptables -F

Perintah untuk menghapus spesifik rules

    # lihat nomor rule yang ingin dihapus terlebih dahulu
    iptables -L --line-numbers

    # menghapus rule berdasarkan chain dan nomor rule
    iptables -D namachain nomorrule
    iptables -D INPUT 2

    # menghapus rule pada rules NAT
    iptables -nvL -t nat --line-numbers
    iptables -t nat -D namachain nomorrule
    iptables -t nat -D POSTROUTING 1
