FROM centos:6

RUN yum install -y yum-utils
RUN yum install -y centos-release-scl
RUN yum-config-manager --enable rhel-server-rhscl-7-rpms
RUN yum install -y devtoolset-4-gcc
RUN yum install -y devtoolset-4-gcc-c++
RUN yum install -y devtoolset-4-gcc-gfortran
RUN yum install -y devtoolset-4-binutils
RUN yum install -y git19
RUN yum install -y python27
ENV PATH=/opt/rh/git19/root/usr/bin:/opt/rh/python27/root/usr/bin:/opt/rh/devtoolset-4/root/usr/bin:$PATH 
ENV LD_LIBRARY_PATH=/opt/rh/gti19/root/usr/lib64:/opt/rh/python27/root/usr/lib64:/opt/rh/devtoolset-4/root/usr/lib64:/opt/rh/devtoolset-4/root/usr/lib:$LD_LIBRARY_PATH 
ENV PKG_CONFIG_PATH=/opt/rh/git19/root/usr/lib64/pkgconfig:/opt/rh/python27/root/usr/lib64/pkgconfig:${PKG_CONFIG_PATH}

RUN yum install -y wget curl zip unzip

RUN curl -L https://github.com/google/protobuf/archive/v3.1.0.tar.gz -o /tmp/protobuf-v3.1.0.tar.gz \
    && cd /tmp \
    && yum install -y autoconf automake libtool unzip \
    && tar xvf protobuf-v3.1.0.tar.gz \
    && cd protobuf-3.1.0 \
    && ./autogen.sh \
    && ./configure \
    && make \
    && make install \
    && ldconfig

# Install cmake>=3.1
RUN mkdir -p /tmp/deps \
    && yum install -y cmake \
    && cd /tmp/deps \
    && curl -L https://cmake.org/files/v3.1/cmake-3.1.3.tar.gz -o cmake-3.1.3.tar.gz \
    && tar xf cmake-3.1.3.tar.gz \
    && cd cmake-3.1.3 \
    && mkdir build && cd build && cmake .. && make && make install \
    && cd / && rm -rf /tmp/deps

RUN cd /tmp \
    && wget http://nixos.org/releases/patchelf/patchelf-0.9/patchelf-0.9.tar.bz2 \
    && tar xfa patchelf-0.9.tar.bz2 \
    && cd patchelf-0.9 \
    && ./configure \
    && make \
    && make install

# Conda environment for Python3 versions
RUN wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh \
     && bash Miniconda3-latest-Linux-x86_64.sh -b -p /opt/miniconda3 \
     && rm -rf Miniconda3-latest-Linux-x86_64.sh
ENV PATH /opt/miniconda3/bin:$PATH
RUN chmod -R ugo+w /opt/miniconda3
