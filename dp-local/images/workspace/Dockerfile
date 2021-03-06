FROM php:7.2-fpm

LABEL name="DP Workspace" \
    vendor="delivery-parts.ru"

RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        ssh-client \
        curl \
        libmemcached-dev \
        libz-dev \
        libpq-dev \
        libjpeg-dev \
        libpng-dev \
        libzip-dev \
        libfreetype6-dev \
        libssl-dev \
        libmcrypt-dev \
        zlib1g-dev \
        libicu-dev \
        g++ \
        jpegoptim \
        optipng \
        pngquant \
        gifsicle \
        libmagickwand-dev \
        imagemagick \
        librabbitmq-dev \
        git \
        nano \
        ca-certificates \
        wget \
        ssh-client \
        iputils-ping \
    && apt-get clean

# Image Magic
RUN pecl install imagick \
    && docker-php-ext-enable imagick

# MongoDB
RUN pecl channel-update pecl.php.net \
    && pecl install mongodb \
    && docker-php-ext-enable mongodb

# Redis
RUN printf "\n" | pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis

RUN pecl install amqp \
    && docker-php-ext-enable amqp \
    && docker-php-ext-install sockets

# PHP extensions
RUN docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-install pgsql \
    && docker-php-ext-configure gd \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2 \
    && docker-php-ext-install gd \
    && docker-php-ext-configure zip \
        --with-libzip \
    && docker-php-ext-install zip \
    && docker-php-ext-install bcmath \
    && docker-php-ext-configure intl \
    && docker-php-ext-install opcache \
    && docker-php-ext-install intl

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
