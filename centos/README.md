 docker run --name=centos7_test -p 9000:80 --privileged=true -v E:/workspace:/workspace -itd centos:7 /usr/sbin/init

### 宝塔

~~~
 # https://www.bt.cn/btcode.html

 docker run --name=baota -p 80:80 -p 443:443 -p 3306:3306 -p 8888:8888 --privileged=true -v E:/workspace:/workspace -itd baota:v1.2 /usr/sbin/init
~~~

 
docker run --name=node-14.5.0-alpine --network dev_net -p 8080-8089:8080-8089 --privileged=true -v E:/workspace:/workspace -itd node:14.5.0-alpine
docker run --name=centos7-java --network dev_net -itd -p 8090-8099:8090-8099 --privileged=true -v E:/workspace:/workspace centos:centos7