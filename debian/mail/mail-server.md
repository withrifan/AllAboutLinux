konfigurasi webmail

- apt install php mariadb-server
- apt install apache2
- apt install dovecot-imapd dovecot-pop3d postfix
  pilih internet site
  masukkan mail.debiantiga.com
- dpkg-reconfigure postfix
  pada force synchronous update pilih yes
  tambahkan 0.0.0.0/0
  pilih ipv4
- nano /etc/postfix/main.cf
  tambahkan di paling bawah
  home_mailbox = Maildir/
- nano /etc/dovecot/dovecot.conf
  listen = \*
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
- grant all privileges on roundcube.\* to tkj@mail.debiantiga.com identified by ‘tkj’;
- flush privileges;
- quit;
- apt install roundcube
- nano /etc/roundcube/config.inc.php
  masukkan domain dan ip serta hapus isi dari smtp user
- cd /etc/apache2/sites-available
- cp 000-default.conf webmail.conf
- nano webmail.conf
  servername mail.debiantiga.com
  documentroot /var/lib/roundcube
- a2ensite webmail.conf
- systemctl restart apache2
- systemctl restart postfix
- systemctl restart dovecot
- buka browser mail.debiantiga.com

konfigurasi webmail

- apt install mariadb-server
- apt install apache2
- apt install dovecot-imapd dovecot-pop3d postfix
  pilih internet site
  masukkan mail.debianempat.com
- dpkg-reconfigure postfix
  pada force synchronous update pilih yes
  tambahkan 0.0.0.0/0
  pilih ipv4
- nano /etc/postfix/main.cf
  tambahkan di paling bawah
  home_mailbox = Maildir/
- nano /etc/dovecot/dovecot.conf
  listen = \*
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
- apt install roundcube
- mysql -u root -p
- grant all privileges on roundcube.\* to tkj@mail.debianempat.com identified by ‘tkj’;
- flush privileges;
- quit;
- mencoba kirim mail dari tkjsatu ke tkjdua
  telnet mail.debianempat.com 25
  mail from: tkjsatu@mail.debianempat.com
  rcpt to: tkjdua@mail.debianempat.com
  data
  coba lagi
  .
  quit
- melihat email dari tkjdua
  telnet mail.debianempat.com 110
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
  servername mail.debianempat.com
  documentroot /var/lib/roundcube
- a2ensite webmail.conf
- systemctl restart apache2
- systemctl restart postfix
- systemctl restart dovecot
- buka browser mail.debianempat.com

konfigurasi webmail

- apt install mariadb-server
- apt install postfix courier-imap courier-pop
  pilih internet site
  masukkan mail.debianlima.com
- maildirmake.dovecot /etc/skel/Maildir
- dpkg-reconfigure postfix
  pada force synchronous update pilih yes
  tambahkan 0.0.0.0/0
  pilih ipv4
- nano /etc/postfix/main.cf
  tambahkan di paling bawah
  home_mailbox = Maildir/
- nano /etc/dovecot/dovecot.conf
  listen = \*
- nano /etc/dovecot/conf.d/10-auth.conf
  disable_plaintext_auth = no
  -nano /etc/dovecot/conf.d/10-mail.conf
  hapus # di mail_location = maildir:~/Maildir
  dan beri tanda # di mail_location = mbox
- systemctl restart postfix
- systemctl restart courier
- adduser tkjsatu
- adduser tkjdua
- mysql -u root -p
- grant all privileges on roundcube.\* to tkj@mail.debianlima.com identified by ‘tkj’;
- flush privileges;
- quit;
- mencoba kirim mail dari tkjsatu ke tkjdua
  telnet mail.debianempat.com 25
  mail from: tkjsatu@mail.debianempat.com
  rcpt to: tkjdua@mail.debianempat.com
  data
  coba lagi
  .
  quit
- melihat email dari tkjdua
  telnet mail.debianempat.com 110
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
  servername mail.debiantiga.com
  documentroot /var/lib/roundcube
- a2ensite webmail.conf
- systemctl restart apache2
- systemctl restart postfix
- systemctl restart courier
- buka browser mail.debianenam.com
