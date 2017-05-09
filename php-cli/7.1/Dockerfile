FROM php:7.1-alpine

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
        zlib-dev \

 && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ \
                                --with-jpeg-dir=/usr/include/ \
                                --with-webp-dir=/usr/include/ \
                                --with-xpm-dir=/usr/include/ \
                                --with-png-dir=/usr/include/ \
                                --with-zlib-dir=/usr/ \
 && docker-php-ext-install mcrypt pdo_mysql intl opcache zip gd \

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

ENTRYPOINT ["docker-php-entrypoint"]

CMD ["php", "-a"]
