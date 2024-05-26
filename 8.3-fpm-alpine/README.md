[![Downloaded GitHub Releases](https://img.shields.io/github/downloads/arierinaldie/php8-docker/tree/8.3-fpm-alpine/total?label=Downloaded%20releases)](https://github.com/arierinaldie/php8-docker/releases)
[![Downloaded GitHub Releases](https://img.shields.io/github/downloads/arierinaldie/php8-docker/total.svg)](https://github.com/arierinaldie/php8-docker/releases)

# php8.3-fpm-alpine
Customized version of the official php8.3-fpm-alpine docker images for developing containerize web app using php8.3

## Build
```sh
docker build -f ./8.3-fpm-alpine/Dockerfile -t test_phpimage ./8.3-fpm-alpine
```

## Usage
### Dive into container
```sh
docker run -it --rm --name test_run_phpimage test_phpimage:latest sh
```
### list all installed extension
```sh
docker run -it --rm --name test_run_phpimage test_phpimage:latest php -m
```
```
[PHP Modules]
amqp
apcu
bcmath
calendar
Core
ctype
curl
date
dom
exif
fileinfo
filter
ftp
gd
hash
iconv
igbinary
imagick
intl
json
libxml
mbstring
memcached
mongodb
mysqli
mysqlnd
openssl
pcntl
pcre
PDO
pdo_mysql
pdo_pgsql
pdo_sqlite
pgsql
Phar
posix
random
readline
redis
Reflection
session
shmop
SimpleXML
sockets
sodium
SPL
sqlite3
ssh2
standard
tokenizer
xml
xmlreader
xmlrpc
xmlwriter
Zend OPcache
zip
zlib

[Zend Modules]
Zend OPcache
```
