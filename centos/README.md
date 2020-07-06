 docker run --name=centos7_test -p 80:80 --privileged=true -v D:/workspace:/workspace -itd centos:7 /usr/sbin/init

### 宝塔

~~~
 # https://www.bt.cn/btcode.html

 docker run --name=baota -p 80:80 -p 443:443 -p 3306:3306 -p 8888-8900:8888-8900 --privileged=true -v D:/workspace:/workspace -itd baota:v1.2 /usr/sbin/init
~~~






 docker run --name=gitlab-runner-vue -p 8080:8080 --privileged=true -v /Users/nijia/workspace:/workspace -itd centos:7 /usr/sbin/init



 curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.rpm.sh | bash