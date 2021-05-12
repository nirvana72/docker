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
yum install -y wget gcc-c++ zlib-devel perl-ExtUtils-MakeMaker gettext libcurl-devel curl-devel make

# 去官网下载最新版本的git源码包
wget https://www.kernel.org/pub/software/scm/git/git-2.31.1.tar.xz 

# 接下来就是解压，配置，安装
xz -d git-2.31.1.tar.xz
tar xvf git-2.31.1.tar
cd git-2.31.1
./configure --prefix=/usr/local
make
sudo make install

# 查看git版本 需要重启终端
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

## gitlab-runner

### 方法1 yum， 这种方法安装的runner版本比较老， 但也能用
~~~
# 添加yum源
curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-ci-multi-runner/script.rpm.sh | sudo bash

# 安装runner
yum install gitlab-ci-multi-runner

# 向GitLab-CI注册runner
gitlab-ci-multi-runner register
~~~

### 方法2 官方安装
https://docs.gitlab.com/runner/install/linux-manually.html
~~~
# 下载
curl -LJO "https://gitlab-runner-downloads.s3.amazonaws.com/latest/rpm/gitlab-runner_amd64.rpm"

# 安装
rpm -i gitlab-runner_amd64.rpm

# 注册
gitlab-runner register
~~~

## gitlab-runner 权限问题
~~~
#查看当前runner用户
ps aux|grep gitlab-runner  

#删除gitlab-runner
sudo gitlab-runner uninstall  

#安装并设置--user(例如我想设置为root)
gitlab-runner install --working-directory /home/gitlab-runner --user root   

#重启gitlab-runner
sudo service gitlab-runner restart  

#再次执行会发现--user的用户名已经更换成root了
ps aux|grep gitlab-runner 
~~~