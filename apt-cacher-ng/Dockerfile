FROM ubuntu:22.04

LABEL website="sangchul.kr"

ARG DEBIAN_FRONTEND=noninteractive
ARG SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD:-root}

# 환경 변수 설정 (선택 사항)
ENV SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD}
ENV DEBIAN_FRONTEND noninteractive

USER root

# apt 패키지 리스트 업데이트 및 apt-cacher-ng 설치
# RUN apt-get update && apt-get install -y apt-cacher-ng

RUN apt-get update \
    && apt-get install -y \
        sudo \
        curl \
        wget \
        ssh \
        vim \
        procps \
        net-tools \
        iputils-ping \
        dnsutils \
        git \
        locales \
        apt-cacher-ng \
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && apt-get update

# apt-cacher-ng의 설정 파일 업데이트
RUN sed -i 's/# ForeGround: 0/ForeGround: 1/' /etc/apt-cacher-ng/acng.conf

# apt-cacher-ng를 0.0.0.0:3142로 listen하도록 설정 (모든 IP에 대해 접근 가능)
RUN sed -i 's/# BindAddress: localhost/BindAddress: 0.0.0.0/' /etc/apt-cacher-ng/acng.conf

RUN echo "root:$SSH_ROOT_PASSWORD" | chpasswd \
    && cp -rf /etc/skel/.bash* /root/. \
    && echo 'export PS1="\\[\\033[01;32m\\]\\u\\[\\e[m\\]\\[\\033[01;32m\\]@\\[\\e[m\\]\\[\\033[01;32m\\]\\h\\[\\e[m\\]:\\[\\033[01;34m\\]\\W\\[\\e[m\\]\\$ "' >> ~/.bashrc

# 컨테이너에서 사용할 포트 공개
EXPOSE 3142

# apt-cacher-ng 실행
CMD /etc/init.d/apt-cacher-ng start && tail -f /var/log/apt-cacher-ng/*

# 만약 Dockerfile이 완료된 후 실행하려는 커맨드가 있다면 아래의 주석을 해제하여 추가할 수 있습니다.
# CMD ["apt-cacher-ng", "start"]