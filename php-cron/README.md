# oanhnn/php-cron

Repository of `oanhnn/php-cron` Docker image.

## Features

- [x] Base from `alpine:3.6` image
- [x] Install php-fpm 7.1
- [x] Run crond

## Requirement
- Docker Engine 1.12+

## Usage

Make `Dockerfile`

```docker
# Dockerfile
FROM oanhnn/php-cron:latest

RUN echo ">>> Setting crond for laravel scheduler" \
 && echo -e "*\t*\t*\t*\t*\tphp /path/to/artisan schedule:run > /dev/null 2>&1" | crontab -u www-data -
```

## Contributing

All code contributions must go through a pull request and approved by
a core developer before being merged. This is to ensure proper review of all the code.

Fork the project, create a feature branch, and send a pull request.

If you would like to help take a look at the [list of issues](https://github.com/oanhnn/docker-images/issues).

## License

This project is released under the MIT License.   
Copyright © 2017 [Oanh Nguyen](https://github.com/oanhnn)   
Please see [License File](https://github.com/oanhnn/docker-images/blob/master/LICENSE) for more information.
