FROM ubuntu:22.04

LABEL website="sangchul.kr"

# 아키텍처 환경변수 설정
ARG SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD:-root}
ARG DEBIAN_FRONTEND=noninteractive
ARG ARCH=amd64
ARG GOLANG_VERSION 1.20.4

# Go 설치를 위한 환경 변수 설정
ENV SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD}
ENV ARCH $ARCH
ENV GOLANG_VERSION 1.20.4
ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

USER root

# 기본 패키지 업데이트 및 필요한 패키지 설치
RUN apt-get update -qq \
    && apt-get install -qq -y wget \
        sudo \
        curl \
        vim \
        git \
        # ssh \
        # procps \
        # net-tools \
        # iputils-ping \
        # dnsutils \
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && apt-get update

# Go 설치
RUN wget -q https://golang.org/dl/go$GOLANG_VERSION.linux-$ARCH.tar.gz \
    && tar -C /usr/local -xzf go$GOLANG_VERSION.linux-$ARCH.tar.gz \
    && rm go$GOLANG_VERSION.linux-$ARCH.tar.gz

# 작업 디렉토리 생성 및 GOPATH 설정
RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"

RUN echo "root:$SSH_ROOT_PASSWORD" | chpasswd \
    && cp -rf /etc/skel/.bash* /root/. \
    && echo 'export PS1="\[\033[01;32m\]\u\[\e[m\]\[\033[01;32m\]@\[\e[m\]\[\033[01;32m\]\h\[\e[m\]:\[\033[01;34m\]\W\[\e[m\]$ "' >> ~/.bashrc

# 작업 디렉토리 설정
WORKDIR $GOPATH

# 필요한 추가 설정이나 응용 프로그램 코드를 추가적으로 작성하실 수 있습니다.
CMD [ "/bin/bash" ]
