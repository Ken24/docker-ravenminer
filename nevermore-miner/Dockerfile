FROM nvidia/cuda:9.1-devel-ubuntu16.04

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
USER ubuntu
WORKDIR /home/ubuntu
ENV HOME /home/ubuntu

RUN echo 'CUDA=/usr/local/cuda' >> $HOME/.bashrc
RUN echo 'export PATH=$PATH:$CUDA/bin' >> $HOME/.bashrc

RUN git config --global http.sslVerify false && git clone https://github.com/brian112358/nevermore-miner.git ccminer
RUN cd ccminer && \
    sed -i -e "s/compat\/curl-for-windows\/openssl\/openssl\/crypto\/sha/openssl/g" api.cpp && \
    chmod 755 ./*.sh && ./build.sh