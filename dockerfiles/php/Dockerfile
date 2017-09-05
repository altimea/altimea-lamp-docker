FROM php:7.0-fpm

ARG CONTAINER_USER=altimea

RUN apt-get update -y \
    && apt-get install -y php-soap libxml2-dev libpng-dev libjpeg62-turbo-dev libfreetype6-dev

RUN useradd -m ${CONTAINER_USER}

RUN sed -i "s/\user = www-data/user = ${CONTAINER_USER}/g" /usr/local/etc/php-fpm.d/www.conf
RUN sed -i 's/\group = www-data/group = users/g' /usr/local/etc/php-fpm.d/www.conf

RUN docker-php-ext-install pdo_mysql \
    && docker-php-ext-install json \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install soap \
    && docker-php-ext-install mysqli \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

