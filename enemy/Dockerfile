FROM nvidia/cuda:8.0-devel-ubuntu16.04

LABEL maintainer="Ken24 <kenn.nishi@gmail.com>"

RUN apt-get update && apt-get install -y \
    libcurl4-openssl-dev \
    libssl-dev \
    libjansson-dev \
    automake \
    autotools-dev \
    build-essential \
    iproute \
    git \
    wget

RUN nvcc --version
RUN echo 'export PATH=$PATH:/usr/local/cuda/bin' > /etc/profile.d/cuda.sh
RUN echo /usr/local/cuda/lib64 > /etc/ld.so.conf.d/cuda.conf
RUN ldconfig

RUN groupadd -g 1942 ubuntu && \
    useradd -m -u 1942 -g 1942 -d /home/ubuntu ubuntu && \
    echo "ubuntu ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers &&\
    chown -R ubuntu:ubuntu /home/ubuntu

RUN apt-get -y install libglib2.0-dev libgirepository1.0-dev asciidoc python-dev freeglut3-dev libx11-dev libxmu-dev libxi-dev libgl1-mesa-glx libglu1-mesa libglu1-mesa-dev gcc make libcurl4-openssl-dev autoconf git screen libncurses5-dev opencl-headers build-essential protobuf-compiler libprotoc-dev libboost-all-dev libleveldb-dev hdf5-tools libhdf5-serial-dev libopencv-core-dev libopencv-highgui-dev libsnappy-dev libsnappy1v5 libatlas-base-dev cmake libstdc++6-4.9-dbg libgoogle-glog0v5 libgoogle-glog-dev libgflags-dev liblmdb-dev python-pip gfortran libjansson-dev uthash-dev autogen libtool pkg-config gcc-multilib dkms libxml2-dev libxslt1-dev zlib1g-dev linux-image-extra-virtual libopencv-dev python-numpy libssl-dev automake autotools-dev
WORKDIR /root
RUN wget https://megatools.megous.com/builds/megatools-1.9.98.tar.gz && \
    tar -xzf megatools-1.9.98.tar.gz && \
    cd megatools-1.9.98 && \
    ./configure && \
    make && \
    make install

USER ubuntu
WORKDIR /home/ubuntu
ENV HOME /home/ubuntu

RUN echo 'CUDA=/usr/local/cuda' >> $HOME/.bashrc
RUN echo 'export PATH=$PATH:$CUDA/bin' >> $HOME/.bashrc

RUN megadl 'https://mega.nz/#!ADxkjDKJ!h3gyL_Yc_ChGufgt1QOFE4mg01YLF3Cqv2nhhfVkN54' && \
    unzip enemy-1.03.zip -d ./ccminer && \
    chmod +x ./ccminer/ccminer