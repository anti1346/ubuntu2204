# 베이스 이미지 사용
FROM ubuntu:22.04

# 메타데이터 설정
LABEL website="sangchul.kr"

# 환경 변수 설정
ARG DEBIAN_FRONTEND=noninteractive
ARG SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD:-root}
ARG SSH_USER=${SSH_USER:-ubuntu}
ARG SSH_PASSWORD=${SSH_PASSWORD:-ubuntu}

ENV SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD}
ENV SSH_USER=${SSH_USER}
ENV SSH_PASSWORD=${SSH_PASSWORD}
ENV TZ=Asia/Seoul

# 시간대 설정
RUN echo $TZ > /etc/timezone

# 패키지 소스 업데이트 및 필요한 패키지 설치
RUN sed -i -e 's/kr.archive.ubuntu.com/mirror.kakao.com/g' -e 's/archive.ubuntu.com/mirror.kakao.com/g' /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y \
        sudo \
        apt-utils \
        aptitude \
        python3 \
        python3-pip \
        build-essential \
        libssl-dev \
        libffi-dev \
        curl \
        dnsutils \
        iputils-ping \
        net-tools \
        netcat \
        openssh-server \
        telnet \
        traceroute \
        vim \
        software-properties-common \
        git \
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# 다운로드할 Ansible 버전 및 URL 지정
ARG ansible_version="v2.16.2"
ARG ansible_url="https://github.com/ansible/ansible/archive/refs/tags/${ansible_version}.tar.gz"

# Ansible 소스 다운로드 및 설치
# https://releases.ansible.com/ansible
# RUN curl -fsSL -o /tmp/ansible-latest.tar.gz https://releases.ansible.com/ansible/ansible-latest.tar.gz \
#     && tar -xf /tmp/ansible-latest.tar.gz -C /tmp \
#     && cd /tmp/ansible-* \
#     && python3 setup.py install \
#     && cd / \
#     && rm -rf /tmp/ansible-*

# Ansible 소스 다운로드 및 압축 해제
RUN curl -fsSL -o /tmp/ansible.tar.gz "$ansible_url" \
    && tar -xzf /tmp/ansible.tar.gz -C /tmp \
    && rm /tmp/ansible.tar.gz \
    && cd /tmp/ansible-${ansible_version} \
    && python3 setup.py install \
    && rm -rf /tmp/ansible-${ansible_version}

# SSH Configure Settings
RUN mkdir /var/run/sshd && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/g' /etc/ssh/sshd_config && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/g' /etc/ssh/sshd_config && \
    sed -i 's/#UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config

# root 사용자 설정
RUN echo "root:$SSH_ROOT_PASSWORD" | chpasswd && \
    cp -rf /etc/skel/.bash* /root/. && \
    echo 'export PS1="\[\033[01;32m\]\u\[\e[m\]\[\033[01;32m\]@\[\e[m\]\[\033[01;32m\]\h\[\e[m\]:\[\033[01;34m\]\W\[\e[m\]$ "' >> ~/.bashrc && \
    ssh-keygen -A

# 추가 사용자 설정
RUN useradd -c "$SSH_USER" -m -d /home/$SSH_USER -s /bin/bash $SSH_USER && \
    usermod -aG sudo $SSH_USER && \
    echo "$SSH_USER:$SSH_PASSWORD" | chpasswd && \
    echo 'export PS1="\[\e[33m\]\u\[\e[m\]\[\e[37m\]@\[\e[m\]\[\e[34m\]\h\[\e[m\]:\[\033[01;31m\]\W\[\e[m\]$ "' >> /home/$SSH_USER/.bashrc && \
    echo "$SSH_USER ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# 작업 디렉토리 설정
WORKDIR /ansible

# Expose SSH port
EXPOSE 22

# Start SSH server
CMD ["/usr/sbin/sshd", "-D"]
