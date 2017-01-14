# docker-lemp-stack

## Install Docker and Docker Compose

	$ sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
	$ echo "deb https://apt.dockerproject.org/repo ubuntu-$(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/docker.list
	$ sudo apt-get update
	$ sudo apt-get install -y linux-image-extra-$(uname -r) docker-engine curl
	$ sudo sh -c "curl -L https://github.com/docker/compose/releases/download/1.5.1/docker-compose-$(uname -s)-$(uname -m) > /usr/local/bin/docker-compose"
	$ sudo chmod +x /usr/local/bin/docker-compose

Source docs:
- https://docs.docker.com/engine/installation/ubuntulinux/
- https://docs.docker.com/compose/install/

## Configure localization

### Ubuntu

	$ sudo locale-gen en_US.UTF-8
	$ echo "export LC_ALL=en_US.UTF-8" >> ~/.bashrc
	$ echo "export LANG=en_US.UTF-8" >> ~/.bashrc
	$ echo "export LANGUAGE=en_US.UTF-8" >> ~/.bashrc
	$ source ~/.bashrc
	$ sudo apt-get install -y ntp
	$ echo "Europe/Helsinki" | sudo tee /etc/timezone
	$ sudo dpkg-reconfigure -f noninteractive tzdata

## Configure firewall

	$ sudo ufw allow ssh
	$ sudo ufw allow http/tcp
	$ sudo ufw allow https/tcp
	$ sudo ufw default allow outgoing
	$ sudo ufw default deny incoming
	$ sudo ufw enable

## Automatic security updates

	$ sudo dpkg-reconfigure --priority=low unattended-upgrades

Source:
- https://help.ubuntu.com/community/AutomaticSecurityUpdates

## How to make mysqldump

	$ mysqldump -u <user> -p<pass> -h <host> <database> | gzip -9 > /home/niko/$(date +"%Y%m%d-%T")-db.sql.gz

## Restore database to mysql container

	$ sudo apt update && sudo apt install -y mysql-client
	$ mysql -u <user> -p<pass> -h $(sudo docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <mysql-container-name-or-if>) <database> < <mysqldump-filename>

## Deploy

Build kiuru/php:<tag>:

	$ sudo docker build -t kiuru/php:5.6.15-fpm images/php/.

Start docker containers on background:

	$ sudo docker-compose -f docker-compose.nikokiuru.yml up -d

Stop docker containers:

	$ sudo docker-compose -f docker-compose.nikokiuru.yml stop

If necessary, delete docker containers:

	$ sudo docker-compose -f docker-compose.nikokiuru.yml rm -v
