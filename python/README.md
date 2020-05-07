docker run --name=centos7_python -p 80:5000 -v D:/workspace:/workspace -itd centos:7

### 下载
~~~
yum install -y wget
cd /usr/local
wget https://www.python.org/ftp/python/3.8.2/Python-3.8.2.tgz

// 如果下载慢， 可从windows上下载
// cp /workspace/temp/Python-3.8.2.tgz /usr/local
~~~

### 安装
~~~
# tar -zxvf Python-3.8.2.tgz  ！解压

# cd Python-3.8.2

# 安装依赖
# yum -y install libffi-devel zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gcc make

# ./configure  ！检查当前环境是否满足要安装软件的依赖关系

# make && make install  ！编译
~~~

### 环境变量
~~~
yum install -y vim
vim ~/.bash_profile

> PATH=$PATH:$HOME/bin:/usr/local/Python-3.8.2

source ~/.bash_profile
~~~

### 创建一个虚拟环境
~~~
cd 项目目录
python3 -m venv venv
~~~

### 激活虚拟环境
~~~
. venv/bin/activate
~~~

### 安装 Flask
~~~
pip3 install Flask
~~~

### hello wrold
app.py
~~~
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'
~~~

~~~
$ export FLASK_APP=hello.py
$ flask run 
// flask run --host=0.0.0.0
~~~