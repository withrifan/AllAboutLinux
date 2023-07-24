konfigurasi samba server

- apt install samba
- nano /etc/samba/smb.conf
  [public]
  path = /samba/public
  browseable = yes
  writeable = no
  security = share
  guest ok = yes
  read only = yes

[data]
path = /samba/data
browseable = yes
writeable = yes
security = user
valid user = tkj
guest ok = no
read only = no

- smbpasswd -a tkj
- mkdir /samba
- mkdir /samba/public
- mkdir /samba/data
- chmod -R 777 /samba/
- nano /samba/public/file-percobaan.txt
- systemctl restart smbd

konfigurasi samba server

- apt install samba
- mkdir /samba
- mkdir /samba/public
- mkdir /samba/data
- chmod -R 777 /samba/
- smbpasswd -a tkj
- nano /etc/samba/smb.conf
  [public]
  path = /samba/public
  browseable = yes
  writeable = yes
  security = share
  guest ok = yes
  read only = no

[data]
path = /samba/data
browseable = yes
writeable = no
security = user
valid user = tkj
guest ok = no
read only = yes
#melarang file bertipe html
veto files =\*html

- nano /samba/public/file-percobaan.txt
- systemctl restart smbd
- remote dari client smb://192.168.10.2

konfigurasi samba

- apt install samba
- mkdir /samba
- mkdir /samba/public
- mkdir /samba/data
- chmod -R 777 /samba/
- smbpasswd -a tkj
- nano /etc/samba/smb.conf
  [public]
  path = /samba/public
  browseable = yes
  writeable = yes
  security = share
  guest ok = yes
  read only = no

[data]
path = /samba/data
browseable = yes
writeable = no
security = user
valid user = tkj
guest ok = no
read only = yes
#melarang file bertipe html
veto files =\*html

- nano /samba/public/file-percobaan.txt
- systemctl restart smbd
- remote dari client smb://192.168.10.2
