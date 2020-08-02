 
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



wget https://pecl.php.net/get/mongodb-1.8.0.tgz



./configure --with-php-config=/www/server/php/74/etc/php-config

/www/server/php/74/bin/pecl install mongodb

composer require mongodb/mongodb


docker run --name=phptest -d php:7.4.8-apache


docker run --name=phptest -d php:7.4.8-apache
docker cp mongodb-1.8.0.tgz centos7_test:/home
docker exec -it phptest /bin/bash
docker cp centos7_test:/home/mongodb-1.8.0/modules/mongodb.so mongodb.so
docker stop phptest

docker rm phptest
