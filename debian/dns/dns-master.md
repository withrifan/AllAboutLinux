## DNS Server

Configure DNS Server Bind9

- apt install bind9 dnsutils
- cp /etc/bind/db.local /etc/bind/db.domain
- cp /etc/bind/db.127 /etc/bind/db/ip
- nano named.conf.local
  zone "debiandua.com" {
  type master;
  file "/etc/bind/db.domain";
  };
  zone "1.168.192.in-addr.arpa" {
  type master;
  file "/etc/bind/db.ip";
  };

- nano db.domain
  @ IN A debiandua.com.
  @ IN A 192.168.1.2
  www IN A 192.168.1.2
  blog IN CNAME www
- nano db.ip
  @ IN NS debiandua.com.
  1 IN PTR debiandua.com.
- nano named.conf.options
  recursion yes;
  allow-query { any; };
  forwarders {
  8.8.8.8;
  };
  forward only;

dnssec-enable yes;
dnssec-validation yes;

- systemctl restart bind
- nano /etc/resolv.conf
  nameserver debiandua.com
  nameserver 192.168.1.2
- nslookup debiandua.com

konfigurasi dns

- apt install bind9 dnsutils
- cp /etc/bind/db.local /etc/bind/db.domain
- cp /etc/bind/db.127 /etc/bind/db.ip
- nano named.conf.local
  zone "debiantiga.com" {
  type master;
  file "/etc/bind/db.domain";
  };
  zone "10.168.192.in-addr.arpa" {
  type master;
  file "/etc/bind/db.ip";
  };
- nano db.domain
  @ IN A debiantiga.com.
  @ IN A 192.168.10.2
  @ IN MX 10 mail.debiantiga.com
  mail IN A 192.168.10.2
  ntp IN A 192.168.10.2
- nano db.ip
  2 IN NS debiantiga.com.
  2 IN PTR debiantiga.com.
  2 IN PTR mail.debiantiga.com.
  2 IN PTR ntp.debiantiga.com.
- nano named.conf.options
  allow-query { any; };
  forwarders {
  8.8.8.8;
  };
  forward only;
  dnssec-enable no;
  dnssec-validation no;
- systemctl restart bind9
- nano /etc/resolv.conf
  nameserver 192.168.10.2
- nslookup debiantiga.com
- nslookup mail.debiantiga.com
- nslookup ntp.debiantiga.com

konfigurasi dns

- apt install bind9 dnsutils
- cp /etc/bind/db.local /etc/bind/db.domain
- cp /etc/bind/db.127 /etc/bind/db.ip
- nano named.conf.local
  zone "debianlima.com" {
  type master;
  file "/etc/bind/db.domain";
  };
  zone "10.168.192.in-addr.arpa" {
  type master;
  file "/etc/bind/db.ip";
  };
- nano db.domain
  @ IN A debianlima.com.
  @ IN A 192.168.10.2
  @ IN MX 10 mail.debianlima.com
  mail IN A 192.168.10.2
- nano db.ip
  2 IN NS debianlima.com.
  2 IN PTR debianlima.com.
  2 IN PTR mail.debianlima.com.
- nano named.conf.options
  allow-query { any; };
  forwarders {
  8.8.8.8;
  };
  dnssec-enable no;
  dnssec-validation no;
- systemctl restart bind9
- nano /etc/resolv.conf
  nameserver 192.168.10.2
- nslookup debianlima.com
- nslookup mail.debianlima.com

konfigurasi dns

- apt install bind9 dnsutils
- cp /etc/bind/db.local /etc/bind/db.domain
- cp /etc/bind/db.127 /etc/bind/db.ip
- nano named.conf.local
  zone "debianenam.com" {
  type master;
  file "/etc/bind/db.domain";
  };
  zone "10.168.192.in-addr.arpa" {
  type master;
  file "/etc/bind/db.ip";
  };
- nano db.domain
  @ IN NS debianenam.com.
  @ IN A 192.168.10.2
  @ IN MX 10 mail.debianenam.com.
  mail IN A 192.168.10.2
  proxy IN A 192.168.10.2
  www IN A 192.168.10.2
- nano db.ip
  @ IN NS debianenam.com.
  2 IN PTR debianenam.com.
- nano named.conf.options
  allow-query { any; };
  forwarders {
  8.8.8.8;
  };
  dnssec-enable no;
  dnssec-validation no;
- systemctl restart bind9
- nano /etc/resolv.conf
  nameserver 192.168.10.2
- nslookup debianenam.com

konfigurasi dns master

- apt install bind9 dnsutils
- cd /etc/bind/
- nano named.conf.local
  zone "debiandelapan.com" {
  type master;
  file "/etc/bind/db.domain";
  allow-transfer {192.168.20.2;};
  also-notify {192.168.20.2;};
  };

zone "20.168.192.in-addr.arpa" {
type master;
file "/etc/bind/db.ip";
allow-transfer {192.168.20.2;};
also-notify {192.168.20.2;};
};

- nano named.conf.options
  allow-query { any; };
  forwarders {
  8.8.8.8;
  };
  dnssec-enable no;
  dnssec-validation no;
- nano db.domain
  @ IN A debiandelapan.com.
  @ IN A 192.168.10.2
  @ IN MX 10 mail.debiandelapan.com.
  mail IN A 192.168.10.2
  www IN A 192.168.10.2
- nano db.ip
  @ IN NS debiandelapan.com.
  2 IN PTR debiandelapan.com.
- systemctl restart bind9
- nano /etc/resolv.conf
  nameserver 192.168.20.2
