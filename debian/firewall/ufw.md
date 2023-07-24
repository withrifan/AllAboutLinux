konfigurasi ufw firewall

- apt install ufw
- ufw enable
- ufw allow from 192.168.10.0/24 to any port 443
- ufw allow from 192.168.10.0/24 to any port 53
- ufw allow from 192.168.10.0/24 to any port 3128
- ufw status numbered

konfigurasi ufw firewall

- apt install ufw
- ufw enable
- ufw status
- ufw allow from 192.168.10.1/24 to any port 53
- ufw allow from 192.168.10.1/24 to any port 80
- ufw allow from 192.168.10.1/24 to any port 433
- ufw allow from 192.168.10.1/24 to any port 3128

- apt install ufw
- ufw enable
- ufw status numbered
- ufw allow from 192.168.2.0/24 to any port 22
- ufw allow from 192.168.2.0/24 to any port 20
- ufw allow from 192.168.2.0/24 to any port 21
- ufw allow from 192.168.2.0/24 to any port 53
- ufw allow from 192.168.2.0/24 to any port 80
