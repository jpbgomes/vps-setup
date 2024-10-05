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

## Get The SSH Key
```
scp jpbgomes@192.168.1.237:/home/jpbgomes/.ssh/rpi_key .\.ssh\rpi_key
```

## Create Alias
```
  Host jpbgomes
  HostName 192.168.1.237
  User jpbgomes
  IdentityFile ~/.ssh/rpi_key
```
