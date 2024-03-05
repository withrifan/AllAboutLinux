## Menambahkan User ke Sudoers

login menggunakan user Root & install sudo packages

    su -
    apt install sudo

menambahkan user rifan ke grub sudo

    usermod -aG sudo rifan

cek user

    groups rifan
    su - rifan
    sudo whoami
