# Указывается исходный образ php-fpm, который используется как основа
FROM php:8.1.2-fpm

RUN apt-get update && apt-get install -y \
    wget \
    git \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    apt-utils \
    libpq-dev \
    libpng-dev \
    libzip-dev \
    zip unzip && \
    docker-php-ext-install pdo pdo_mysql && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install gd && \
    docker-php-ext-install zip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD ./_docker/app/php.ini etc/php/php.ini

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