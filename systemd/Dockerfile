FROM ubuntu:22.04

LABEL website="sangchul.kr"

ARG SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD:-root}
ARG DEBIAN_FRONTEND=noninteractive

ENV SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD}
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul

USER root

# systemd를 포함한 필수 패키지 설치
RUN apt-get update \
    && apt-get install -y \
        systemd \
        sudo \
        passwd \
        curl \
        procps \
        net-tools \
        iputils-ping \
        dnsutils \
        openssh-server \
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# 표준 시간대 설정
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN sed -i -e 's/^#PermitRootLogin prohibit-password/PermitRootLogin yes/' \
    -e 's/^#PasswordAuthentication yes/PasswordAuthentication yes/' \
    -e 's/^UsePAM yes/#UsePAM yes/' "/etc/ssh/sshd_config"

# root 사용자의 비밀번호를 설정하고 bash 프롬프트를 구성
RUN echo "root:${SSH_ROOT_PASSWORD}" | chpasswd \
    && echo 'export PS1="\[\e[33m\]\u\[\e[m\]\[\e[37m\]@\[\e[m\]\[\e[34m\]\h\[\e[m\]:\[\033[01;31m\]\W\[\e[m\]$ "' >> /root/.bashrc

EXPOSE 22

# systemd를 기본 명령으로 사용하도록 설정
CMD ["/lib/systemd/systemd"]
