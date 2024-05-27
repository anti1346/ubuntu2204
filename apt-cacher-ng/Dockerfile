FROM ubuntu:22.04

LABEL website="sangchul.kr"

ARG DEBIAN_FRONTEND=noninteractive
ARG SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD:-root}

ENV SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD}
ENV DEBIAN_FRONTEND noninteractive

USER root

# apt 패키지 리스트 업데이트 및 apt-cacher-ng 설치
# RUN apt-get update && apt-get install -y apt-cacher-ng

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        apt-utils \
        sudo \
        passwd \
        wget \
        curl \
        procps \
        iputils-ping \
        dnsutils \
        net-tools \
        locales \
        ssh \
        vim \
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# # apt-cacher-ng의 설정 파일 업데이트
# RUN sed -i 's/# ForeGround: 0/ForeGround: 1/' /etc/apt-cacher-ng/acng.conf \
#     && sed -i 's/# BindAddress: localhost/BindAddress: 0.0.0.0/' /etc/apt-cacher-ng/acng.conf

RUN echo "root:$SSH_ROOT_PASSWORD" | chpasswd \
    && cp -rf /etc/skel/.bash* /root/. \
    && echo 'export PS1="\\[\\033[01;32m\\]\\u\\[\\e[m\\]\\[\\033[01;32m\\]@\\[\\e[m\\]\\[\\033[01;32m\\]\\h\\[\\e[m\\]:\\[\\033[01;34m\\]\\W\\[\\e[m\\]\\$ "' >> ~/.bashrc

# # 컨테이너에서 사용할 포트 공개
# EXPOSE 3142

# # apt-cacher-ng 실행
# CMD /etc/init.d/apt-cacher-ng start && tail -f /var/log/apt-cacher-ng/*

# 만약 Dockerfile이 완료된 후 실행하려는 커맨드가 있다면 아래의 주석을 해제하여 추가할 수 있습니다.
# CMD ["apt-cacher-ng", "start"]
CMD ["/bin/bash"]