# docker php7 fpm redis

    Docker container to run php-fpm as a partner to a nginx container

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
    - redis client via pecl (not installed by default)
    - xdebug
  - installs composer
  - installs phpunit
  - installs git
  - expects a php-fpm instance to be running before it's started with an alais of php on port 9000
  - sets the default timezone to Europe/London via build/php.ini which is added to the container

## Build

  Use docker-compose in parent directory to launch
