 docker run --name=centos7_test -p 9000:80 --privileged=true -v E:/workspace:/workspace -itd centos:7 /usr/sbin/init

### 宝塔

~~~
 # https://www.bt.cn/btcode.html

 docker run --name=baota20210511 -p 8888:8888 -p 80:80 -p 81:81 -p 8080:8080 -p 8081:8081 --privileged=true -v E:/workspace:/workspace -itd centos:7 /usr/sbin/init
~~~


### window 进入docker 虚拟机
docker run --privileged -it -v /var/run/docker.sock:/var/run/docker.sock --rm jongallant/ubuntu-docker-client

docker run --net=host --ipc=host --uts=host --pid=host -it --security-opt=seccomp=unconfined --privileged --rm -v /:/host alpine /bin/sh

chroot /host




### docker ping 不通外网
新建一个centos容器， 检查是否能ping通外网
docker run --name=centos7_test -itd centos:7 /usr/sbin/init
查看 nameserver 192.168.65.1

修改不能ping外网的容器
vi /etc/resolv.conf