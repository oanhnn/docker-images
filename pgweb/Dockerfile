#https://github.com/sosedoff/pgweb

FROM alpine:latest

LABEL image="oanhnn/php-alpine" \
      license="MIT" \
      homepage="https://github.com/oanhnn/docker-images"

ENV PGWEB_VERSION=0.9.7 \
    DATABASE_URL="postgres://postgres:postgres@postgres:5432/postgres?sslmode=disable" \
    AUTH_USER="" \
    AUTH_PASS=""

COPY ./docker-entrypoint.sh /usr/local/bin/docker-entrypoint

RUN apk add --update ca-certificates wget \
 && wget -q -O /tmp/pgweb_linux_amd64.zip https://github.com/sosedoff/pgweb/releases/download/v$PGWEB_VERSION/pgweb_linux_amd64.zip \
 && unzip /tmp/pgweb_linux_amd64.zip -d /usr/local/bin \
 && mv /usr/local/bin/pgweb_linux_amd64 /usr/local/bin/pgweb \
 && chmod a+x /usr/local/bin/pgweb /usr/local/bin/docker-entrypoint \
 && apk del ca-certificates wget \
 && rm -rf /tmp/* /var/cache/apk/*

EXPOSE 8081

ENTRYPOINT ["/usr/local/bin/docker-entrypoint"]

CMD ["/usr/local/bin/pgweb", "--bind=0.0.0.0", "--listen=8081", "--user=${AUTH_USER}", "--pass=${AUTH_PASS}"]
