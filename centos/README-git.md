centos 安装 git
~~~
 docker run --name=centos7 -itd centos:7
~~~

~~~
# 查看是否有自带的git
git --version

# 有的话卸载自带的低版本
yum remove git

# 有必要就安装 vim
yum -y install vim-enhanced


# 安装前要手动安装下依赖包
yum install -y wget
yum install -y gcc-c++
yum install -y zlib-devel perl-ExtUtils-MakeMaker
yum install -y gettext
yum install -y make

# 去官网下载最新版本的git源码包
wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.9.0.tar.gz

# 接下来就是解压，配置，安装
tar -zxvf git-2.9.0.tar.gz
cd git-2.9.0
./configure --prefix=/usr/local
make
sudo make install

# 查看git版本
git --version
~~~

~~~
git config --global user.name "nirvana72"
git config --global user.email "15279663@qq.com"

# 查看git配置
git config --global  --list

# 安装 ssh
yum install openssh-clients.x86_64 

# 生成公钥和私钥（用于github）
# 生成过程中， 文件位置[可默认 /root/.ssh], 密码
ssh-keygen -t rsa -C "15279663@qq.com"

# id_rsa.pub 内容添加到github

# 测试连接
ssh git@github.com
~~~


 docker run --name=centos7_test -p 80:80 -v D:/workspace:/workspace -itd centos:7