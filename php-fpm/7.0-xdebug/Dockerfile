FROM php:7.0-fpm-alpine

RUN apk update \
 && apk add --no-cache --virtual .build-deps \
        autoconf \
        freetype-dev \
        g++ \
        icu-dev \
        libjpeg-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libwebp-dev \
        libxpm-dev \
        make \
        postgresql-dev \
        zlib-dev \

 && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ \
                                --with-jpeg-dir=/usr/include/ \
                                --with-webp-dir=/usr/include/ \
                                --with-xpm-dir=/usr/include/ \
                                --with-png-dir=/usr/include/ \
                                --with-zlib-dir=/usr/ \
 && docker-php-ext-install mcrypt pdo_mysql pdo_pgsql intl opcache zip gd \

 && pecl install xdebug \
 && docker-php-ext-enable xdebug \
 && sed -i '1 a xdebug.remote_autostart=true' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
 && sed -i '1 a xdebug.remote_mode=req' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
 && sed -i '1 a xdebug.remote_handler=dbgp' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
 && sed -i '1 a xdebug.remote_connect_back=1' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
 && sed -i '1 a xdebug.remote_port=9001' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
 && sed -i '1 a xdebug.remote_enable=1' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \

 && runDeps="$( \
    scanelf --needed --nobanner --recursive /usr/local \
      | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
      | sort -u \
      | xargs -r apk info --installed \
      | sort -u \
    )" \
 && apk add --no-cache --virtual .php-rundeps $runDeps \

 && apk del .build-deps \
 && rm -rf /var/cache/apk/* /tmp/*

EXPOSE 9000

ENTRYPOINT ["docker-php-entrypoint"]

CMD ["php-fpm"]
