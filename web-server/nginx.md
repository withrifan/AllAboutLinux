# NGINX Web Server
Install NGINX in Ubuntu

    sudo apt install nginx

## NGINX Reverse Proxy
Edit sites-available

    location / {
        proxy_pass http://localhost:8000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
       }

Delete script 

    try_files $uri $uri/ =404;

## Limit Request
10req/mnt or 1req/6s

    limit_req_zone $binary_remote_addr zone=one:10m rate=10r/m;
    
    location / {
        limit_req zone=one;
    }

## Restart NGINX
    sudo systemctl restart nginx
    sudo service nginx restart
    sudo /etc/init.d/nginx restart

### Opsional
Install Node with nvm

    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
    exit
    nvm install v14.15.4
    node --version
    npm run start
