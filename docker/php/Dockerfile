FROM php:7.1.16-fpm


RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libcurl4-openssl-dev \
        libssl-dev \
        libicu-dev \
        libxslt-dev \
        libexif-dev \
        libmemcached-dev  \
        openssl \
        zlib1g-dev \
        wget  \
    && docker-php-ext-install sockets \
    && docker-php-ext-install curl iconv mcrypt mbstring mysqli pdo pdo_mysql zip opcache \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-configure bcmath \
    && docker-php-ext-install bcmath \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-configure xsl \
    && docker-php-ext-install xsl \
    && pecl install apcu \
    && pecl install xdebug-2.6.0 \
    && docker-php-ext-enable  opcache apcu \
    && docker-php-ext-enable xdebug

RUN docker-php-ext-install exif
RUN docker-php-ext-configure exif \
            --enable-exif

RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl

    # create symlink to support standard /usr/bin/php
RUN ln -s /usr/local/bin/php /usr/bin/php

RUN apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin && mv /usr/local/bin/composer.phar /usr/local/bin/composer \
    && php -r "unlink('composer-setup.php');"

WORKDIR "/var/www/html"