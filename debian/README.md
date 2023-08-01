## Add User in Sudoers

login to Root user & install sudo packages

    su -
    apt install sudo

add user privilege

    usermod -aG sudo rifan

check user

    groups rifan
    su - rifan
    sudo whoami
