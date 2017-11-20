FROM alpine:3.6

ENV LANG="en_US.UTF-8" \
    LC_ALL="en_US.UTF-8" \
    LANGUAGE="en_US.UTF-8" \
    TIMEZONE="UTC" \
    PHP_MEMORY_LIMIT="512M" \
    DEPLOYER_VERSION="6.0.3"

RUN apk add --update \
    ca-certificates \
    curl \
    git \
    openssh-client \
    php7 \
    php7-dom \
    php7-ctype \
    php7-curl \
    php7-json \
    php7-mbstring \
    php7-mcrypt \
    php7-opcache \
    php7-openssl \
    php7-phar \
    php7-tokenizer \
    php7-xmlwriter \
    php7-xml \
    php7-zip \
    php7-zlib \
    rsync \
 && rm -rf /tmp/* /var/cache/apk/* \
 && echo ">>> Setting up" \
 && ln -nfs /usr/bin/php7 /usr/bin/php \
 && ln -nfs /etc/php7 /etc/php \
 && echo -e 'Host *\nUseRoaming no' >> /etc/ssh/ssh_config \
 && echo ">>> Config PHP" \
 && sed -i "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" /etc/php/php.ini \
 && sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" /etc/php/php.ini

RUN echo ">>> Install Deployer" \
 && curl -LO https://deployer.org/releases/v${DEPLOYER_VERSION}/deployer.phar \
 && mv deployer.phar /usr/bin/dep \
 && chmod +x /usr/bin/dep

CMD ["dep"]
