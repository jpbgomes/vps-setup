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

sudo apt install -y php8.3 php8.3-cli php8.3-fpm php8.3-mysql php8.3-xml php8.3-mbstring php8.3-curl php8.3-zip
php -v
```

### Enable PHP-FPM
```
sudo systemctl start php8.3-fpm
sudo systemctl enable php8.3-fpm
```

## Install Composer

[Link to Documentation](https://getcomposer.org/download/)
