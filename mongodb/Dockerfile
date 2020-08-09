FROM php:7.4.8-apache
COPY mongodb-debian-1.8.0.so /usr/local/lib/php/extensions/no-debug-non-zts-20190902/mongodb.so
# COPY mysqli.so /usr/local/lib/php/extensions/no-debug-non-zts-20190902/mysqli.so
# COPY pdo_mysql.so /usr/local/lib/php/extensions/no-debug-non-zts-20190902/pdo_mysql.so
# COPY default.conf /etc/apache2/sites-enabled/000-default.conf
# COPY ext-custom.ini /usr/local/etc/php/conf.d/ext-custom.ini
COPY index.php /var/www/index/index.php

# docker build -t php-apache:7.4.8 .
# docker run --name=php-demo -itd -p 80:80 php-apache:7.4.8