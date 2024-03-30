# 使用Ubuntu 20.04作为基础镜像
FROM ubuntu:20.04

# 安装必要的软件包
RUN apt-get update && \
    apt-get install -y binutils net-tools git autoconf make gcc g++ libreadline-dev dos2unix lrzsz unzip wget build-essential autoconf automake libtool

# 下载boost 1.74.0源码并进行安装
WORKDIR /
RUN wget https://boostorg.jfrog.io/artifactory/main/release/1.74.0/source/boost_1_74_0_rc1.tar.gz && \
    tar -xvf boost_1_74_0_rc1.tar.gz && \
    cd boost_1_74_0/ && \
    ls && \
    ./bootstrap.sh && \
    ./b2 install --with=all

WORKDIR /

RUN wget https://github.com/google/protobuf/releases/download/v2.6.1/protobuf-2.6.1.tar.gz && \
        tar -zxvf protobuf-2.6.1.tar.gz -C . && \
        cd protobuf-2.6.1/ && \
        ./autogen.sh && \
        ./configure && \
        make && \
        make check  && \
        make install

# 配置动态链接库路径
RUN echo -e "\n/usr/local/lib" | tee -a /etc/ld.so.conf && \
    ldconfig

# 设定工作目录为根目录
WORKDIR /

# 输出提示信息
CMD ["echo", "PokerHub Server Base Docker container built successfully! "]