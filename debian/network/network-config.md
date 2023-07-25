## Setting IP address

Configure

    nano /etc/network/interface

---

DHCP client

    auto enp0s3
    iface enp0s3 inet dhcp

Restart DHCP client interface

    sudo dhclient -r enp0s3
    sudo dhclient enp0s3

---

Static address

    auto enp0s3
    iface enp0s3 inet static
    address 192.168.1.254
    netmask 24
    gateway 192.168.1.1

Restart Config

    /etc/init.d/networking restart

---

Check IP

    ip a

---

Setup nameserver

    nano /etc/resolv.conf
    nameserver 8.8.8.8
    nameserver 8.8.4.4
