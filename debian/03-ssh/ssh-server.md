## SSH Server

Konfigurasi openssh-server

    apt install openssh-server
    nano /etc/ssh/sshd_config

Mengubah port SSH

    Port 2222

Mengizinkan login menggunakan user Root

    PermitRootLogin yes

Menambahkan user & group yang diizinkan dan diblokir saat remote ssh server

    AllowUsers root rifan
    AllowGroups rifan
    DenyUsers user1
    DenyGroups user1

---

Restart & cek status service SSH

    systemctl restart ssh
    systemctl status ssh

Connect ke SSH server

    ssh user@ipaddress -p portnumber
    ssh rifan@192.168.1.254 -p 2222