# Qucik start docker dev env

in LEMP_docker/ run in the terminal

    docker-compose up

This first time builds then starts up a nginx instance 80 and SSL on 443, Mariadb and php-fpm v7 and leaves the terminal window tailing the logs from all instances. When your done CTRL-C closes it al down gracefully. Second time on the command just restarts the containers if nothing changed in the Docker files for the mages, if something has changed it will rebuild the images and containers.

When running in a web browser go to http://local.dev/ or http://127.0.0.1/ you'll need to be resolving local.dev or *.dev to 127.0.0.1 checkout [dnsmasq](https://gist.github.com/freshsauce/c408533d608bfe24f4f5) to wild card this.

Tweak domains, and db usernames and passwords as required in the Docker files and files inclued from the build/ sub directories.

Containers created are prefixed with the parent directory name eg. LEMP_docker becomes lempdocker_{contanerName}_1

e.g.

- lempdocker_web_1
- lempdocker_php_1
- lempdocker_mysql_1
