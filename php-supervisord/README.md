# oanhnn/php-supervisord

Repository of `oanhnn/php-supervisord` Docker image.

## Features

- [x] Base from `alpine:3.6` image
- [x] Install php-fpm 7.1
- [x] Install supervisor
- [x] Use ONBUILD for customizing supervisor programs

## Requirement
- Docker Engine 1.12+

## Usage

Make folder `supervisor.d` and put all your supervisor's program config files to that.

Make `Dockerfile`

```docker
# Dockerfile
FROM oanhnn/php-supervisord:latest

RUN echo ">>> Install nodejs, npm, yarn and laravel-echo-server" \
 && apk add --update \
    nodejs \
    nodejs-npm yarn \
 && apk add --update --no-cache -t .build-deps python make g++ gcc \
 && yarn global add --prod --no-lockfile laravel-echo-server \
 && apk del .build-deps \
 && yarn cache clean \
 && rm -rf /tmp/* /var/cache/apk/* \
 && echo ">>> Setting crond for laravel scheduler" \
 && echo -e "*\t*\t*\t*\t*\tphp /path/to/artisan schedule:run > /dev/null 2>&1" | crontab -u www-data -

EXPOSE 9000 9001
```

When you build, all your supervisor's program config files in `supervisor.d` will copy to container.

See more in Laravel example

## Contributing

All code contributions must go through a pull request and approved by
a core developer before being merged. This is to ensure proper review of all the code.

Fork the project, create a feature branch, and send a pull request.

If you would like to help take a look at the [list of issues](https://github.com/oanhnn/docker-images/issues).

## License

This project is released under the MIT License.   
Copyright © 2017 [Oanh Nguyen](https://github.com/oanhnn)   
Please see [License File](https://github.com/oanhnn/docker-images/blob/master/LICENSE) for more information.
