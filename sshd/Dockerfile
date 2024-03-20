# 베이스 이미지 사용
FROM ubuntu:22.04

# 메타데이터 설정
LABEL website="sangchul.kr"

# 환경 변수 설정
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul

ARG SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD:-root}
ARG SSH_USER=${SSH_USER:-ubuntu}
ARG SSH_PASSWORD=${SSH_PASSWORD:-ubuntu}

ENV SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD}
ENV SSH_USER=${SSH_USER}
ENV SSH_PASSWORD=${SSH_PASSWORD}

# root 권한으로 진행
USER root

# 패키지 소스 업데이트 및 필요한 패키지 설치
RUN sed -i 's/archive.ubuntu.com/mirror.kakao.com/g' /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        systemd \
        build-essential \
        openssh-server \
        sudo \
        passwd \
        apt-utils \
        aptitude \
        dnsutils \
        iputils-ping \
        net-tools \
        netcat \
        curl \
        ssh \
        telnet \
        traceroute \
        vim \
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

# 시간대 설정
RUN echo $TZ > /etc/timezone

# root 사용자 설정
RUN echo "root:$SSH_ROOT_PASSWORD" | chpasswd \
    && cp -rf /etc/skel/.bash* /root/. \
    && echo 'export PS1="\[\033[01;32m\]\u\[\e[m\]\[\033[01;32m\]@\[\e[m\]\[\033[01;32m\]\h\[\e[m\]:\[\033[01;34m\]\W\[\e[m\]$ "' >> ~/.bashrc \
    && ssh-keygen -A

# 추가 사용자 설정
RUN useradd -c "$SSH_USER" -m -d /home/$SSH_USER -s /bin/bash $SSH_USER \
    && usermod -aG sudo $SSH_USER \
    && echo "$SSH_USER:$SSH_PASSWORD" | chpasswd \
    && echo 'export PS1="\[\e[33m\]\u\[\e[m\]\[\e[37m\]@\[\e[m\]\[\e[34m\]\h\[\e[m\]:\[\033[01;31m\]\W\[\e[m\]$ "' >> /home/$SSH_USER/.bashrc \
    && echo "$SSH_USER ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# SSH Configure Settings
RUN mkdir /var/run/sshd \
    && sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/g' /etc/ssh/sshd_config \
    && sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/g' /etc/ssh/sshd_config \
    && sed -i 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

# SSH 포트 열기
EXPOSE 22

# systemd를 기본 명령으로 사용하도록 설정
CMD ["/lib/systemd/systemd"]
