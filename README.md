# VPS SETUP


## Install SSH
```
sudo apt install openssh-server
```

```
pwd
cd ~
mkdir .ssh
sudo chmod 700 .ssh
cd .ssh
ssh-keygen -t rsa -b 4096 -f rpi_key
cat rpi_key.pub >> authorized_keys
```

### Get The SSH Key
```
scp jpbgomes@192.168.1.237:/home/jpbgomes/.ssh/rpi_key .\.ssh\rpi_key
```

### Create Alias
```
Host jpbgomes
HostName 192.168.1.237
User jpbgomes
IdentityFile ~/.ssh/rpi_key
```

## Install PHP
```
sudo apt update

sudo apt install -y lsb-release apt-transport-https ca-certificates
sudo wget -qO - https://packages.sury.org/apt.gpg | sudo apt-key add -
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/php.list

sudo apt install -y php8.3 php8.3-cli php8.3-fpm php8.3-mysql php8.3-xml php8.3-mbstring php8.3-curl php8.3-zip php8.3-bcmath libapache2-mod-php
php -v
```

### Enable PHP-FPM
```
sudo systemctl start php8.3-fpm
sudo systemctl enable php8.3-fpm
```

## Install Composer

[Link to Documentation](https://getcomposer.org/download/)

## Install MySQL
```
sudo apt install mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

## Create New User && Secure Installation
```
CREATE USER 'jpbgomes'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON *.* TO 'jpbgomes'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
EXIT;
```

```
sudo mysql_secure_installation
```


## Apache2
```
sudo apt install apache2
```
```
sudo nano /etc/apache2/sites-available/jpbgomes.conf
```
```
<VirtualHost *:80>
    ServerName jpbgomes.com
    ServerAlias www.jpbgomes.com
    DocumentRoot /var/www/jpbgomes/public

    <Directory /var/www/jpbgomes>
        AllowOverride All
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/jpbgomes.log
    CustomLog ${APACHE_LOG_DIR}/jpbgomes.log combined
</VirtualHost>
```
```
sudo a2ensite jpbgomes.conf
sudo systemctl restart apache2
```

Fix Permissions
```
sudo chown -R www-data:www-data /var/www/jpbgomes
sudo chmod -R 755 /var/www/jpbgomes
```
## Certbot
```
sudo apt update
sudo apt install certbot python3-certbot-apache
```

```
sudo certbot --apache -d jpbgomes.com -d www.jpbgomes.com
```
