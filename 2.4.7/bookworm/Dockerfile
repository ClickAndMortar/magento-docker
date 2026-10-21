FROM php:8.3.7-fpm-bookworm AS php

ENV MAGE_MODE=production

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    libfreetype6-dev libicu-dev libjpeg62-turbo-dev libpng-dev libxslt1-dev libzip-dev libwebp-dev \
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-install -j$(nproc) bcmath gd intl pdo_mysql soap sockets xsl zip

# Composer épinglé et vérifié : SHA-256 recoupée entre getcomposer.org, la release GitHub et la signature GPG de Packagist.
ARG COMPOSER_VERSION=2.10.3
ARG COMPOSER_SHA256=7a2d379d5b8ffdaa028580ef26494c36d2feef4b178d3dd1473a4dbc5e17c8d6
RUN curl -fsSL -o /usr/local/bin/composer "https://getcomposer.org/download/${COMPOSER_VERSION}/composer.phar" \
    && echo "${COMPOSER_SHA256}  /usr/local/bin/composer" | sha256sum -c - \
    && chmod +x /usr/local/bin/composer

WORKDIR /app

COPY config/php/custom.ini /usr/local/etc/php/conf.d/90-magento.ini
COPY config/php/www.conf /usr/local/etc/php-fpm.d/www.conf
