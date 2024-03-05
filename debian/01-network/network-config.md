## Setting IP address (IPv4)

Menghapus IP address yang sudah diterapkan pada sebuah interface

    ip addr flush enp0s3

---

Konfigurasi interface pada Debian

    nano /etc/network/interface

Jika menggunakan DHCP client

    auto enp0s3
    iface enp0s3 inet dhcp

Restart DHCP client interface

    sudo dhclient -r enp0s3
    sudo dhclient enp0s3

Jika menggunakan Static address

    auto enp0s3
    iface enp0s3 inet static
    address 10.10.10.254
    netmask 24
    gateway 10.10.10.1

---

Restart konfigurasi

    /etc/init.d/networking restart

Check IP address

    ip a

Tes ping ke gateway

    ping 10.10.10.1

---

Setup nameserver

    nano /etc/resolv.conf
    nameserver <ip address>
    nameserver 8.8.8.8

## Setting IP address (IPv6)

Jika menggunakan Static address

    auto enp0s3
    iface enp0s3 inet6 static
    address 2001:db8:abcd::2/64
    gateway 2001:db8:abcd::1

Restart konfigurasi

    /etc/init.d/networking restart

Tes ping ke gateway

    ping6 2001:db8:abcd::1

## Setting IP address Interface Vlan

Install package vlan

    apt install vlan

Mengaktifkan vlan module

    modprobe 8021q

Menambahkan interface vlan misal vlan 99 pada interface enp0s3

    nano /etc/network/interfaces

Konfigurasi IP address interface vlan 99

    auto enp0s3.99
    iface enp0s3.99 inet static
    address 10.10.99.254
    netmask 24
    gateway 10.10.99.1

Restart konfigurasi

    /etc/init.d/networking restart

Tes ping ke gateway

    ping 10.10.99.1