# 基于别人的镜像增加 pdo_mysql支持，创建一个自己的镜像

FROM sohmc/php-mysqli:7-fpm-alpine
ADD ./php_ext/pdo_mysql.so /usr/local/lib/php/extensions/no-debug-non-zts-20190902
ADD ./docker/php/docker-php-ext-mysqli.ini /usr/local/etc/php/conf.d/docker-php-ext-mysqli.ini