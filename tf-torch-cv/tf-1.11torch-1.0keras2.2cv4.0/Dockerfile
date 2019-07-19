FROM nvidia/cuda:9.0-cudnn7-devel

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
        libgl1-mesa-glx \
        vim

# install miniconda
RUN wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O Miniconda.sh && \
	/bin/bash Miniconda.sh -b -p /opt/conda && \
	rm Miniconda.sh

ENV PATH /opt/conda/bin:$PATH
RUN ln -s /opt/conda/bin/pip /opt/conda/bin/pip3

# setup python
RUN conda install python=3.6
# install conda opencv for dependency pip install opencv-python
RUN conda install -c conda-forge opencv -y

# install tensorflow, pytorch, keras
RUN pip3 install --upgrade pip && \
        pip3 install --no-cache-dir tensorflow-gpu==1.11.0 \
        torch==1.0.0 \
        keras==2.2.4 \
        torchvision \
        numpy \
        opencv-python \
        visdom \
        pandas \
        scikit-learn


ENV LANG C.UTF-8
WORKDIR /