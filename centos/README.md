 docker run --name=centos7_test -p 9000:80 --privileged=true -v E:/workspace:/workspace -itd centos:7 /usr/sbin/init

### 宝塔

~~~
 # https://www.bt.cn/btcode.html

 docker run --name=baota -p 8888:8888 -p 3306:3306 -p 80:80 --privileged=true -v D:/workspace:/workspace -itd centos:7 /usr/sbin/init
~~~


### window 进入docker 虚拟机
docker run --privileged -it -v /var/run/docker.sock:/var/run/docker.sock --rm jongallant/ubuntu-docker-client

docker run --net=host --ipc=host --uts=host --pid=host -it --security-opt=seccomp=unconfined --privileged --rm -v /:/host alpine /bin/sh

chroot /host




