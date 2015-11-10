# docker-lemp-stack

## Deploy

Build kiuru/php:<tag>:

	$ sudo docker build -t kiuru/php:5.6.15-fpm images/php/.

Start docker containers:

	$ sudo docker-compose up

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
