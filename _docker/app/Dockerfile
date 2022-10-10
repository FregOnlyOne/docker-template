# Указывается исходный образ php-fpm, который используется как основа
FROM php:8.1.2-fpm

RUN apt-get update && apt-get install -y \
    curl \
    wget \
    git \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev

RUN docker-php-ext-install pdo pdo_mysql

COPY ./_docker/app/php.ini /usr/local/etc/php/conf.d/php.ini

# Указывается рабочая директория для PHP
WORKDIR /var/www

# Устанавливается composer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- \
    --filename=composer \
    --install-dir=/usr/local/bin

# Запускаем контейнер
# Из документации: The main purpose of a CMD is to provide defaults for an executing container. These defaults can include an executable, 
# or they can omit the executable, in which case you must specify an ENTRYPOINT instruction as well.
CMD ["php-fpm"]