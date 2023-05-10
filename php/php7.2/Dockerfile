# Dockerfile
FROM php:7.2-fpm-alpine

# Install PHP extension dependencies
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
  && apk add --no-cache $PHPIZE_DEPS && apk add linux-headers --update --no-cache

# Install xdebug extension Enable xdebug extension
RUN pecl install xdebug-2.9.8 && docker-php-ext-enable xdebug

# Configure xdebug settings
RUN cat >> /usr/local/etc/php/php.ini <<EOF
[xdebug]
# zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20170718/xdebug.so
xdebug.remote_enable=1
xdebug.remote_autostart=1
xdebug.remote_connect_back=0
xdebug.remote_host=host.docker.internal
xdebug.remote_port=9003
EOF

RUN apk del $PHPIZE_DEPS
