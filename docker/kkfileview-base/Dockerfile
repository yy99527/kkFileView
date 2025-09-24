FROM registry.cn-shanghai.aliyuncs.com/mamy-ns/ubuntu:24.04
 
RUN sed -i 's@//.*archive.ubuntu.com@//mirrors.aliyun.com@g' /etc/apt/sources.list &&\
    sed -i 's@//security.ubuntu.com@//mirrors.aliyun.com@g' /etc/apt/sources.list &&\
    sed -i 's@//ports.ubuntu.com@//mirrors.aliyun.com@g' /etc/apt/sources.list
 
ENV DEBIAN_FRONTEND=noninteractive
 
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates openjdk-8-jre tzdata locales xfonts-utils fontconfig \
        software-properties-common && \
    add-apt-repository ppa:libreoffice/ppa && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        libreoffice-nogui \
        libreoffice-core-nogui \
        fonts-noto \
        fonts-noto-cjk \
        fonts-wqy-microhei \
        fonts-dejavu
 
RUN echo 'Asia/Shanghai' > /etc/timezone &&\
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime &&\
    localedef -i zh_CN -c -f UTF-8 -A /usr/share/locale/locale.alias zh_CN.UTF-8 &&\
    locale-gen zh_CN.UTF-8 &&\
    apt-get install -y --no-install-recommends ttf-mscorefonts-installer &&\
    apt-get install -y --no-install-recommends ttf-wqy-microhei ttf-wqy-zenhei xfonts-wqy &&\
        apt-get autoremove -y &&\
    apt-get clean &&\
    rm -rf /var/lib/apt/lists/*
 
# 内置一些常用的中文字体，避免普遍性乱码
ADD fonts/* /usr/share/fonts/chinese/
 
RUN cd /usr/share/fonts/chinese &&\
    # 安装字体
    mkfontscale &&\
    mkfontdir &&\
    fc-cache -fv
 
ENV LANG=zh_CN.UTF-8 LC_ALL=zh_CN.UTF-8
