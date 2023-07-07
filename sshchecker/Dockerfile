FROM nginx:1.25

LABEL website="sangchul.kr"

ARG DEBIAN_FRONTEND=noninteractive
ARG SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD:-root}

ENV SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD}
ENV TZ=Asia/Seoul

USER root

RUN apt-get update -qq \
    && apt-get install -qq -y lsb-release \
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
        python3 \
        python3-pip \
        python3-dnspython \
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && apt-get update -qq

RUN sudo pip install dnspython

RUN sudo ln -s /usr/bin/python3 /usr/bin/python

RUN git clone https://github.com/anti1346/SSL-Certificate-Verify.git .

RUN echo "root:$SSH_ROOT_PASSWORD" | chpasswd \
    && cp -rf /etc/skel/.bash* /root/. \
    && echo 'export PS1="\\[\\033[01;32m\\]\\u\\[\\e[m\\]\\[\\033[01;32m\\]@\\[\\e[m\\]\\[\\033[01;32m\\]\\h\\[\\e[m\\]:\\[\\033[01;34m\\]\\W\\[\\e[m\\]\\$ "' >> ~/.bashrc

CMD ["/usr/bin/bash"]
