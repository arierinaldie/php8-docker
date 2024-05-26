# base image
FROM php:8.3-fpm-alpine

# supervisor git
RUN apk add --no-cache supervisor git \
&& docker-php-ext-install ftp exif shmop bcmath pcntl calendar \
# opcache
&& docker-php-ext-install opcache \
# pdo_mysql mysqli
&& docker-php-ext-install pdo_mysql mysqli \
# pdo_pgsql pgsql
&& apk add --no-cache libpq-dev \
&& docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
&& docker-php-ext-install pdo_pgsql pgsql \
# sockets
&& apk add --no-cache linux-headers \
&& docker-php-ext-install sockets \
# gd
&& apk add --no-cache zlib-dev libpng-dev libjpeg-turbo-dev freetype-dev \
&& docker-php-ext-configure gd --with-freetype --with-jpeg \
&& docker-php-ext-install gd \
# zip
&& apk add --no-cache libzip-dev \
&& docker-php-ext-install zip \
# intl
&& apk add --no-cache icu-dev \
&& docker-php-ext-install intl \
# extract source for manual install
&& docker-php-source extract \
# apcu
&& mkdir -p /usr/src/php/ext/apcu \
&& curl -fsSL https://pecl.php.net/get/apcu-5.1.23.tgz | tar xvz -C /usr/src/php/ext/apcu --strip 1 \
&& docker-php-ext-install apcu \
# redis
&& mkdir -p /usr/src/php/ext/redis \
&& curl -fsSL https://pecl.php.net/get/redis-6.0.2.tgz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
&& docker-php-ext-install redis \
# memcached
&& apk add --no-cache libmemcached-dev \
&& mkdir -p /usr/src/php/ext/memcached \
&& curl -fsSL https://pecl.php.net/get/memcached-3.2.0.tgz | tar xvz -C /usr/src/php/ext/memcached --strip 1 \
&& docker-php-ext-install memcached \
# imagick
&& apk add --no-cache imagemagick-dev \
&& mkdir -p /usr/src/php/ext/imagick \
&& curl -fsSL https://pecl.php.net/get/imagick-3.7.0.tgz | tar xvz -C /usr/src/php/ext/imagick --strip 1 \
&& docker-php-ext-install imagick \
# igbinary
&& mkdir -p /usr/src/php/ext/igbinary \
&& curl -fsSL https://pecl.php.net/get/igbinary-3.2.15.tgz | tar xvz -C /usr/src/php/ext/igbinary --strip 1 \
&& docker-php-ext-install igbinary \
# ssh2
&& apk add --no-cache libssh2-dev \
&& mkdir -p /usr/src/php/ext/ssh2 \
&& curl -fsSL https://pecl.php.net/get/ssh2-1.4.1.tgz | tar xvz -C /usr/src/php/ext/ssh2 --strip 1 \
&& docker-php-ext-install ssh2 \
# xmlrpc
&& apk add --no-cache libxml2-dev \
&& mkdir -p /usr/src/php/ext/xmlrpc \
&& curl -fsSL https://github.com/php/pecl-networking-xmlrpc/archive/refs/tags/xmlrpc-1.0.0RC3.tar.gz | tar xvz -C /usr/src/php/ext/xmlrpc --strip 1 \
&& docker-php-ext-install xmlrpc \
# amqp
&& apk add --no-cache rabbitmq-c-dev \
&& mkdir -p /usr/src/php/ext/amqp \
&& curl -fsSL https://pecl.php.net/get/amqp-2.1.2.tgz | tar xvz -C /usr/src/php/ext/amqp --strip 1 \
&& docker-php-ext-install amqp \
# mongodb
&& mkdir -p /usr/src/php/ext/mongodb \
&& curl -fsSL https://pecl.php.net/get/mongodb-1.19.0.tgz | tar xvz -C /usr/src/php/ext/mongodb --strip 1 \
&& docker-php-ext-install mongodb \
# just clean up
&& docker-php-source delete \
&& rm -rf /var/cache/apk/* /tmp/*

ENV COMPOSER_HOME /composer
ENV COMPOSER_ALLOW_SUPERUSER 1

# composer
RUN cd ~ \
&& curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

# supervisor
COPY ./supervisord.conf /etc
RUN mkdir -p /var/log/supervisor /etc/supervisor /etc/supervisor/conf.d
EXPOSE 9001

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
