FROM ubuntu:22.04

# Set metadata labels
LABEL website="sangchul.kr"

# Set environment variables
ARG DEBIAN_FRONTEND=noninteractive
ARG SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD:-root}
ENV SSH_ROOT_PASSWORD=${SSH_ROOT_PASSWORD}
ENV TZ=Asia/Seoul

# Switch to root user
USER root

# Install required packages
RUN apt-get update -qq \
    && apt-get install -qq -y sudo \
        # lsb-release \
        # curl \
        # wget \
        # ssh \
        # vim \
        # procps \
        # net-tools \
        # iputils-ping \
        # dnsutils \
        git \
        python3 \
        python3-pip \
        python3-dnspython \
        nginx \
    && apt-get clean \
    && apt-get autoremove -y \
    && apt-get purge -y --auto-remove \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && apt-get update -qq

# Set root user password and configure bash prompt
RUN echo "root:$SSH_ROOT_PASSWORD" | chpasswd \
    && cp -rf /etc/skel/.bash* /root/. \
    && echo 'export PS1="\\[\\033[01;32m\\]\\u\\[\\e[m\\]\\[\\033[01;32m\\]@\\[\\e[m\\]\\[\\033[01;32m\\]\\h\\[\\e[m\\]:\\[\\033[01;34m\\]\\W\\[\\e[m\\]\\$ "' >> ~/.bashrc

# Install dnspython library
RUN pip install dnspython

# Clone the SSL Certificate Verify repository
RUN git clone https://github.com/anti1346/SSL-Certificate-Verify.git /sslchecker

COPY run_script.sh /sslchecker/run_script.sh

RUN chmod +x /sslchecker/run_script.sh

# Expose port 80
EXPOSE 80

# Set volume
VOLUME ["/sslchecker"]

# Set working directory
WORKDIR /sslchecker

# Execute the script
CMD ["/sslchecker/run_script.sh"]
