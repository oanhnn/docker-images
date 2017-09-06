# oanhnn/php-cron

Repository of `oanhnn/php-cron` Docker image.

## Features

- [x] Base from `alpine:3.6` image
- [x] Install php-fpm 7.1
- [x] Install supervisor
- [x] Run php-fpm, crond and syslogd via supervisord

## Requirement
- Docker Engine 1.12+

## Usage

Using with Docker Engine

```shell
$ docker pull oanhnn/php-cron:latest
$ docker run -d -p 9000:9000 --name php-cron oanhnn/php-cron:latest
```

Or using with Docker Compose

```yaml
version: "3"

services:
  app:
    image: oanhnn/php-cron:latest
    environment:
      TERM: linux
    volumes:
      - ./dockers/app/php-fpm.conf:/etc/php/php-fpm.conf:ro
      - ./dockers/app/cron.conf:/etc/crontabs/www-data:ro
      - .:/app
    networks:
      - internal
    working_dir: /app
    restart: always

  web:
    image: nginx:stable-alpine
    environment:
      TERM: linux
    depends_on:
      - app
    volumes:
      - ./dockers/web/site.conf:/etc/nginx/conf.d/site.conf:ro
      - .:/app
    networks:
      - internal
      - external
    ports:
      - "80:80"
    working_dir: /app
    restart: always

networks:
  external:
    driver: bridge
  internal:
    driver: bridge
```

It should start web server on http://localhost:80

## Contributing

All code contributions must go through a pull request and approved by
a core developer before being merged. This is to ensure proper review of all the code.

Fork the project, create a feature branch, and send a pull request.

If you would like to help take a look at the [list of issues](https://github.com/oanhnn/docker-images/issues).

## License

This project is released under the MIT License.   
Copyright © 2017 [Oanh Nguyen](https://github.com/oanhnn)   
Please see [License File](https://github.com/oanhnn/docker-images/blob/master/LICENSE) for more information.
