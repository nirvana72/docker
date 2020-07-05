yum install -y curl policycoreutils-python openssh-server wget vim firewalld postfix
systemctl enable sshd
systemctl start sshd

systemctl start firewalld
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=https
systemctl reload firewalld

vim /etc/postfix/main.cf
inet_interfaces = all

systemctl enable postfix
systemctl start postfix


wget https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el7/gitlab-ce-13.1.2-ce.0.el7.x86_64.rpm
rpm -i gitlab-ce-13.1.2-ce.0.el7.x86_64.rpm

vim  /etc/gitlab/gitlab.rb
external_url 'http://gitlab.nij.local'

gitlab-ctl reconfigure
# 如果这一步卡住， 新开一个终端 /opt/gitlab/embedded/bin/runsvdir-start

gitlab-ctl restart



# 重启失败 执行 /opt/gitlab/embedded/bin/runsvdir-start