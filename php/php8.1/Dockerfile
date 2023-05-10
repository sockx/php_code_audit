# Dockerfile
FROM php:8.1-fpm-alpine

# Install PHP extension dependencies
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
  && apk add --no-cache $PHPIZE_DEPS && apk add linux-headers --update --no-cache

# Install xdebug extension Enable xdebug extension
RUN pecl install xdebug && docker-php-ext-enable xdebug

# Configure xdebug settings
RUN cat >> /usr/local/etc/php/php.ini <<EOF
[xdebug]
# zend_extension=xdebug.so
xdebug.mode=debug
xdebug.start_with_request=yes
xdebug.client_host=host.docker.internal
xdebug.client_port=9003
EOF

RUN apk del $PHPIZE_DEPS
