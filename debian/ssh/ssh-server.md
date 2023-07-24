konfigurasi ssh

- apt install openssh-server
- nano /etc/ssh/sshd_config
  tambahkan AllowUsers tkj@192.168.2.3
- systemctl restart ssh
