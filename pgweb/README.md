# oanhnn/pgweb

Repository of `oanhnn/pgweb` Docker image.

[pgweb](https://github.com/sosedoff/pgweb) : Web-based PostgreSQL database browser written in Go.

## Features

- [x] Using alpine:latest
- [x] Install pgweb latest

## Requirement
- Docker Engine 1.12+

## Usage

> Note that as a default, the postgres container does not have SSL enabled, so just disable that by `sslmode=disable`.

Using with Docker Engine

```shell
$ docker run -d -p 5432:5432 --name db -e POSTGRES_PASSWORD=pass -e POSTGRES_USER=user -e POSTGRES_DB=testdb postgres:alpine
$ docker run -d -p 80:80 --name pgweb -e DATABASE_URL="postgres://user:pass@db:5432/testdb?sslmode=disable" -e AUTH_USER=dev -e AUTH_PASS=1234 oanhnn/pgweb:latest
```

Or using with Docker Compose

```yaml
version: "3"

services:
  db:
    image: postgres:9.6-alpine
    environment:
      POSTGRES_DB:       testdb
      POSTGRES_USER:     user
      POSTGRES_PASSWORD: pass
    volumes:
      - ./data:/var/lib/postgresql/data
      - ./backup:/docker-entrypoint-initdb.d
    networks:
      - internal
    restart: always

  pgweb:
    image: sosedoff/pgweb
    environment:
      DATABASE_URL: "postgres://user:pass@db:5432/testdb?sslmode=disable"
      AUTH_USER:    "dev"
      AUTH_PASS:    "1234"
    networks:
      - external
      - internal
    ports:
      - "80:80"
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
