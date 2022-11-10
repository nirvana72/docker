docker volume create mysql

docker run --name=mysql --network my_net -d -p 3306:3306 -v mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 mysql:5.7