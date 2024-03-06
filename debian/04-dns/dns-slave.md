## DNS Slave

Konfigurasi DNS server menggunakan Bind9

    apt install bind9 dnsutils

Konfigurasi zone tipe slave untuk domain withrifan.id

    nano /etc/bind/named.conf.local

    zone "withrifan.id" {
        type slave;
        file "db.domain";
        masters {10.10.10.254;};
    };

Restart Bind9

    systemctl restart bind9

Cek apakah db.domain sudah ada di server slave

    ls /var/cache/bind/

Ubah resolv.conf

    nano /etc/resolv.conf

    nameserver 10.10.10.254
    nameserver 10.10.10.253