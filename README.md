# docker-zoneminder-php7.4-mysql8
zoneminder-latest ,docker images with php 7.4 ,Mysql 8 &amp; MSMTP
Based on Iconnor's Zoneminder 
This image has been created on ubuntu:focal with zoneminder-latest/ubuntu focal main
To pull the Repository from the dockerhub
please refer the following link

https://hub.docker.com/repository/docker/bkjaya1952/docker-zoneminder-php7.4-mysql8


Usage :

To create a zoneminder- docker container (name zm)with php 7.4 ,mysql 8 & msmtp

On the Ubuntu terminal enter the following commands

<code>sudo docker create -t -p 8080:80 --shm-size=4096m --name zm --privileged=true bkjaya1952/docker-zoneminder-php7.4-mysql8:latest</code>

<code>sudo docker start zm</code>

(You will have to configure the running zm container for mysql 8 ,zm data base and make some changes to start apache and zoneminder during the first run .)

<code>sudo docker exec -t -i zm /bin/bash</code>

(Now  you will be with in the zm container.

Make changes as follows)

(Configuring Mysql )

<code>firstrun.sh</code>

The press Enter Key when password prompts apear twice

Then edit your timezone

Enter your  timezone details when prompts apear

<code>exit</code>

<code>sudo docker restart zm</code>

<code>http://localhost:8080/zm/</code>

(To use msmtp for emailing please refer https://hub.docker.com/repository/docker/bkjaya1952/docker-zoneminder-master)

( The procedure of  composing an image can be obtained from the following links

https://bkjaya.wordpress.com/2020/01/15/how-to-build-a-zoneminder-master-docker-image-with-mysql-8-msmtp/  )

# Note:- If you want your docker container zm to detect ip camera automatically, you will have to use the following command when creating the container .

<code>sudo docker create -t -p 80:80 --shm-size=4096m --name zm --network=host --privileged=true bkjaya1952/docker-zoneminder-php7.4-mysql8:latest</code>

In this case you will have to restrain in using the port 80 in your host for any other purpose when running the zm container.

Then the zoneminder web panel will be at <code>http://localhost/zm/</code>






