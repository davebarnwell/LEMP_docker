FROM nginx
MAINTAINER Dave Barnwell <dave@freshsace.co.uk>

COPY build/default.conf   /etc/nginx/conf.d/default.conf

RUN mkdir -p /var/www/vhosts/cert
RUN mkdir -p /var/www/vhosts/site

COPY cert/server.crt     /var/www/vhosts/cert/server.crt
COPY cert/server.key     /var/www/vhosts/cert/server.key
COPY build/default.conf  /etc/nginx/conf.d/default.conf
COPY build/nginx.conf    /etc/nginx/nginx.conf


VOLUME /var/www/vhosts
WORKDIR /var/www/vhosts

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]