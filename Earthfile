VERSION 0.7
FROM ubuntu:18.04
WORKDIR /collimator


base-apt:
    USER root

    RUN if [ `uname -m` != 'aarch64' ] ; then echo "This image is for arm64 only" ; exit 1 ; fi

    RUN apt-get update && apt-get install -y build-essential wget curl git \
        libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev libffi-dev \
        sudo

    RUN useradd -m ubuntu && echo "ubuntu:ubuntu" | chpasswd && adduser ubuntu sudo
    RUN echo "ubuntu ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
    RUN chown -R ubuntu:ubuntu /collimator
    USER ubuntu


all:
    FROM +base-apt

    COPY . ./

    ARG VERSION=3.11
    RUN bash ./build_python3.sh --version $VERSION
