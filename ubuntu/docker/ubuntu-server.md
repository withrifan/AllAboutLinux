network:
    ethernets:
        enp0s3:
            dhcp4: no
            dhcp6: no
            addresses: [192.168.2.88/24]
            gateway4: 192.168.2.1
            nameservers:
                addresses: [1.1.1.1,1.0.0.1]
    version: 2

konfigurasi ntp server
- apt install ntp
- nano /etc/ntp.conf
beri # pada pool 0 1 2 3
tambahkan 
server 127.127.1.0
fudge 127.127.1.0 stratum 1
restrict 40.40.40.0 mask 255.255.255.0 nomodify notrap
- systemctl restart ntp
- ntpq -p

konfigurasi openssh
- apt install openssh-server
- nano /etc/ssh/sshd_config
PermitRootLogin yes
AllowUsers tkj@40.40.40.0/24
- sudo passwd
- systemctl restart ssh
#ssh keypair linuxclient
buka client
- ssh-keygen -t rsa
- enter dan kosongkan passphrase
- ssh-copy-id tkj@20.20.20.2 (ip server)
- ssh tkj@20.20.20.2 (remoteserver)
#mengirim file dari client linux ke server
- nano coba.txt
- scp ~/coba.txt tkj@20.20.20.2:~/

konfigurasi ftp
- apt install proftpd
- nano /etc/proftpd/proftpd.conf
ubah server name nya
hapus # Default root
- nano /etc/ftpuser (untuk memblokir user)
#anonymous login
- nano /etc/proftpd/proftpd.conf
hapus # pada <Anonymous> dan </Anonymous>
hapus # pada User dan Group
hapus # pada UserAlias
hapus # pada RequireValidShell
#ftp client linux remote
buka client linux 
- apt install lftp
- lftp -u tkj tkj@20.20.20.2 (remote server)
- pwd (melihat direktori server)
- !pwd (melihat direktori client)
- ls (melihat file yang ada di server)
- !ls -l (melihat file yang ada di client)
- put -a namafile.txt (upload file dari client ke server)
- mput -a namafile.txt namafilelagi.txt (upload beberapa file dari client ke server)
- get -a namafile.txt (download file dari server ke client)
- mget -a namafile.txt file.txt (download beberpa file dari server ke client)
- mkdir namafile (membuat folder di server)
- rmdir namafile (menghapus folder di server)
- rm test.txt (menghapus file di server)
- !ip a (menampilkan ip a pada client (menjalankan perintah client))

konfigurasi samba
- apt install samba
- mkdir /home/sambapublic
- mkdir /home/sambaprivate
- chmod 777 -R /home/sambapublic
- chmod 777 -R /home/sambaprivate
- smbpasswd -a tkj
- nano /etc/samba/smb.conf
[sambapublic]
path = /home/sambapublic
browseable = yes
writeable = yes
security = share
guest ok = yes
read only = no
#melarang file bertipe html
veto files =*html

[sambaprivate]
path = /home/sambaprivate
browseable = yes
writeable = no
security = user
valid user = tkj
guest ok = no
read only = yes
- systemctl restart smbd

konfigurasi dns
- apt install bind9
- cd /etc/bind
- cp db.local db.domain
- cp db.127 db.ip
- nano named.conf.local
zone "ubuntusatu.com" {
type master;
file "/etc/bind/db.domain";
};
zone "20.20.20.in-addr.arpa" {
type master;
file "/etc/bind/db.ip";
};
- nano db.domain
@	IN	A	ubuntusatu.com.
@	IN	A	20.20.20.2
@	IN	MX	10	mail.ubuntusatu.com
mail	IN	A	20.20.20.2
www	IN	A	20.20.20.2
- nano db.ip
2	IN	NS	ubuntusatu.com.
2	IN	PTR	ubuntusatu.com.
- nano named.conf.options
allow-query { any; };
forwarders {
  8.8.8.8;
};
dnssec-enable no;
dnssec-validation no;
- systemctl restart bind9
- nano /etc/netplan/50......
tambahkan
nameservers:
 addresses: [20.20.20.2]
- nslookup ubuntusatu.com

konfigurasi webmail 
- apt install mariadb-server
- apt install apache2
- apt install dovecot-imapd dovecot-pop3d postfix
pilih internet site
masukkan mail.debianlima.com
- dpkg-reconfigure postfix
pada force synchronous update pilih yes
tambahkan 0.0.0.0/0
pilih ipv4
- nano /etc/postfix/main.cf
tambahkan di paling bawah
home_mailbox = Maildir/
- nano /etc/dovecot/dovecot.conf
listen = *
- nano /etc/dovecot/conf.d/10-auth.conf
disable_plaintext_auth = no
-nano /etc/dovecot/conf.d/10-mail.conf
hapus # di mail_location = maildir:~/Maildir
dan beri tanda # di mail_location = mbox
- maildirmake.dovecot /etc/skel/Maildir
- systemctl restart postfix
- systemctl restart dovecot
- adduser tkjsatu
- adduser tkjdua
- mysql -u root -p
- grant all privileges on roundcube.* to tkj@mail.ubuntusatu.com identified by ‘tkj’;
- flush privileges;
- quit; 
- mencoba kirim mail dari tkjsatu ke tkjdua
telnet mail.ubuntusatu.com 25
mail from: tkjsatu@mail.ubuntusatu.com
rcpt to: tkjdua@mail.debianempat.com
data
coba lagi
.
quit
- melihat email dari tkjdua
telnet mail.ubuntusatu.com 110
user tkjdua
pass 2
retr 1
quit
- apt install roundcube
- nano /etc/roundcube/config.inc.php
masukkan domain dan ip serta hapus isi dari smtp user
- cd /etc/apache2/sites-available
- cp 000-default.conf webmail.conf
- nano webmail.conf
servername mail.ubuntusatu.com
documentroot /var/lib/roundcube
- a2ensite webmail.conf
- systemctl restart apache2
- systemctl restart postfix
- systemctl restart dovecot
- buka browser mail.ubuntusatu.com

konfigurasi proxy
- apt install squid3
- nano /etc/squid/squid.conf
pada cache_mgr ubah jadi ubuntusatu
http_access deny all ubah menjadi allow
visible_hostname tambahkan ubuntusatu
acl situs dstdomain "/etc/squid/situs.txt"
http_access deny situs
acl user src 40.40.40.0/24
http_access allow user
- nano /etc/squid/situs.txt
ubuntusatu.com
- systemctl restart squid

konfigurasi web dengan php
- apt install php
- nano .etcphp/7.2/apache2/php.ini
date.timezone = "Asia/Indonesia"
- systemctl restart apache2
- nano /var/www/html/index.php
- nano /etc/apache2/sites-available/utama.conf
ubah menjadi /var/www/html
- systemctl restart apache2

konfigurasi databases
- apt install mariadb-server
- mysql_secure_instalation
Set root password? [Y/n] y
New password:
Re-enter new password:
Remove anonymous users? [Y/n] y
Disallow root login remotely? [Y/n] y
Remove test database and access to it? [Y/n] y
Reload privilege tables now? [Y/n] y
- mysql -u root -p
Enter password:
# show user list
MariaDB [(none)]> select user,host,password from mysql.user;

konfigurasi dhcpserver
- apt install isc-dhcp-server
- nano /etc/dhcp/dhcpd.conf
option domain-name "ubuntusatu.com";
option domain-name-servers ubuntusatu.com;
hapus # pada authoritative;
- nano /etc/dhcp/dhcpd.conf
- # A slightly different configuration for an internal subnet.
subnet 50.50.50.0 netmask 255.255.255.0 {
  range 50.50.50.2 50.50.50.100;
  option domain-name-servers 20.20.20.2;
  option domain-name "ubuntusatu.com";
  option routers 50.50.50.1;
  option broadcast-address 50.50.50.101;
  default-lease-time 600;
  max-lease-time 7200;
}
- systemctl restart isc-dhcp-server

konfigurasi iptables nat
- apt install iptables-persistent
iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
- iptables-save > /etc/iptables/rules.v4

konfigurasi wordpress