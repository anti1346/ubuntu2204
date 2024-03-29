# Use the Ubuntu 22.04 base image
FROM ubuntu:22.04

LABEL website="sangchul.kr"

ARG DEBIAN_FRONTEND=noninteractive
ARG SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD:-root}

ENV SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD}
ENV TZ=Asia/Seoul

USER root

# Use Kakao mirror for Ubuntu repository
RUN sed -i -e 's/kr.archive.ubuntu.com/mirror.kakao.com/g' -e 's/archive.ubuntu.com/mirror.kakao.com/g' /etc/apt/sources.list \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        systemd \
        sudo \
        procps \
        net-tools \
        iputils-ping \
        dnsutils \
        curl \
        # openssh-server \
        # vim \
        # git \
    && apt-get clean \
    && apt-get autoremove -y \
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

# 표준 시간대 설정
RUN echo $TZ > /etc/timezone

# root 사용자의 비밀번호를 설정하고 bash 프롬프트를 구성
RUN echo "root:$SSH_ROOT_PASSWORD" | chpasswd \
    && echo 'export PS1="\[\e[33m\]\u\[\e[m\]\[\e[37m\]@\[\e[m\]\[\e[34m\]\h\[\e[m\]:\[\033[01;31m\]\W\[\e[m\]$ "' >> ~/.bashrc

# Set the default command to run systemd
CMD ["/lib/systemd/systemd"]


#####
# docker buildx create --use
# docker buildx build --platform linux/amd64,linux/arm64 --tag anti1346/ubuntu2204:init --no-cache --push .
# docker run -d --privileged --name ubuntu-systemd anti1346/ubuntu2204:init
# docker exec -it ubuntu-systemd bash
