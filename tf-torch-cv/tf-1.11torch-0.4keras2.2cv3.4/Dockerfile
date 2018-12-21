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
        vim

# install python
RUN wget https://www.python.org/ftp/python/3.5.6/Python-3.5.6.tgz && tar -xvf Python-3.5.6.tgz
RUN cd Python-3.5.6 && ./configure && make && make install
RUN ln -fs /usr/local/bin/python3 /usr/local/bin/python && rm Python-3.5.6.tgz && rm -R Python-3.5.6

# install tensorflow, pytorch, keras
RUN pip3 install --upgrade pip
RUN pip3 install --no-cache-dir tensorflow-gpu==1.11.0 torch==0.4.1 keras==2.2.4 torchvision

# install opencv
WORKDIR /
ENV OPENCV_VERSION="3.4.3"
RUN wget https://github.com/opencv/opencv/archive/${OPENCV_VERSION}.zip \
&& unzip ${OPENCV_VERSION}.zip \
&& mkdir /opencv-${OPENCV_VERSION}/cmake_binary \
&& cd /opencv-${OPENCV_VERSION}/cmake_binary \
&& cmake -DBUILD_TIFF=ON \
  -DBUILD_opencv_java=OFF \
  -DWITH_CUDA=OFF \
  -DWITH_OPENGL=ON \
  -DWITH_OPENCL=ON \
  -DWITH_IPP=ON \
  -DWITH_TBB=ON \
  -DWITH_EIGEN=ON \
  -DWITH_V4L=ON \
  -DBUILD_TESTS=OFF \
  -DBUILD_PERF_TESTS=OFF \
  -DCMAKE_BUILD_TYPE=RELEASE \
  -DCMAKE_INSTALL_PREFIX=$(python -c "import sys; print(sys.prefix)") \
  -DPYTHON_EXECUTABLE=$(which python) \
  -DPYTHON_INCLUDE_DIR=$(python -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())") \
  -DPYTHON_PACKAGES_PATH=$(python -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())") \
  .. \
&& make install \
&& rm /${OPENCV_VERSION}.zip \
&& rm -r /opencv-${OPENCV_VERSION}

# link cv to python library
RUN ln -sf /usr/local/python/cv2 /usr/local/lib/python3.5/site-packages

ENV LANG C.UTF-8