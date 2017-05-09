# oanhnn/php-alpine

Repository of `oanhnn/php-alpine` Docker image.

## Features

- [x] Using latest stable Alpine Linux.
- [x] Installed php-fpm and some extensions

```shell
# php -m
[PHP Modules]
bcmath
Core
ctype
curl
date
dom
fileinfo
filter
gd
hash
iconv
intl
json
libxml
mbstring
mcrypt
mysqli
mysqlnd
openssl
pcre
PDO
pdo_mysql
pdo_pgsql
pdo_sqlite
Phar
posix
readline
Reflection
session
SimpleXML
soap
SPL
standard
tokenizer
xml
xmlwriter
Zend OPcache
zip

[Zend Modules]
Zend OPcache
```

## Requirement
- Docker Engine 1.12+

## Usage

### Pull PHP 7.0

```shell
$ docker pull oanhnn/php-alpine:7.0
$ docker run -it --rm oanhnn/php-alpine:7.0 php -v
PHP 7.0.16 (cli) (built: Feb 18 2017 15:05:55) ( NTS )
Copyright (c) 1997-2017 The PHP Group
Zend Engine v3.0.0, Copyright (c) 1998-2017 Zend Technologies
    with Zend OPcache v7.0.16, Copyright (c) 1999-2017, by Zend Technologies
```

### Pull PHP 7.1

```shell
$ docker pull oanhnn/php-alpine:7.1
$ docker run -it --rm oanhnn/php-alpine:7.1 php -v
PHP 7.1.4 (cli) (built: May  1 2017 23:09:19) ( NTS )
Copyright (c) 1997-2017 The PHP Group
Zend Engine v3.1.0, Copyright (c) 1998-2017 Zend Technologies
    with Zend OPcache v7.1.4, Copyright (c) 1999-2017, by Zend Technologies
```

### Environments for rebuild

Environment           | Default | Description
----------------------|---------|------------
`TIMEZONE`            | "UTC"   | Set timezone for PHP
`PHP_MEMORY_LIMIT`    | "512M"  | Set maximum memory for php
`MAX_UPLOAD`          | "10M"   |
`PHP_MAX_FILE_UPLOAD` | 20      |
`PHP_MAX_POST`        | "20M"   |

### Paths

* PHP bin files: `/usr/bin/php` , `/usr/sbin/php-fpm`
* PHP ini file: `/etc/php/php.ini`
* PHP FPM config: `/etc/php/php-fpm.conf`, `/etc/php/php-fpm.d/www.conf`
* PHP FPM logs: `/var/logs/php-fpm`
* PHP FPM webroot: `/var/www/html`

## Contributing

All code contributions must go through a pull request and approved by
a core developer before being merged. This is to ensure proper review of all the code.

Fork the project, create a feature branch, and send a pull request.

If you would like to help take a look at the [list of issues](https://github.com/oanhnn/docker-images/issues).

## License

This project is released under the MIT License.   
Copyright © 2017 [Oanh Nguyen](https://github.com/oanhnn)   
Please see [License File](https://github.com/oanhnn/docker-images/blob/master/LICENSE) for more information.
