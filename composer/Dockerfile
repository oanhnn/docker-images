FROM php:7.1-alpine

RUN apk update \
 && apk add --no-cache \
        bash \
        curl \
        git \
        mercurial \
        openssh \
        openssl \
        subversion \
        tini \
 && echo "memory_limit=-1" > "$PHP_INI_DIR/conf.d/memory-limit.ini" \
 && echo "date.timezone=${PHP_TIMEZONE:-UTC}" > "$PHP_INI_DIR/conf.d/date_timezone.ini" \
 && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
 && php -r "if (hash_file('SHA384', 'composer-setup.php') === trim(file_get_contents('https://composer.github.io/installer.sig'))) { echo 'Installer verified' . PHP_EOL; } else { echo 'Installer invalid' . PHP_EOL; unlink('composer-setup.php'); exit(1); }" \
 && php composer-setup.php \
 && php -r "unlink('composer-setup.php');" \
 && mv composer.phar /usr/local/bin/composer \
 && chmod a+x /usr/local/bin/composer \
 && composer --ansi --version --no-interaction \
 && rm -rf /var/cache/apk/* /tmp/*

COPY docker-entrypoint.sh /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["composer"]
