~~~
docker run --name=centos7-java -itd -p 8080:8080 -v /Users/nijia/workspace:/workspace -w /workspace centos:7
~~~

### spring-boot 环境
~~~
// 工具
yum install -y which zip unzip

// java 
yum install java-1.8.0-openjdk* -y

// Maven
yum install -y maven 

// sdkman
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"

// spring-boot cli
sdk install springboot
spring --version
~~~

### 创建项目并运行
~~~
spring init demo-spring-boot
cd demo-spring-boot
mvn spring-boot:run
~~~