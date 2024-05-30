FROM php:8.3.7-fpm-bookworm AS php

ENV MAGE_MODE=production

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    libfreetype6-dev libicu-dev libjpeg62-turbo-dev libpng-dev libxslt1-dev libzip-dev libwebp-dev \
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-install -j$(nproc) bcmath gd intl pdo_mysql soap sockets xsl zip

RUN curl -sSL https://getcomposer.org/download/latest-2.x/composer.phar -o /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer

WORKDIR /app

COPY config/php/custom.ini /usr/local/etc/php/conf.d/90-magento.ini
COPY config/php/www.conf /usr/local/etc/php-fpm.d/www.conf
