type master;
allow-transfer {172.16.2.2;};
also-notify {172.16.2.2;};
nameserver 172.16.1.2;

type slave;
masters {172.16.1.2;};
nameserver 172.16.2.2;
nameserver 172.16.1.2;

konfigurasi dns slave

- apt install bind9 dnsutils
- nano /etc/bind/named.conf.local
  zone "debiandelapan.com" {
  type slave;
  masters {192.168.10.2;};
  };
- systemctl restart bind9
- nano /etc/resolv.conf
  nameserver 192.168.20.2
  nameserver 192.168.10.2
