FROM nvidia/cuda:9.0-base-ubuntu16.04

RUN apt-get update && \
        apt-get install -y \
        wget \
        zlib1g-dev \
        libssl-dev \
        curl\
        build-essential \
        cmake \
        git \
        wget \
        unzip \
        yasm \
        pkg-config \
        libswscale-dev \
        libtbb2 \
        libtbb-dev \
        libjpeg-dev \
        libpng-dev \
        libtiff-dev \
        libavformat-dev \
        libpq-dev \
        vim

# install python
RUN wget https://www.python.org/ftp/python/3.6.3/Python-3.6.3.tgz && tar -xvf Python-3.6.3.tgz
RUN cd Python-3.6.3 && ./configure && make && make install
RUN ln -fs /usr/local/bin/python3 /usr/local/bin/python && rm Python-3.6.3.tgz && rm -R Python-3.6.3

# install tensorflow, pytorch
RUN pip3 install --upgrade pip
RUN pip3 install --no-cache-dir torch==1.0.0 torchvision
ENV LANG C.UTF-8