# Use the Ubuntu 22.04 base image
FROM ubuntu:22.04

LABEL website="sangchul.kr"

ENV TZ=Asia/Seoul

# Use Kakao mirror for Ubuntu repository
RUN sed -i -e 's/kr.archive.ubuntu.com/mirror.kakao.com/g' -e 's/archive.ubuntu.com/mirror.kakao.com/g' /etc/apt/sources.list \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        systemd \
        sudo \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && (cd /lib/systemd/system/sysinit.target.wants/; \
        for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done) \
    && rm -f /lib/systemd/system/multi-user.target.wants/* \
    && rm -f /etc/systemd/system/*.wants/* \
    && rm -f /lib/systemd/system/local-fs.target.wants/* \
    && rm -f /lib/systemd/system/sockets.target.wants/*udev* \
    && rm -f /lib/systemd/system/sockets.target.wants/*initctl* \
    && rm -f /lib/systemd/system/basic.target.wants/* \
    && rm -f /lib/systemd/system/anaconda.target.wants/*

# Set the default command to run systemd
CMD ["/lib/systemd/systemd"]



#####
# docker buildx create --use
# docker buildx build --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:init --no-cache --push .
# docker pull anti1346/ubuntu2204:init
# docker inspect anti1346/ubuntu2204:init --format='{{.Architecture}}'
# docker run -d --privileged --name ubuntu-systemd anti1346/ubuntu2204:init
# docker exec -it ubuntu-systemd bash

