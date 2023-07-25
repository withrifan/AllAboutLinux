## SSH Server

Config OpenSSH-Server

    apt install openssh-server
    nano /etc/ssh/sshd_config

Change port SSH

    Port 2222

Permit root login

    PermitRootLogin yes

Restart & status service SSH

    systemctl restart ssh
    systemctl status ssh

Connect to SSH server

    ssh user@ipaddress -p portnumber
    ssh rifan@192.168.1.254 -p 2222
