 
### docker 安装
docker run -itd --name mongo -p 27017:27017 mongo:4.4.0 --auth

// admin 用户进入
docker exec -it mongo mongo admin
// 切换db
use xy365
// 创建账号
db.createUser({user:"xy365", pwd:"123456", roles:["readWrite"]});

// 退出重新进入
docker exec -it mongo mongo xy365
// 验证t账号
db.auth('xy365', '123456')

db.t_article.insert({title: 'aaaa', subtitle:'bbbbb', type: 'rich'})
db.t_article.insert({title: 'xxx', subtitle:'bbbbb', type: 'rich', tag: 'aaa'})
db.t_article.insert({title: 'yyy', name: 'name'})
db.t_article.insert({title: 'aaaa1', subtitle:'bbbbb', type: 'rich'})
db.t_article.insert({title: 'aaaa2', subtitle:'bbbbb', type: 'rich'})
db.t_article.insert({title: 'aaaa3', subtitle:'bbbbb', type: 'rich'})
db.t_article.insert({title: 'aaaa4', subtitle:'bbbbb', type: 'rich'})
db.t_article.insert({title: 'aaaa5', subtitle:'bbbbb', type: 'rich'})

db.t_article.find()


db.t_article.update({'title':'aaaa'},{$set:{'subtitle':'MongoDB'}})

db.t_article.remove({'title':'aaaa'})

db.t_article.find().count()

db.t_article.find().skip(2).limit(2)



// 切换db
use admin
// 创建root账号
db.createUser({user:"root",pwd:"123456",roles:[{role:"root",db:"admin"}]})
// 验证root账号
db.auth('root', '123456')
// 获取用户信息
db.getUsers()


### 编译生成 mongodb.so
wget https://pecl.php.net/get/mongodb-1.8.0.tgz

tar zxvf mongodb-1.8.0.tgz
cd mongodb-1.8.0
phpize
./configure
make && make install

### php 安装mongodb操作库
composer require mongodb/mongodb
> composer 中的mongodb/mongodb库很恶心，必须要检测php的mongodb扩展才能下载
> docker composer:latest 镜像基于 linux alpine, 安装mongodb扩展各种缺依赖
> docker php:7.4-apache 镜像基于 linux debian 也是各种缺依赖
> 安装依赖感觉还是centos yum 最好用， 只能自建基于 centos7的composer镜像

docker run --name=centos7_test -itd centos:7 /usr/sbin/init

// 安装PHP7
yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum -y install https://rpms.remirepo.net/enterprise/remi-release-7.rpm
yum -y install yum-utils
yum-config-manager --enable remi-php74
yum install php php-cli

// php开启pecl的支持
yum -y install php-devel php-pear
pecl channel-update pecl.php.net

// 安装 php mongodb 扩展
yum -y install make zip unzip php-mbstring
pecl install mongodb 
echo "extension=mongodb.so" >> `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"`

// 安装 composer
php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"
php composer-setup.php
php -r "unlink('composer-setup.php');"
mv composer.phar /usr/local/bin/composer
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/



// 镜像打包
docker commit centos7_test composer:mongodb-1.0
docker save -o php.tar nirvana72/php-apache:mongo-1.0