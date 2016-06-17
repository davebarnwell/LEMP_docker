FROM php:7-fpm
MAINTAINER Dave Barnwell <dave@freshsace.co.uk>

ENV TERM xterm

# Install modules (graphics, multi-byte string support etc..)
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install mbstring iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install sockets

# Install PDO mysql
RUN docker-php-ext-install pdo pdo_mysql mysqli

# Enable and configure xdebug
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
COPY build/xdebug.ini   /usr/local/etc/php/conf.d/xdebug.ini


# Install Redis
#ENV PHPREDIS_VERSION php7

# RUN curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz \
#     && tar xfz /tmp/redis.tar.gz \
#     && rm -r /tmp/redis.tar.gz \
#     && mv phpredis-$PHPREDIS_VERSION /usr/src/php/ext/redis \
#     && docker-php-ext-install redis

#RUN apt-get install -y php-pear php7.0-dev \
#    && pecl install redis \
#    && touch /usr/local/etc/php/conf.d/redis.ini \
#    && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini

RUN apt-get install -y wget curl vim

# Install git
RUN apt-get update && apt-get install -y git-core

# Install php tools (composer / phpunit)
RUN cd $HOME && \
    wget http://getcomposer.org/composer.phar && \
    chmod +x composer.phar && \
    mv composer.phar /usr/local/bin/composer && \
    wget https://phar.phpunit.de/phpunit.phar && \
    chmod +x phpunit.phar && \
    mv phpunit.phar /usr/local/bin/phpunit
RUN mkdir -p /var/www/vhosts
WORKDIR /var/www/vhosts
VOLUME /var/www/vhosts
COPY build/php.ini   /usr/local/etc/php/conf.d/php.ini
EXPOSE 9000
CMD ["php-fpm"]