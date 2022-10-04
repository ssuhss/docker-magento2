FROM php:8.1.5-fpm

COPY --from=composer:2.2.9 /usr/bin/composer /usr/local/bin/composer

RUN pecl install xdebug && docker-php-ext-enable xdebug

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y -qq libjpeg62-turbo-dev libpng-dev libxml2-dev libxslt-dev libsodium-dev libzip-dev libfreetype6-dev
RUN docker-php-ext-configure gd --with-freetype --with-jpeg

RUN apt-get install -y git unzip \
                           libfreetype6-dev \
                           libjpeg62-turbo-dev \
                           libxml2-dev \
                           libxslt1-dev

RUN docker-php-ext-install pdo \
    pdo_mysql \
    gd \
    bcmath \
    intl \
    xsl \
    soap \
    sockets \
    simplexml

RUN apt-get install -y \
            libzip-dev \
            zip \
      && docker-php-ext-install zip

COPY xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

WORKDIR /app/code/
CMD ["php-fpm"]

EXPOSE 9000