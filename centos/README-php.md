### PHP 7

~~~
yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum -y install https://rpms.remirepo.net/enterprise/remi-release-7.rpm

yum -y install yum-utils
yum-config-manager --enable remi-php74
yum install php php-cli
~~~

### apache

~~~

yum install httpd

vim /etc/httpd/conf/httpd.conf

 <Directory />
    Options FollowSymLinks
    AllowOverride None
    Order deny,allow
    allow from all
</Directory>

cd /etc/httpd/conf.d
vim nij.conf

<VirtualHost *:80>
    DocumentRoot /workspace/nij.php
    ServerName php.nij.local
</VirtualHost>

systemctl restart httpd.service

http://php.nij.local/test.php

~~~

### composer

~~~
php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"
php composer-setup.php
php -r "unlink('composer-setup.php');"
mv composer.phar /usr/local/bin/composer
~~~