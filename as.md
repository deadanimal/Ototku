# Server configuration

## Requirement

Below are the minimum items required before doing any configuration

1. IP address 
2. Credentials(username/password) or keypair
3. VPN credentials to access private network
4. Items to be installed/configured: Laravel or Database
5. Subdomain or domain known to be pointed

## Step by step for Laravel

### Step 1: Install

```
adduser sammy
usermod -aG sudo sammy

sudo apt update
sudo apt install nginx
systemctl status nginx
sudo mkdir -p /var/www/your_domain/html
sudo chown -R $USER:$USER /var/www/your_domain/html
sudo chmod -R 755 /var/www/your_domain
sudo nano /etc/nginx/sites-available/your_domain
sudo ln -s /etc/nginx/sites-available/your_domain /etc/nginx/sites-enabled/
sudo systemctl restart nginx
```

```
server {
        listen 80;
        listen [::]:80;

        root /var/www/your_domain/html;
        index index.html index.htm index.nginx-debian.html;

        server_name your_domain.com www.your_domain;

        location / {
                try_files $uri $uri/ =404;
        }
}
```



```
sudo apt -y install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt -y install php7.4
sudo apt install curl php-cli php-mbstring php-curl git unzip
sudo apt-get install -y php7.4-cli php7.4-json php7.4-common php7.4-mysql php7.4-zip php7.4-gd php7.4-mbstring php7.4-curl php7.4-xml php7.4-bcmath
sudo mv composer.phar /usr/local/bin/composer
mv composer.phar ~/.local/bin/composer
composer --version
```

```
sudo nano hello.php

<?php
echo 'Hello World!';
?>

php hello.php
```


```
server {
    listen 80;
    server_name server_domain_or_IP;
    root /var/www/travel_list/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Content-Type-Options "nosniff";

    index index.html index.htm index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```