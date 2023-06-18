FROM --platform=linux/amd64 ubuntu:22.04

LABEL author="MG8853" maintainer="TeamFelNull"

RUN useradd -d /home/container -m container

ENV LANG C.UTF-8

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y \
    && apt-get install -y sudo git curl unzip git build-essential \
    ca-certificates openssl tar sqlite3 fontconfig tzdata iproute2 jq

RUN cd /srv && mkdir jvm && cd jvm && \
    curl https://download.oracle.com/graalvm/17/latest/graalvm-jdk-17_linux-x64_bin.tar.gz && \
    tar -xzvf graalvm-jdk-17_linux-x64_bin.tar.gz --strip-components 1 && rm graalvm-jdk-17_linux-x64_bin.tar.gz

ENV PATH=/srv/jvm/bin:$PATH
ENV JAVA_HOME=/srv/jvm

USER container
ENV USER=container HOME=/home/container

WORKDIR /home/container

COPY entrypoint.sh /entrypoint.sh

CMD ["/bin/bash", "/entrypoint.sh"]
