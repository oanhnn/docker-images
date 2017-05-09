# oanhnn/php-fpm

Repository of `oanhnn/php-fpm` Docker image.

## Features

- [x] Using latest php:7.x-fpm-alpine
- [x] Installed `mcrypt`, `pdo`,_`mysql`, `intl`, `opcache`, `zip` and `gd` extensions

## Requirement
- Docker Engine 1.12+

## Usage

### Extends from `php:7.x-alpine` image

### Pull php-fpm 7.0

```shell
$ docker pull oanhnn/php-fpm:7.0
$ docker run -it --rm oanhnn/php-fpm:7.0 php -v
```
### Pull php fpm 7.0 with xdebug

```shell
$ docker pull oanhnn/php-fpm:7.0-xdebug
$ docker run -it --rm oanhnn/php-fpm:7.0-xdebug php -v
```

### Pull php fpm 7.1

```shell
$ docker pull oanhnn/php-fpm:7.1
$ docker run -it --rm oanhnn/php-fpm:7.1 php -v
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
