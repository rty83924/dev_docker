FROM php:7.4-fpm

WORKDIR /www
RUN  apt-get update \
    && export CFLAGS="$PHP_CFLAGS" CPPFLAGS="$PHP_CPPFLAGS" LDFLAGS="$PHP_LDFLAGS" \
    && apt-get install -y --no-install-recommends libfreetype6-dev libjpeg62-turbo-dev libpng-dev libmagickwand-dev libmcrypt-dev libmemcached-dev zlib1g-dev \
    && rm -rf /var/lib/apt/lists/* \
    && mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini" \
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install -j$(nproc) bcmath calendar exif gettext sockets dba mysqli pcntl pdo_mysql shmop sysvmsg sysvsem sysvshm iconv gd \
    && pecl install mcrypt imagick-3.4.4 memcached-3.1.3 redis-5.0.2 swoole-4.4.3\
    && docker-php-ext-enable mcrypt imagick memcached redis swoole \
    && docker-php-ext-configure opcache --enable-opcache && docker-php-ext-install opcache 
