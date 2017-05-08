FROM nginx:1.13-alpine

ENV NGINX_UPSTREAM="php-fpm:9000" \
    NGINX_DOMAINS="example.com"

COPY side.conf /etc/nginx/site.template
