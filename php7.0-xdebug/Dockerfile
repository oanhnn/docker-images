FROM oanhnn/php7.0-cli

RUN apk update \
 && apk add --no-cache --virtual .build-deps \
        autoconf \
        g++ \
        make \

 && pecl install xdebug \
 && docker-php-ext-enable xdebug \
 && sed -i '1 a xdebug.remote_autostart=true' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
 && sed -i '1 a xdebug.remote_mode=req' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
 && sed -i '1 a xdebug.remote_handler=dbgp' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
 && sed -i '1 a xdebug.remote_connect_back=1 ' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
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

ENTRYPOINT ["docker-php-entrypoint"]

CMD ["php", "-a"]
