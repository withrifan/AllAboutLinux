# Apache2 Web Server
Install Apache2 in Ubuntu

    apt install apache2

## Apache2 Reverse Proxy

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
