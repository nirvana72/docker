# 基于别人的镜像增加 pdo_mysql支持，创建一个自己的镜像

FROM php:7.4.4-fpm-alpine3.11
ADD ./ext/*.so /usr/local/lib/php/extensions/no-debug-non-zts-20190902/
# ADD ./docker/php/docker-php-ext-mysqli.ini /usr/local/etc/php/conf.d/docker-php-ext-mysqli.ini

# docker build -t nirvana72/php:7.4-fpm-alpine .