---
title: Docker编译安装GmSSL
date: 2021-10-07 09:15:39
tags:
  - docker
  - GmSSL
  - OpenSSL
  - centos
image: ../images/WechatIMG98.jpeg
---
    版本：
    centos：7
    OpenSSL: 1.1.1
    GmSSL: v1
---

GmSSL资料比较少，用的也不多，踩了很多坑，整理个docker版本的，Centos7默认提供的openssl版本是1.0.2的，GmSSL依赖1.1以上版本，所以要先安装openssl 1.1以上版本

---
Dockerfile文件如下:

```

FROM centos:7
WORKDIR  /usr/local/gmssl
RUN yum -y install perl make gcc gcc-c++ libstdc++-devel pcre-devel zlib-devel net-tools pcre wget zip unzip openssl openssl-devel && \
yum clean all && \
wget https://github.com/guanzhi/GmSSL/archive/master.zip && unzip master.zip
RUN cd GmSSL-master/ && \
./config && \
make && \
make install

```