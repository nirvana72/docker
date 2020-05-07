### centos 安装 git
~~~
docker run --name=centos7_nodejs -p 80:80 -v D:/workspace:/workspace -itd centos:7
~~~

### 安装
~~~
# 查看nodejs版本
node -v

# 安装前提
yum install -y wget

# 下载nodejs
cd /usr/src
wget https://npm.taobao.org/mirrors/node/v14.0.0/node-v14.0.0-linux-x64.tar.xz

# 解压
tar xvf node-v14.0.0-linux-x64.tar.xz

# 删除包
rm node-v14.0.0-linux-x64.tar.xz

# 重命名文件夹
mv node-v14.0.0-linux-x64 node

# 进入node文件夹，测试执行
cd node/bin
./node -v
~~~

### 配置全局

~~~
yum install -y vim-enhanced
vim ~/.bash_profile
~~~

> PATH=$PATH:$HOME/bin:/usr/src/node/bin

### 重载
~~~
source ~/.bash_profile

node -v
npm -v

# 避免每次都要执行 source ~/.bash_profile
# vim .bashrc
> PATH=$PATH:$HOME/bin:/usr/src/node/bin
~~~