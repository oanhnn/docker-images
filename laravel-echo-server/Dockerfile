FROM node:alpine

RUN apk add --update --no-cache bash \
 && apk add --update --no-cache -t .build-deps python make g++ gcc \
 && npm i -g laravel-echo-server \
 && apk del .build-deps \
 && rm -rf /tmp/* /var/cache/apk/*

WORKDIR /var/www

EXPOSE 6001

ENTRYPOINT ["laravel-echo-server"]

CMD ["start"]
