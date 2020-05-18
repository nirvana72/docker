### 查看swoole 是否安装
~~~
php -m 
~~~

### 安装
~~~
wget https://github.com/swoole/swoole-src/archive/v4.5.0.tar.gz

tar -zxvf v4.5.0.tar.gz

cd swoole-src-4.5.0

yum install php-devel

phpize && \
./configure && \
make && sudo make install

vim /etc/php.ini

extension=swoole.so;

// swoole.so 目录
// cd /usr/lib64/php/modules
~~~

### easyswoole
~~~
yum install zip unzip
cd your-project
composer require easyswoole/easyswoole=3.x

// dev.php -> TEMP_DIR 临时目录
// 'TEMP_DIR' => '/tmp',
~~~




docker commit centos7_test swoole:v1





docker run --name=swoole -p 80:80 -p 9501-9509:9501-9509 --privileged=true -v D:/workspace:/workspace -itd swoole:v1.1 /usr/sbin/init