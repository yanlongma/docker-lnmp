FROM php:7.1-fpm-alpine

# apk
RUN apk --update add \
        autoconf \
        build-base \
        linux-headers \
        libaio-dev \
        zlib-dev \
        curl \
        git \
        subversion \
        freetype-dev \
        libjpeg-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libtool \
        libbz2 \
        bzip2 \
        bzip2-dev \
        libstdc++ \
        libxslt-dev \
        openldap-dev \
        imagemagick-dev \
        make \
        unzip \
        wget \
        libmemcached-dev

# PHP Core Extensions
RUN docker-php-ext-install \
        bcmath \
        pdo_mysql \
        mysqli \
        pcntl \
        sockets\
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

# PECL Extensions
RUN pecl install redis-4.2.0 \
    && pecl install mongodb-1.5.3 \
    && pecl install memcached-3.1.3 \
    && pecl install swoole-4.3.1 \
    && docker-php-ext-enable redis mongodb memcached swoole

# Delete
RUN apk del build-base \
    	linux-headers \
    	libaio-dev \
    && rm -rf /var/cache/apk/*

VOLUME /var/www
WORKDIR /var/www

EXPOSE 9000
CMD ["php-fpm"]