# Docker based web development environment based on a LEMP stack (NGINX, PHP7, MariaDb)

Reusable web development containers running NGINX, PHP7 as fpm,
and MariaDb which is 100% compatible with MySQL.

You'll need to install [Docker on your machine](https://www.docker.com/community-edition#/download).

Then open a terminal to in LEMP_docker/ directory and run the following in the terminal

    docker-compose up

This first time builds then starts up a webserver instance on port 80 (HTTP)
and SSL on port 443 (HTTPS) using a self signed certificate, Mariadb and php-fpm v7 and
leaves the terminal window tailing the logs from all instances.

When your done CTRL-C closes it al down gracefully.

Second time on the command just restarts the containers if nothing changed in the Docker files
for the mages, if something has changed it will rebuild the images and containers.

When running in a web browser go to http://local.dev/ or http://127.0.0.1/ you'll need to be
resolving local.dev or *.dev to 127.0.0.1

checkout [dnsmasq](https://gist.github.com/davebarnwell/c408533d608bfe24f4f5)
to make your life easy and wild card *.dev.local to 127.0.0.1

Tweak domains, db usernames and passwords as required in the docker-compose.yml
and/or Docker files and files included from the build/ sub directories.

Containers created are prefixed with the parent directory name
eg. LEMP_docker becomes lempdocker_{contanerName}_1

e.g.

- lempdocker_web_1
- lempdocker_php_1
- lempdocker_mysql_1


## quick docker-compose commands

docker-compose when run applies it's actions to the containers as defined in the docker-compose.yml
file of the current directory

    docker-compose up -d          # Builds images if required and starts containers if not running
    docker-compose up -d --build  # Build images before starting containers
    docker-compose start          # Start containers, which must have been buiult previously
    docker-compose stop           # Stop containers
    docker-compose logs           # show logs from all containers
    docker-compose logs -f        # Tail logs from all containers CTRL-C to stop tailing
    
## Local file layout

- /Project-root           directory
    - docker-compose.yml  defines the container setup
    - /docker             The individual container build scripts
    - /public             website root directory for public assets etc
    - **/other_dirs**     Other directories you want your app to have access to, e.g. the code for