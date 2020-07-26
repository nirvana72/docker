yum update

安装 docker 
https://developer.aliyun.com/mirror   docker-ce

修建镜像仓库
https://cr.console.aliyun.com/#/accelerator  镜像仓库加速


## portainer
拉取portainer镜像
docker pull portainer/portainer:1.24.1-alpine

创建portainer容器
docker volume create portainer
docker run -d -p 9000:9000 --name=portainer -v /var/run/docker.sock:/var/run/docker.sock -v portainer:/data --restart=always portainer/portainer:1.24.1-alpine 

开放9000端口
访问 http://ip:9000

## gitlab
下拉镜像(特慢， 可以使用 docker save | docker load )
docker pull gitlab/gitlab-ce:13.1.5-ce.0

创建容器
docker run --name=gitlab -d -v /etc/gitlab:/etc/gitlab -v /var/opt/gitlab:/var/opt/gitlab -v /var/log/gitlab:/var/log/gitlab -p 9001:80 gitlab/gitlab-ce:13.1.5-ce.0

迁移
备份
gitlab-rake gitlab:backup:create
会生成 /var/opt/gitlab/backups/xxxx_gitlab_backup.tar

复制到新环境同目录下还原备份
gitlab-rake gitlab:backup:restore BACKUP=xxxx // 只要xxxx

## nginx
安装
sudo yum install nginx
启动
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
查看
ps -ef |grep nginx
配置文件
cd /etc/nginx/conf.d
转发配置
~~~
# xxx.conf
server 
{
  listen 80;
  server_name xy365-api.lan8.cn;
  
  location / {
    proxy_pass http://127.0.0.1:8001;
  }
}
~~~

# 部署项目

创建网络组
docker network create my_net1 

## php
docker pull php:7.4-apache

index.php
~~~
<?php
  phpinfo();
?>
~~~

Dockerfile
~~~
FROM php:7.4-apache
MAINTAINER nijia 15279663@qq.com
COPY index.php /var/www/html
~~~

创建项目镜像
docker build -t nirvana72/php-test:1.0 .
根据项目镜像创建容器
docker run --name=php-test --network my_net1 -d -p 8001:80 nirvana72/php-test:1.0

## mysql
docker pull mysql:5.7

docker volume create mysql_data

docker run -d --name=mysql -p 3306:3306 -v mysql_data:/var/lib/mysql --network my_net1 --network-alias mysql5.7 -e MYSQL_ROOT_PASSWORD=123456 mysql:5.7