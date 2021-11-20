FROM centos:7

LABEL os_version = "centos7"
LABEL python_version = "python3.10"
LABEL golang_version = "golang-1.17"
LABEL author = "lijixiang723@163.com"

WORKDIR /root/


ADD  CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo

COPY ./*.tar.gz /root/

RUN yum clean all && yum makecache && \
    yum -y install gcc gcc-c++ wget automake autoconf libtool make zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel libffi-devel && \
    mkdir -p /usr/local/python3 && \
    mkdir -p /root/.pip && \
    tar -C /usr/local/ -zxvf /root/go1.17.3.linux-amd64.tar.gz && \
    tar -zxvf /root/Python-3.10.0.tar.gz && \
    rm -rf /root/*.tar.gz && \
    cd /root/Python-3.10.0 && \
    ./configure --prefix=/usr/local/python3 && \
    make && \
    make install && \
    rm -rf /root/Python-3.10.0 && \
    ln -s /usr/local/python3/bin/python3.10 /usr/bin/python3 && \
    ln -s /usr/local/python3/bin/pip3.10 /usr/bin/pip3

ADD  ./.pip /root/.pip/

ENV LANG=zh_CN.UTF-8 \
    LANGUAGE=zh_CN:zh \
    LC_ALL=zh_CN.UTF-8 \
    GOPATH=/root/go/ \
    GOROOT=/usr/local/go/ \
    GO111MODULE=on \
    CGO_ENABLED=0 \
    GOOS=linux \
    GOARCH=amd64 \
    GOPROXY="https://goproxy.cn,direct" \
    PATH=$PATH:/usr/local/go/bin/