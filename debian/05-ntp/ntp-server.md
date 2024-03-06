## NTP server (ntpsec)

Cek waktu di Debian, pastikan sudah benar timezonenya

    timedatectl

Konfigurasi NTP server menggunakan id.pool.ntp.org dan beri tanda # pada debian ntp

    nano /etc/ntpsec/ntp.conf

    pool 0.id.pool.ntp.org
    pool 1.id.pool.ntp.org
    pool 2.id.pool.ntp.org
    pool 3.id.pool.ntp.org
    server 127.127.1.0
    fudge 127.127.1.0 stratum 1

Tambahkan di bagian bawah network yang digunakan sebagai sinkronisasi waktu (network Debian server)

    restrict 10.10.10.0 mask 255.255.255.0

Restart NTP

    systemctl restart ntpsec
    systemctl restart ntp

Cek NTP

    ntpq -pn

## NTP server (chrony)

Konfigurasi NTP server menggunakan chrony

    apt install chrony

Tambahkan id.pool.ntp.org dan beri tanda # pada debian pool ntp

    nano /etc/chrony/chrony.conf

    pool 0.id.pool.ntp.org iburst
    pool 1.id.pool.ntp.org iburst
    pool 2.id.pool.ntp.org iburst
    pool 3.id.pool.ntp.org iburst

Pada bagian bawah tambahkan network yang digunakan untuk sinkronisasi waktu (network Debian server)

    allow 10.10.10.0/24

Restart chrony

    systemctl restart chrony

Cek status

    chronyc sources


## Pengujian NTP server pada Windows

1. Masuk ke Control Panel
2. Masuk ke Clock and Regian
3. Pilih Set the time and date
4. Masuk ke Internet Time
5. Change settings
6. Masukkan domain ntp.withrifan.id
7. Update now