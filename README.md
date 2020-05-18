# docker-zoneminder-1.34-php7.4-mysql8-latest
zoneminder-1.34 ,docker images with php 7.4 ,Mysql 8 &amp; MSMTP

This image has been created on ubuntu:focal with zoneminder-1.34/ubuntu focal main
To pull the Repository from the dockerhub
please refer the following link

https://hub.docker.com/r/bkjaya1952/docker-zoneminder-master-php7.4-mysql8


Usage :

To create a zoneminder-1.34 docker container (name zm)with php 7.4 ,mysql 8 & msmtp

On the Ubuntu terminal enter the following commands

<code>sudo docker create -t -p 8080:80 --shm-size=4096m --name zm --privileged=true bkjaya1952/docker-zoneminder-master-php7.4-mysql8:latest</code>

<code>sudo docker start zm</code>

(You will have to configure the running zm container for mysql 8 ,zm data base and make some changes to start apache and zoneminder during the first run .)

<code>sudo docker exec -t -i zm /bin/bash</code>

(Now  you will be with in the zm container.

Make changes as follows)

<code>mysql -uroot -p < /usr/share/zoneminder/db/zm_create.sql</code>

<code>mysql</code>

<code>CREATE USER 'zmuser'@localhost IDENTIFIED WITH mysql_native_password BY 'zmpass';</code>

<code>GRANT ALL PRIVILEGES ON zm.* TO 'zmuser'@'localhost' WITH GRANT OPTION;</code>

<code>FLUSH PRIVILEGES ;</code>

<code>quit</code>

<code>mysqladmin -uroot -p reload</code>


<code>dpkg-reconfigure tzdata</code>

Then edit your timezone in the system

Then edit your time zone at /etc/php/7.4/apache2/php.ini

<code>sed -i "961i date.timezone = Asia/Colombo" /etc/php/7.4/apache2/php.ini</code>        ( ie. Asia/Colombo )


<code>exit</code>

<code>sudo docker restart zm</code>

<code>http://localhost:8080/zm/</code>

(To use msmtp for emailing please refer https://hub.docker.com/repository/docker/bkjaya1952/docker-zoneminder-master)

( The procedure of  composing an image can be obtained from the following links

https://bkjaya.wordpress.com/2020/01/15/how-to-build-a-zoneminder-master-docker-image-with-mysql-8-msmtp/  )

# Note:- If you want your docker container zm to detect ip camera automatically, you will have to use the following command when creating the container .

<code>sudo docker create -t -p 80:80 --shm-size=4096m --name zm --network=host --privileged=true bkjaya1952/docker-zoneminder-master-php7.4-mysql8:latest</code>

In this case you will have to restrain in using the port 80 in your host for any other purpose when running the zm container.

Then the zoneminder web panel will be at <code>http://localhost/zm/</code>






