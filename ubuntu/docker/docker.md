###Mikrotik###
ether1 nat ether2 intnet(registry) ether3 intnet2(client)
intnet = 192.168.10.1/30
intnet2 = 192.168.20.1/30

###docker registry###

atur ip address
- sudo nano /etc/netplan/01-network-manager-all.yaml 
network:
    version: 2
    renderer: NetworkManager
- sudo netplan apply

install docker
- sudo apt update
- sudo apt install apt-transport-https ca-certificates curl software-properties-common
- curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
- sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
- sudo apt update
- apt-cache policy docker-ce
- sudo apt install docker-ce
- sudo systemctl status docker

menjalankan docker tanpa sudo
- docker (masuk ke docker)
- sudo usermod -aG docker rifan
- su - rifan (masukkan password)
- id -nG (mengecek user sudah masuk grub)

install docker-compose
- curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-Linux-x86_64' -o /usr/local/bin/docker-compose
- chmod -x /usr/bin/docker-compose
- docker-compose -v

install nginx
- apt install nginx
- ufw allow 'Nginx HTTPS'

install let's encrypt nginx (SSL)
-

###docker client###
atur ip
network:
 ethernets:
  enp0s3:
   addresses: [192.168.20.2/30]
   gateway4: 192.168.20.1
   nameservers:
    addresses: [8.8.8.8]
   dhcp4: no
   optional: true
 version: 2
- netplan apply

install docker
- apt update
- apt install apt-transport-https ca-certificates curl software-properties-common
- curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
- add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable
- apt update
- apt-cache policy docker-ce
- apt install docker-ce
- systemctl status docker-ce

menjalankan docker tanpa sudo
- docker (masuk ke docker)
- sudo usermod -aG docker tkj
- su - tkj (masukkan password)
- id -nG (mengecek user sudah masuk grub)


###jika tidak bisa install aplikasi###
- sudo kill -9 <process_id>
- sudo rm /var/lib/apt/lists/lock
- sudo rm /var/cache/apt/archives/lock
- sudo rm /var/lib/dpkg/lock
- sudo dpkg --configure -a
- apt update



