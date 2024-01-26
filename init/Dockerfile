FROM ubuntu:22.04

LABEL website="sangchul.kr"

ENV TZ=Asia/Seoul
ENV container docker

# 우분투 저장소에 카카오 미러를 사용하세요.
RUN sed -i -e 's/kr.archive.ubuntu.com/mirror.kakao.com/g' -e 's/archive.ubuntu.com/mirror.kakao.com/g' /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y \
        systemd systemd-sysv \
        software-properties-common \
        sudo \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    # 불필요한 시스템 단위와 대상을 정리합니다.
    && cd /lib/systemd/system/sysinit.target.wants/ \
    && ls | grep -v 'systemd-tmpfiles-setup' | xargs rm -f $1 \
    && rm -f /lib/systemd/system/multi-user.target.wants/* \
    && rm -f /etc/systemd/system/*.wants/* \
    && rm -f /lib/systemd/system/local-fs.target.wants/* \
    && rm -f /lib/systemd/system/sockets.target.wants/*udev* \
    && rm -f /lib/systemd/system/sockets.target.wants/*initctl* \
    && rm -f /lib/systemd/system/basic.target.wants/* \
    && rm -f /lib/systemd/system/anaconda.target.wants/* \
    && rm -f /lib/systemd/system/plymouth* \
    && rm -f /lib/systemd/system/systemd-update-utmp*

VOLUME ["/sys/fs/cgroup", "/tmp", "/run"]

CMD ["/lib/systemd/systemd"]



#####
# docker buildx create --use
# docker buildx build --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:init --no-cache --push .
# docker pull anti1346/ubuntu2204:init
# docker inspect anti1346/ubuntu2204:init --format='{{.Architecture}}'
# docker run -d --privileged --name ubuntu-systemd anti1346/ubuntu2204:init
# docker exec -it ubuntu-systemd bash



## docker build
```
docker build -t anti1346/ubuntu2204:init . --no-cache
```

## docker push
```
docker push anti1346/ubuntu2204:init
```

## docker pull
```
docker pull anti1346/ubuntu2204:init
```

## docker container run
```
docker run -d --privileged --name ubuntu-init anti1346/ubuntu2204:init
```
```
docker run -d --privileged --name ubuntu-init --volume /sys/fs/cgroup:/sys/fs/cgroup:ro anti1346/ubuntu2204:init

docker run -d --privileged --name ubuntu-init anti1346/ubuntu2204:init

docker run -d --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro anti1346/ubuntu2204:init



docker run -it --tmpfs /tmp --tmpfs /run --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro anti1346/ubuntu2204:init


```

docker inspect my_ubuntu_systemd_container


## entering a running docker container
```
docker exec -it ubuntu-init bash
```



docker run -d --privileged --volume /sys/fs/cgroup:/sys/fs/cgroup:ro anti1346/ubuntu2204:init




docker push anti1346/ubuntu2004:init








docker run -d --privileged --name ubuntu-init --cap-add SYS_ADMIN -v /sys/fs/cgroup:/sys/fs/cgroup:ro anti1346/ubuntu2204:init



















