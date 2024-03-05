## DHCP Server

install isc-dhcp-server packages & backup default config

    apt install isc-dhcp-server
    cp /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf.backup

config DHCP server for 192.168.10.0/24 with range 192.168.10.100-200

    nano /etc/dhcp/dhcpd.conf
        # A slightly different configuration for an internal subnet.
        subnet 192.168.10.0 netmask 255.255.255.0 {
        range 192.168.10.100 192.168.10.200;
        option domain-name-servers 192.168.10.1;
        option domain-name "example.com";
        option routers 192.168.10.1;
        option broadcast-address 192.168.10.255;
        default-lease-time 600;
        max-lease-time 7200;
        }

add an interface that will serve DHCP requests

    nano /etc/default/isc-dhcp-server
        # On what interfaces should the DHCP server (dhcpd) serve DHCP requests?
        #Separate multiple interfaces with spaces, e.g. "eth0 eth1".
        INTERFACESv4="enp0s3"
        INTERFACESv6=""

restart & check status for service DHCP server

    systemctl restart isc-dhcp-server.service
    systemctl status isc-dhcp-server.service
