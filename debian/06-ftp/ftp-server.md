konfigurasi ftp server anonymous

- apt install proftpd
- remote pakai filezila
- mkdir /ftpuser
- chmod 777 /ftpuser
- nano /etc/proftpd/proftpd.conf
- edit server name menjadi debiandua.com
- hapus # di default root dan edit directory /ftpuser
- systemctl restart proftpd
- nano /ftpuser/file.txt
- nano /etc/proftpd/proftpd.conf
- hapus # anonymous dan ~ ganti dengan /ftpuser
- hapus # user ftp dan group
- hapus # useralias anonymous ftp
- hapus # agar tidak butuh pengecekan yg valid
- # hapus didepannya </Anonymous>
- systemctl restart proftpd
- remote filezila tanpa user dan pass

konfigurasi ftp server

- apt install proftpd
- remote pakai filezila
- mkdir /ftpuser
- nano /ftpuser/file.txt
- chmod 777 /ftpuser
- nano /etc/proftpd/proftpd.conf
- edit server name menjadi debianempat.com
- ganti portnya 201 (opsional)
- hapus # di default root dan edit directory /ftpuser/
- hapus # pada <Anonymous /ftpuser>
- hapus # pada user dan group
- hapus # pada UserAlias
- hapus # pada RequireValidShell
- hapus # pada </Anonymous>
- systemctl restart proftpd

konfigurasi ftp

- apt install proftpd
- remote pakai filezila
- mkdir /ftpuser
- nano /ftpuser/file.txt
- chmod 777 /ftpuser
- nano /etc/proftpd/proftpd.conf
- edit server name menjadi debianempat.com (opsional)
- ganti portnya 21 (opsional)
- hapus # di default root dan edit directory /ftpuser/
- hapus # pada <Anonymous /ftpuser>
- hapus # pada user dan group
- hapus # pada UserAlias
- hapus # pada RequireValidShell
- hapus # pada </Anonymous>
- systemctl restart proftpd

konfigurasi ftp user auth (user A direktori A, user B direktori B)

- apt install vsftpd
- adduser ftptkj1
- chown nobody:nogroup /home/ftptkj1/
- chmod a-w /home/ftptkj1/
- ls -la /home/ftptkj1/
- nano /etc/vsftpd.conf
  anonymous_enable=NO
  local_enable=YES
  write_enable=YES
  chroot_local_user=YES
  user_sub_token=ftptkj1
  local_root=/home/ftptkj1/
  userlist_enable=YES
  userlist_file=/etc/vsftpd.userlist
  userlist_deny=NO
- systemctl restart vsftpd
