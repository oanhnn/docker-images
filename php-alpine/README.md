# oanhnn/php7.0-fpm-alpine

[![Build Status](https://travis-ci.org/oanhnn/php7.0-fpm-alpine.svg?branch=master)](https://travis-ci.org/oanhnn/php7.0-fpm-alpine)
[![](https://images.microbadger.com/badges/image/oanhnn/php7.0-fpm-alpine.svg)](https://microbadger.com/images/oanhnn/php7.0-fpm-alpine)
[![](https://images.microbadger.com/badges/version/oanhnn/php7.0-fpm-alpine.svg)](https://microbadger.com/images/oanhnn/php7.0-fpm-alpine)

Repository of `oanhnn/php7.0-fpm-alpine` Docker image.

## Features
- [x] Using latest stable Alpine Linux.
- [x] Installed php-fpm 7.0 and some extensions

## Requirement
- Docker Engine 1.12+

## Usage

```shell
$ docker pull oanhnn/php7.0-fpm-alpine
$ docker run -it oanhnn/php7.0-fpm-alpine:latest sh
/var/www # php -v
PHP 7.0.16 (cli) (built: Feb 18 2017 15:05:55) ( NTS )
Copyright (c) 1997-2017 The PHP Group
Zend Engine v3.0.0, Copyright (c) 1998-2017 Zend Technologies
    with Zend OPcache v7.0.16, Copyright (c) 1999-2017, by Zend Technologies
/var/www # php -m
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

## Contributing
All code contributions must go through a pull request and approved by
a core developer before being merged. This is to ensure proper review of all the code.

Fork the project, create a feature branch, and send a pull request.

If you would like to help take a look at the [list of issues](issues).

## License
This project is released under the MIT License.   
Copyright © 2017 [Oanh Nguyen](https://github.com/oanhnn)   
Please see [License File](LICENSE) for more information.
