docker run --name=centos7_python -p 80:80 -v D:/workspace:/workspace -itd centos:7

### 下载
~~~
yum install -y wget
wget https://www.python.org/ftp/python/3.8.2/Python-3.8.2.tar.xz
~~~

### 安装
~~~
# tar -zxvf Python-3.8.2.tgz  ！解压

# cd Python-3.8.2

# yum -y install libffi-devel zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gcc make ！安装相关依赖

# ./configure  ！检查当前环境是否满足要安装软件的依赖关系

# make && make install  ！编译
~~~

### 环境
~~~
yum install -y vim-enhanced
vim ~/.bash_profile

> PATH=$PATH:$HOME/bin:/root/Python-3.8.2

source ~/.bash_profile
~~~

### flask
~~~
# virtualenv 类似于 npm composer 项目独立依赖环境
pip3 install virtualenv

# 依赖包目录名
virtualenv env

# 指定依赖包目录
source env/bin/activate

# 指定了独立环境后， 安装的依赖都是项目独立了
pip3 install flask
~~~