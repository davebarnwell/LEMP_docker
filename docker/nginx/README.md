# docker nginx container

- Based on official nginx
- exposes port 80 and 443 (ssl)
- volume /var/www web root is one of
- /var/www/vhosts/site/public_html      (domain local.dev)
- expects a php-fpm instance to be running before it's started with an alias of php-fpm on port 9000
- sets the default host conf to build/default.conf which is added to the container

Use docker-compose in parent directory to launch
  
