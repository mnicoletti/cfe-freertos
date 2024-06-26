FROM --platform=linux/amd64 ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get -qy update \
    && apt-get -y install --no-install-recommends \
        ca-certificates \
        make \
        cmake \
        wget \
        sudo \
        git \
        build-essential \
        vim \
        tree \
        strace \
        ltrace \
        lcov \
        libglib2.0-dev \
        libfdt-dev \
        libpixman-1-dev \
        python3 \
        python3-pip \
        python3-venv \
        zlib1g-dev \
        ninja-build \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip
RUN pip3 install --upgrade sphinx sphinx-rtd-theme

RUN mkdir /home/docker
RUN chown -R 1000:1000 /home/docker

RUN groupadd -g 1000 docker
RUN echo "docker:x:1000:1000:docker,,,:/home/docker:/bin/bash" | tee -a /etc/passwd

RUN mkdir -p /toolchain

RUN wget -qO- https://developer.arm.com/-/media/Files/downloads/gnu-rm/9-2019q4/gcc-arm-none-eabi-9-2019-q4-major-x86_64-linux.tar.bz2 | tar xvj -C /toolchain/

ENV PATH="/toolchain/gcc-arm-none-eabi-9-2019-q4-major/bin:${PATH}"

ADD bashrc /root/.bashrc
ADD bashrc /home/docker/.bashrc
ADD gitconfig /root/.gitconfig
ADD gitconfig /home/docker/.gitconfig

WORKDIR /opt/qemu-iobc
