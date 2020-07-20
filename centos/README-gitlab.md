# centos gitlab安装

docker run --name=gitlab -p 9000:9000 --privileged=true -itd centos:7 /usr/sbin/init
   // --restart always


### 安装依赖
~~~
yum update
yum install -y curl policycoreutils-python openssh-server wget vim firewalld postfix
systemctl enable sshd
systemctl start sshd
~~~

### 防火墙
~~~
systemctl start firewalld
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=https
systemctl reload firewalld
~~~

### postfix 邮件服务
~~~
vim /etc/postfix/main.cf
# inet_interfaces = all

systemctl enable postfix
systemctl start postfix
~~~

### 下载gitlab
~~~
wget https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el7/gitlab-ce-13.1.2-ce.0.el7.x86_64.rpm
~~~

### 安装gitlab
~~~
rpm -i gitlab-ce-13.1.2-ce.0.el7.x86_64.rpm
~~~

### 配置
~~~
vim  /etc/gitlab/gitlab.rb
external_url 'http://gitlab.nij.local'

# 如果使用端口号
# external_url 'http://gitlab.nij.local:9000'
# 防火墙开放端口
# firewall-cmd --zone=public --add-port=9000/tcp --permanent
# firewall-cmd --reload
~~~

# 重启
~~~
gitlab-ctl reconfigure
# 如果这一步卡住， 新开一个终端 /opt/gitlab/embedded/bin/runsvdir-start

gitlab-ctl restart
# 重启失败的话先执行 /opt/gitlab/embedded/bin/runsvdir-start
~~~


### CICD
1. 一台可以访问 gitlab的服务器
2. 拉取时如果访问的是域名,需要配置host
~~~
[root@3a676d2e1965 etc]# cat hosts
127.0.0.1	localhost
::1	localhost ip6-localhost ip6-loopback
fe00::0	ip6-localnet
ff00::0	ip6-mcastprefix
ff02::1	ip6-allnodes
ff02::2	ip6-allrouters
172.17.0.3	3a676d2e1965
172.17.0.2	gitlab.nij.local 
~~~

3. 安装gitlab runner
> https://docs.gitlab.com/runner/install/linux-repository.html

3. 2 默认 yum 安装的git版本太低， 有可能造成功能不可用
3. 3 升级默认的git 版本至  2.26
> README-git.MD


4. 注册 runner
> https://docs.gitlab.com/runner/register/index.html

> 注册成功可以查看注册配置信息
> cat ~/.gitlab-runner/config.toml // 仅 mac 下测试
5. 项目中写 gitlab-ci.yml
~~~
stages:
  - build
  - deploy-test
  - deploy-prod

cache:
  key: ${CI_BUILD_REF_NAME}
  paths:
    - node_modules/

job1:
  stage: build
  only:
    - master
  script:
    - cd /workspace/demo.gitlab.vue
    - npm install
  tags: 
    - vue-demo

job2:
  stage: deploy-test
  only:
    - master
  script:
    - cd /workspace/demo.gitlab.vue
    - npm run build:test
    - cp -r dist/* /workspace/demo.gitlab.vue-test/
  tags: 
    - vue-demo

job3:
  stage: deploy-prod
  only:
    - master
  script:
    - cd /workspace/demo.gitlab.vue
    - npm run build
    - cp -r dist/* /workspace/demo.gitlab.vue-prod/
  when: manual
  tags: 
    - vue-demo
~~~

### 发布结果测试
1. 安装nginx
~~~
yum install -y nginx
cd /etc/nginx/conf.d
~~~

2. test 服务器
> vim vue-test.nij.local.conf
~~~
server {
    listen       8080;
    server_name vue-test.nij.local;
    index index.html;
    root /workspace/demo.gitlag.vue-test;

    # location / {
        
    # }

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
~~~

3. prod 服务器
> vim vue.nij.local.conf
~~~
server {
    listen       8080;
    server_name vue.nij.local;
    index index.html;
    root /workspace/demo.gitlag.vue-prod;

    # location / {
        
    # }

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
~~~