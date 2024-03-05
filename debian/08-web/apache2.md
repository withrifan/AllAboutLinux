## Apache2 Web Server

install Apache2 in Debian

    apt install apache2
    apachectl -V

## Create VirtualHosts

virtualhost for domain example.id

    mkdir /var/www/example
    chown -R www-data:www-data /var/www/example
    nano /var/www/example/index.html
    cd /etc/apache2/sites-available/
    cp 000-default.conf example.conf
    nano example.conf

        <VirtualHost *:80>
            ServerAdmin admin@example.id
            ServerName example.id
            ServerAlias www.example.id
            DocumentRoot /var/www/example
        </VirtualHost>

    a2dissite 000-default.conf
    sudo a2ensite example.conf
    sudo systemctl reload apache2

## Apache Userdir

configure apache2 userdir

    a2enmod userdir
    adduser user1
    mkdir /home/user1/public_html
    nano /home/user1/public_html/index.html

check with

    http://example.id/~user1/

## Basic Authentication of HTTP users

add script in example.conf

    nano /etc/apache2/sites-available/example.conf

    <Directory /var/www/example>
    AuthType Basic
    AuthName "restricted"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
    </Directory>

add htpasswd for user rifan

    htpasswd -c /etc/apache2/.htpasswd rifan

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
