FROM php:7.4-apache

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

ENV APACHE_DOCUMENT_ROOT /app/src/public

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

RUN apt-get update -y && \
    apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libpq5 libpq-dev \
    libzip-dev libicu-dev g++ libxml2-dev && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-configure zip --with-libzip && \
    docker-php-ext-install pdo pgsql pdo_pgsql gd bcmath zip xmlrpc soap pcntl && \
    apt-get autoremove --purge -y libpq-dev; \
    apt-get clean ; \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN docker-php-ext-enable pdo_pgsql

RUN export TERM=xterm

RUN docker-php-ext-configure intl && docker-php-ext-install intl

RUN a2enmod rewrite

