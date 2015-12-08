# docker-lemp-stack

## Install Docker and Docker Compose

	$ sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
	$ echo "deb https://apt.dockerproject.org/repo ubuntu-$(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/docker.list
	$ sudo apt-get update
	$ sudo apt-get install linux-image-extra-$(uname -r) docker-engine curl
	$ sudo sh -c "curl -L https://github.com/docker/compose/releases/download/1.5.1/docker-compose-$(uname -s)-$(uname -m) > /usr/local/bin/docker-compose"
	$ sudo chmod +x /usr/local/bin/docker-compose

Source docs:
- https://docs.docker.com/engine/installation/ubuntulinux/
- https://docs.docker.com/compose/install/

## Deploy

Build kiuru/php:<tag>:

	$ sudo docker build -t kiuru/php:5.6.15-fpm images/php/.

Start docker containers:

	$ sudo docker-compose up -d

Run test:

	$ curl -I http://localhost/index.html
	HTTP/1.1 200 OK
	Server: nginx/1.9.6
	Date: Mon, 09 Nov 2015 12:07:46 GMT
	Content-Type: text/html
	Content-Length: 20
	Last-Modified: Mon, 09 Nov 2015 11:51:13 GMT
	Connection: keep-alive
	ETag: "564088b1-14"
	Accept-Ranges: bytes

	$ curl -I http://localhost/index.php
	HTTP/1.1 200 OK
	Server: nginx/1.9.6
	Date: Mon, 09 Nov 2015 12:08:36 GMT
	Content-Type: text/html; charset=UTF-8
	Connection: keep-alive
	X-Powered-By: PHP/5.6.15

Stop docker containers:

	$ sudo docker-compose stop

If necessary, delete docker containers:

	$ sudo docker-compose rm -f
