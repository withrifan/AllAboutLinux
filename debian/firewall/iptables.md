- apt install iptables-persistent
  iptables -L
  iptables -A POSTROUTING -t nat -o enp0s3 -j MASQUERADE
  iptables -A PREROUTING -t nat -o enp0s3 -j REDIRECT -p tcp -s 192.168.2.0/24
  --dport 80 -to--ports 3128
  iptables-save > /etc/iptables/rules.v4
- nano /etc/sysctl.conf
  net.ipv4.ip_forward = 1

- iptables -A INPUT -p tcp --dport 22 -m iprange --src-range 192.168.2.2-192.168.2.10 -j ACCEPT
- iptables -A INPUT -p tcp --dport 22 -j DROP
- iptables-save > /etc/iptables/rules.v4
- reboot

#atur iptables

- iptables -A INPUT -p tcp --dport 20 -m iprange --src-range 192.168.2.2-192.168.2.10 -j ACCEPT
- iptables -A INPUT -p tcp --dport 21 -m iprange --src-range 192.168.2.2-192.168.2.10 -j ACCEPT
- iptables-save > /etc/iptables/rules.v4
- reboot
