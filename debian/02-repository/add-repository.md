## Menambah Repository Debian

Perintah menambah repository

    nano /etc/apt/sources.list

Menggunakan repository debian.org

    deb http://deb.debian.org/debian/ bookworm main non-free-firmware
    deb-src http://deb.debian.org/debian/ bookworm main non-free-firmware

Repository security debian

    deb http://security.deb.debian.org/debian-security bookworm-security main non-free-firmware
    deb-src http://security.deb.debian.org/debian-security bookworm-security main non-free-firmware

Repository bookworm updates

    deb http://deb.debian.org/debian/ bookworm-updates main non-free-firmware
    deb-src http://deb.debian.org/debian/ bookworm-updates main non-free-firmware

Jika menggunakan untrusted repository atau local repo bisa menambahkan

    deb [trusted=yes] http://...

---

Update repository

    apt update 

Cek package yang dapat di upgrade

    apt list --upgradable

Upgrade package

    apt upgrade

