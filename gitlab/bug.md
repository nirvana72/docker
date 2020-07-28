// 迁移过来的老项目， 如果CICD 500

进入容器
docker exec -it gitlab /bin/bash

执行DB控制台
gitlab-rails dbconsole

执行SQL
update projects set runners_token = null, runners_token_encrypted = null where name = 'vue_58';
