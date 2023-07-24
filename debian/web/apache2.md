## Apache2 Web Server

Install Apache2 in Ubuntu

    apt install apache2

## VirtalHost

    mkdir -p /var/www/your_domain
    sudo chown -R $USER:$USER /var/www/your_domain
    sudo chmod -R 755 /var/www/your_domain
    nano /var/www/your_domain/index.html

    sudo nano /etc/apache2/sites-available/your_domain.conf
        <VirtualHost *:80>
            ServerAdmin admin@your_email_domain
            ServerName your_domain
            ServerAlias www.your_domain
            DocumentRoot /var/www/your_domain
            ErrorLog ${APACHE_LOG_DIR}/error.log
            CustomLog ${APACHE_LOG_DIR}/access.log combined
        </VirtualHost>

## virtual webpage user11-20##

apt install apache2
mkdir /home/user11/public_html
mkdir /home/user12/public_html
mkdir /home/user13/public_html
mkdir /home/user14/public_html
mkdir /home/user15/public_html
mkdir /home/user16/public_html
mkdir /home/user17/public_html
mkdir /home/user18/public_html
mkdir /home/user19/public_html
mkdir /home/user20/public_html
a2enmod userdir
(jika error UTF
export LANGUAGE=en_US.UTF-8
export LC_ALL=en_US.UTF-8
)
systemctl restart apache2
apt install w3m
w3m http://smkbisa.net/~user11/

## httpasswd

##internal.smkbisa.net dengan authentikasi##
cd /etc/apache2/sites-available/
cp 000-default.conf internal.conf
cp default-ssl.conf internal-ssl.conf
mkdir /var/www/internal
nano index.html
nano internal.conf
ServerName internal.smkbisa.net
ServerAdmin webmaster@smkbisa.net
DocumentRoot /var/www/internal
<Directory /var/www/internal>
AuthType Basic
AuthName "Masukkan username dan password"
AuthUserFile /etc/apache2/htpasswd
Require valid-user
</Directory>
nano internal-ssl.conf
ServerAdmin webmaster@smkbisa.net
DocumentRoot /var/www/internal
<Directory /var/www/internal>
AuthType Basic
AuthName "Masukkan username dan password"
AuthUserFile /etc/apache2/htpasswd
Require valid-user
</Directory>
touch /etc/apache2/htpasswd
htpasswd -b /etc/apache2/htpasswd user1 smkbisa
htpasswd -b /etc/apache2/htpasswd user2 smkbisa
htpasswd -b /etc/apache2/htpasswd user3 smkbisa
htpasswd -b /etc/apache2/htpasswd user4 smkbisa
htpasswd -b /etc/apache2/htpasswd user5 smkbisa
htpasswd -b /etc/apache2/htpasswd user6 smkbisa
htpasswd -b /etc/apache2/htpasswd user7 smkbisa
htpasswd -b /etc/apache2/htpasswd user8 smkbisa
htpasswd -b /etc/apache2/htpasswd user9 smkbisa
htpasswd -b /etc/apache2/htpasswd user10 smkbisa
systemctl restart apache2

## Reverse Proxy

    a2enmod proxy
    a2enmod proxy_http

Edit sites-available

     ProxyPreserveHost on
        ProxyRequests off
        ProxyPass / http://localhost:3000/
        ProxyPassReverse / http://localhost:3000/
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/a387-jarkom-labs

Edit ports.conf

     Listen 80
     <IfModule ssl_module>
        Listen 443
    </IfModule>
    <IfModule mod_gnutls.c>
        Listen 443
    </IfModule>

## Webmail

konfigurasi web server

- apt install apache2
- ls /etc/apache2/sites-available/
- cp 000-default.conf webmail.conf
- nano webmail.conf
- ubah servername, ganti /var/www/index.html /var/lib/roundcube
- a2ensite webmail.conf
- systemctl restart apache2

konfigurasi web

- apt install apache2
- cd /etc/apache2/sites-available
- cp 000-default.conf website.conf
- nano website.conf
  servername www.debianenam.com
  serveradmin webmaster@debianenam.com
  documentroot /var/www/web
- mkdir/var/www/web/
- nano index.html
- cd /etc/apache2/sites-available
- a2ensite website.conf
- systemctl restart apache2

## Restart Apache2

    sudo a2ensite your_domain.conf
    sudo a2dissite 000-default.conf
    sudo service apache2 restart
    sudo systemctl restart apache2
    sudo /etc/init.d/apache2 restart

### Opsional

Install Node with nvm

    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
    exit
    nvm install v14.15.4
    node --version
    npm run start
