### centos 虚拟机安装

. 下载vmbox https://www.virtualbox.org/wiki/Downloads
. 下载centos7 镜像 http://mirrors.aliyun.com/centos/7/isos/x86_64/ mini版本

### 安装前配置
网络选 nat网络， 需要在VMBOX 管理-》全局-》网络中创建 nat网络， 个人理解为overlay 网络的原理

存储 -》 选择盘片 （ xxx.iso）

### 安装完成系统配置
vmbox 挂载光盘  （VMBOX 界面操作）

修改主机名
> hostname node1

光盘挂载到系统， 配置yum 源
~~~
mount /dev/cdrom /mnt
cd /etc/yum.repos.d/
cp -p CentOS-Media.repo centos7.repo
vi centos7.repo

name=CentOS7
baseurl=file:///mnt
gpgcheck=0
cnabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

>wq!

cd /etc/sysconfig/network-scripts/
vi ifcfg-enp0s3

> ONBOOT=yes

>wq!

service network restart
~~~

### xshell 连接虚拟机
~~~
yum install -y net-tools
ifconf  查看IP

VMBOX ->管理 ->全局 -> 网络 -> 端口转发 -> 新建

TCP  主机IP 127.0.0.1:2000 子系统IP 10.0.2.4:22
xshell 配置连接
~~~