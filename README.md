> 以下docker 命令中的 {$path} 先替换成具体目录后再执行...

# 添加国内镜像
~~~
"https://docker.mirrors.ustc.edu.cn",
"https://registry.docker-cn.com",
"http://hub-mirror.c.163.com"
~~~

# nginx+php+mysql
#### 1.link 引用方式
三个服务分别创建三个容器， 由于服务之间用到 link 引用，所以创建顺序需要从
mysql -> php -nginx 
严格执行，否则后建的容器引用不到服务。容器开启时，貌似也需要按照这个顺序。

~~~
# 创建 mysql 容器
docker run --name=mysql -d 
-p 3306:3306 -v {$path}/docker/mysql/mysqld.cnf:/etc/mysql/mysql.conf.d/mysqld.cnf -v {$path}/docker/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 mysql:5.7.29

# 创建 php服务 容器
docker run --name=phpserver -d -v {$path}/workspace:/workspace -v {$path}/docker/php/docker-php-ext-sodium.ini:/usr/local/etc/php/conf.d/docker-php-ext-sodium.ini --link mysql:mysql nirvana72/php:7.4-fpm-alpine

# 创建 nginx 容器
docker run --name=nginx -d -p 80:80 -v {$path}/workspace:/workspace -v {$path}/docker/nginx/conf.d:/etc/nginx/conf.d:ro --link phpserver:phpserver nginx:1.17-alpine
~~~

#### 2.bridge网络方式
创建一个docker环境内的网络名，容器创建时都挂到这个网络上去，这样容器之间就可以通过别名互相访问
~~~
# 创建bridge网络
docker network create dev_net
# 查看bridge网络
docker network ls
~~~

~~~
# mysql 容器
docker run -d --name=mysql -p 3306:3306 -v {$path}/docker/mysql/mysqld.cnf:/etc/mysql/mysql.conf.d/mysqld.cnf -v {$path}/docker/mysql/data:/var/lib/mysql --network dev_net --network-alias mysql -e MYSQL_ROOT_PASSWORD=123456 mysql:5.7.29
# php 容器
docker run --name=phpserver -d -v {$path}/workspace:/workspace -v {$path}/docker/php/docker-php-ext-sodium.ini:/usr/local/etc/php/conf.d/docker-php-ext-sodium.ini --network dev_net --network-alias phpserver nirvana72/php:7.4-fpm-alpine
# nginx 容器
docker run --name=nginx -d -p 80:80 -v {$path}/workspace:/workspace -v {$path}/docker/nginx/conf.d:/etc/nginx/conf.d:ro --network dev_net --network-alias nginx nginx:1.17-alpine
~~~

# nodejs 容器
~~~
# 创建
docker run --name=nodejs -itd -p 8080:8080 -v  {$path}/workspace:/workspace -w /workspace node:12.16.2-alpine
# 修改 npm 镜像源
npm config set registry https://registry.npm.taobao.org
# 安装 vue-cli 4.0
npm install -g @vue/cli
~~~

# php composer
如果不想在容器内装 composer ，又要为php项目安装依赖，创建一个composer容器临时用一下
~~~
# 创建 composer 容器， 为 php 项目安装依赖用
docker run -dit --name=composer -v {$path}/workspace:/workspace -w /workspace composer:latest /bin/bash
# 更新国内仓库镜像
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
~~~

# portainer
一个可视化docker 管理UI
~~~
# 创建卷
docker volume create portainer

# linux
docker run -d -p 9000:9000 --name portainer -v portainer:/var/run/docker.sock portainer/portainer

# windows
docker run -d -p 9000:9000 --name portainer -v /var/run/docker.sock:/var/run/docker.sock -v portainer:/data portainer/portainer
~~~


# volume 使用
- volume  是指为了适应不同系统的目录结构，而一些数据又需要持久化在宿主机上，所以在docker系统目录下创建一个带别外的存储空间给容器作持久化使用
- 默认目录应该是在docker安装目录下，可以用docker inspect查看，windows由于docker是装在虚拟机上的，所以目录也在虚拟机上
- 开发环境下，因为持久化数据经常需要去定位查看和修改，所以个人觉得还是指定目录的好

~~~
# 列出所有卷
docker volume ls
# 创建卷
docker volume create workspace
# 查看卷
docker inspect workspace
# 使用卷
docker run --name=nodejs -itd -p 8080:8080 -v workspace:/workspace node:12.16.2-alpine
# 删除卷
docker volume rm edc-nginx-vol
~~~

# 其它命令
~~~
# 进入容器命令
 docker exec -it nginx bash
~~~