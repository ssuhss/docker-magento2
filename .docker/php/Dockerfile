FROM php:8.1.5-fpm

ARG ssh_prv_key
ARG ssh_pub_key

COPY --from=composer:2.2.7 /usr/bin/composer /usr/local/bin/composer

RUN pecl install xdebug && docker-php-ext-enable xdebug

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y -qq libjpeg62-turbo-dev libpng-dev libxml2-dev libxslt-dev libsodium-dev libzip-dev libfreetype6-dev openssh-server
RUN docker-php-ext-configure gd --with-freetype --with-jpeg



RUN apt-get install -y git unzip \
                           libfreetype6-dev \
                           libjpeg62-turbo-dev \
                           libxml2-dev \
                           libxslt1-dev \
                           cron \
			               build-essential \
			               supervisor

RUN docker-php-ext-install  pdo \
                            pdo_mysql \
                            gd \
                            bcmath \
                            intl \
                            xsl \
                            soap \
                            sockets \
                            simplexml \
                            pcntl \
                            exif \
                            opcache \
                            dom

RUN apt-get install -y \
            libzip-dev \
            zip \
            ssmtp \
            mailutils \
            wget \
      && docker-php-ext-install zip

RUN wget https://github.com/mailhog/mhsendmail/releases/download/v0.2.0/mhsendmail_linux_amd64
RUN chmod +x mhsendmail_linux_amd64
RUN mv mhsendmail_linux_amd64 /usr/local/bin/mhsendmail


COPY xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

WORKDIR /app/code/magento2/
CMD ["php-fpm"]

EXPOSE 9000
