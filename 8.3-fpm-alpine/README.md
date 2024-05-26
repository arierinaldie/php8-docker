[![Downloaded GitHub Releases](https://img.shields.io/github/downloads/arierinaldie/php8-docker/tree/8.3-fpm-alpine/total?label=Downloaded%20releases)](https://github.com/arierinaldie/php8-docker/releases)

# php8.3-fpm-alpine
Customized version of the official php8.3-fpm-alpine docker images for developing containerize web app using php8.3

## Build
```sh
docker build -f ./8.3-fpm-alpine/Dockerfile -t test_phpimage ./8.3-fpm-alpine
```

## Usage
```sh
# list all installed extension
docker run -it --rm --name test_run_phpimage test_phpimage:latest php -m

# dive in to container
docker run -it --rm --name test_run_phpimage test_phpimage:latest sh
```