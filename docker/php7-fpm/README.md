# docker php7 fpm redis

    This container can be found pre-built on docker hub as freshsauce/cf-php7-fpm-redis
    https://registry.hub.docker.com/u/freshsauce/cf-php7-fpm-redis/

    It's designed to run php-fpm for a nginx container based on image freshsauce/nginx

  - Based on official php7 fpm build
  - exposes port 9000
  - volume /var/www web root is one of
    - /var/www/vhosts/site/public_html      (domain cf.dev)
    - /var/www/vhosts/api/public_html       (domain api.cf.dev)
    - /var/www/vhosts/payments/public_html  (domain payment.cf.dev)
  - installs pear
  - installs PHP with
    - gd
    - mbstring
    - iconv
    - mcrypt
    - pdo
    - pdo_mysql
    - mysql
    - redis client via pecl
    - xdebug
  - installs composer
  - installs phpunit
  - installs git
  - expects a php-fpm instance to be running before it's started with an alais of php on port 9000
  - sets the default timezone to Europe/London via build/php.ini which is added to the container

## Pull or build

    docker pull freshsauce/cf-php7-fpm-redis

  Or build under your own username on docker

    docker build -t username/cf-php7-fpm-redis .

## Run up with

    docker run --name php -v /host/web/html:/var/www/vhosts/site/public_html \
      --link redis:redis --link mysql:db -d username/cf-php7-fpm-redis

  - links to a mysql container aliased as db
  - links to a redis container aliased as redis
  - mounts host directory /host/web/html as /var/www/vhosts/site/public_html in the container
