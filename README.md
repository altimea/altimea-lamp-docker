# Altimea LAMP Docker

Official Docker images set up to be used within our company's projects while developing.

## What comes with it?

* PHP-FPM 7.0 (separate container)
* Apache 2.4 (separate container)
* MySQL 5.7 (separate container): With the external connection turned on and default user/password root/root

The containers are linked internally, so if you are configuring a database conection string in your project, you should put the database URL as "mysql" which is resolved to an internal IP inside docker containers.

## Dependencies

* docker
* docker-compose

## Optional dependencies

* Linux (Gnome):
	* Docker Manager for Gnome Shell: https://github.com/faidoc/gnome-shell-extension-docker
		* This will allow you to start/stop the docker service, and manage some basic things of your containers like starting/stopping or open a terminal inside the container.

## Starting point

* You need to create a copy of the .env.example file and name it .env. In this file you have to put your current user name. Docker will create an user with that exact name inside the containers for you to and your containers to be able to write and read to your project's files.
* Open ***volumes/apache/conf/httpd.conf*** and change User and Group to your current user.
* Create a virtual host and place it on ***volumes/apache/conf/vhosts*** it will automatically loaded.
* Open a terminal inside this repo root folder and run docker-compose
	* ***Considerations***
		* Docker Compose as it is configured right now, creates a volume with the content of its parent directory.

```docker-compose up -d```
* Done! You now have a LAMP environment

### Creating new virtualhosts

* Just put a new virtual host inside ***volumes/apache/conf/vhosts*** and restart the apache container

### Other commands

* Stop and remove containers: ```docker-compose down```

### TODO

* Allow to configure user and group ID, because it can happen that the user created inside the docker container has an ID different from your real user. 