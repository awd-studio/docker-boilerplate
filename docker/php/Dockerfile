FROM php:7.3-fpm

RUN apt-get update -qq && apt-get install -yqq \
    g++ \
    git \
    libxml2-dev \
    libicu-dev \
    libcurl4-gnutls-dev \
    libmcrypt-dev \
    libjpeg-dev \
    libpng-dev \
    libzip-dev \
    zip \
    zlib1g-dev \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-source extract \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && docker-php-source delete \
    && docker-php-ext-install opcache pdo_mysql soap intl zip \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_port=10000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_connect_back=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && rm -rf /tmp/*

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

CMD ["php-fpm", "-F"]

WORKDIR /var/www/app

EXPOSE 9000
