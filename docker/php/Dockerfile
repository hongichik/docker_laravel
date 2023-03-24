FROM php:8.1.12-fpm

RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    nano \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    unzip \
    git \
    zip \
    libwebp-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libxpm-dev \
    libfreetype6-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath zip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j "$(nproc)" gd \
    && pecl install redis \
    && docker-php-ext-enable redis

COPY php.ini /usr/local/etc/php/

WORKDIR /var/www/html


CMD ["php-fpm"]

EXPOSE 8000 8001 9000

