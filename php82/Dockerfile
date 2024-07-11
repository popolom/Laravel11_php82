FROM php:8.2-apache

RUN set -ex apk --no-cache add postgresql-dev libpq-dev && \
    apt-get update && apt-get install -y \
    less \
    libpq-dev \
    postgresql \
    && docker-php-ext-install \
    pdo \
    pdo_pgsql \
    pgsql

RUN apt-get install -y git

RUN apt-get update
RUN apt-get -y install \
    libzip-dev \
    zip
RUN docker-php-ext-install zip

RUN apt-get update && apt-get install -y \
  libssl-dev \
  openssl

RUN pecl install xdebug \
  && docker-php-ext-enable xdebug

# ドキュメントルートを変更する
ENV APACHE_DOCUMENT_ROOT='/var/www/public/'
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

RUN a2enmod rewrite

COPY php.ini /usr/local/etc/php/

WORKDIR /workspace