

docker pull gitlab/gitlab-runner:alpine-v13.2.0
docker run --name=gitlab-runner-1 --privileged=true --rm -d -v /var/run/docker.sock:/var/run/docker.sock -v /srv/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner:alpine-v13.2.0
docker exec -it gitlab-runner-1 /bin/bash
gitlab-runner register


/srv/gitlab-runner/config/config.toml

[[runners]]
  name = "docker-runner-1"
  url = "http://gitlab.lan8.cn"
  token = "Kb4vzEoHHiAzxpYFjERw"
  executor = "docker"
  [runners.custom_build_dir]
  [runners.cache]
    [runners.cache.s3]
    [runners.cache.gcs]
  [runners.docker]
    tls_verify = false
    image = "docker:latest"
    privileged = true
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["/cache","/var/run/docker.sock:/var/run/docker.sock"]
    shm_size = 0

