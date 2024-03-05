## DNS Server

Konfigurasi DNS server menggunakan Bind9

    apt install bind9 dnsutils

Konfigurasi zone tipe master untuk domain withrifan.id

    nano /etc/bind/named.conf.local

    zone "withrifan.id" {
        type master;
        file "db.domain";
    };

    //ip address dimulai dari belakang
    zone "10.10.10.in-addr.arpa" {
            type master;
            file "db.ip";
    };

Konfigurasi DNS forwarders

    nano /etc/bind/named.conf.options

    forwarders {
        10.10.10.1;
        8.8.8.8;
    };
    allow-query {any;};
    recursion yes;

Membuat db.domain dan db.ip

    cp /etc/bind/db.local /var/cache/bind/db.domain
    cp /etc/bind/db.127 /var/cache/bind/db.ip

Menambah record DNS pada db.domain

    nano /var/cache/bind/db.domain

    ;
    ; BIND data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     withrifan.id. root.withrifan.id. (
                                  2         ; Serial
                            604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                            604800 )       ; Negative Cache TTL
    ;
    @       IN      NS      withrifan.id.
    @       IN      A       10.10.10.254
    www     IN      CNAME   @
    ssh     IN      A       10.10.10.254
    ftp     IN      A       10.10.10.254
    ntp     IN      A       10.10.10.254
    samba   IN      A       10.10.10.254
    webmail IN      A       10.10.10.254
    @       IN      MX      10      mail.withrifan.id.
    mail    IN      A       10.10.10.254

Konfigurasi reverse DNS pada db.ip

    nano /var/cache/bind/db.ip

    ;
    ; BIND reverse data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     withrifan.id. root.withrifan.id. (
                                  1         ; Serial
                            604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                            604800 )       ; Negative Cache TTL
    ;
    @       IN      NS      withrifan.id.
    254     IN      PTR     withrifan.id.
    254     IN      PTR     www.withrifan.id.
    254     IN      PTR     ssh.withrifan.id.
    254     IN      PTR     ftp.withrifan.id.
    254     IN      PTR     ntp.withrifan.id.
    254     IN      PTR     webmail.withrifan.id.
    254     IN      PTR     mail.withrifan.id.
    254     IN      PTR     samba.withrifan.id.

---

Restart & cek status Bind9

    systemctl restart bind9
    systemctl status bind9

Ubah resolv.conf

    nano /etc/resolv.conf

    nameserver 10.10.10.254

Pengujian DNS

    nslookup withrifan.id
    nslookup 10.10.10.254

## Konfigurasi DNS Master

Lakukan hal yang sama seperti di atas sesuai kebutuhan. Hanya menambahkan IP server DNS slave pada zone

    nano /etc/bind/named.conf.local

    zone "withrifan.id" {
            type master;
            file "db.domain";
            allow-transfer {10.10.10.253;};
            also-notify {10.10.10.253;};
    };

    zone "10.10.10.in-addr.arpa" {
            type master;
            file "db.ip";
            allow-transfer {10.10.10.253;};
            also-notify {10.10.10.253;};
    };

Ubah resolv.conf

    nano /etc/resolv.conf

    nameserver 10.10.10.254
    nameserver 10.10.10.253