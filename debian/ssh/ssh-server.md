## SSH Server

config openssh-server

    apt install openssh-server
    ssh -V

    nano /etc/ssh/sshd_config

change port SSH

    Port 2222

permit root login

    PermitRootLogin yes

connect to SSH server

    ssh user@ipaddress -p portnumber
    ssh rifan@192.168.1.254 -p 2222

add allow/deny user & group to remote ssh server

    nano /etc/ssh/sshd_config

    AllowUsers root rifan
    AllowGroups rifan
    DenyUsers user1 user2
    DenyGroups user1 user1

restart & status service SSH

    systemctl restart ssh
    systemctl status ssh
