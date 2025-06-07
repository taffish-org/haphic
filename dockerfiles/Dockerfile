FROM ghcr.io/taffish-org/intel-oneapi:2025.0.2-0-devel-ubuntu24.04

LABEL maintainer="taffish@163.com"

RUN apt-get update && apt-get install -y curl git gcc g++ make python3-dev python3-pip python3-venv && \
    cd / && python3 -m venv haphicenv && . /haphicenv/bin/activate && \
    pip install --upgrade pip && pip install pysam portion numpy scipy scikit-learn networkx sparse_dot_mkl matplotlib

RUN . /haphicenv/bin/activate && cd / && \
    git clone https://github.com/zengxiaofei/HapHiC.git && \
    ln -s /HapHiC/haphic /usr/local/bin/haphic && \
    haphic check

ENV PATH=/haphicenv/bin:${PATH}
ENV PATH=/HapHiC/utils:${PATH}

# install samtools
RUN apt-get install -y zlib1g-dev libncurses-dev liblzma-dev libbz2-dev libcurl4-gnutls-dev libcrypto++-dev libdeflate-dev && \
    cd / && \
    git clone --recursive https://github.com/samtools/htslib.git && \
    git clone --recursive https://github.com/samtools/samtools.git && \
    cd /samtools/ && make && make install

# install bwa
RUN cd / && \
    curl -LO https://github.com/lh3/bwa/archive/refs/tags/v0.7.18.tar.gz && \
    tar -zxvf /v0.7.18.tar.gz && rm /v0.7.18.tar.gz && \
    cd /bwa-0.7.18/ && make && \
    cp /bwa-0.7.18/bwa                /usr/local/bin/ && \
    cp /bwa-0.7.18/qualfa2fq.pl       /usr/local/bin/ && \
    cp /bwa-0.7.18/xa2multi.pl        /usr/local/bin/ && \
    cp /bwa-0.7.18/bwakit/run-HLA     /usr/local/bin/ && \
    cp /bwa-0.7.18/bwakit/run-bwamem  /usr/local/bin/ && \
    cp /bwa-0.7.18/bwakit/run-gen-ref /usr/local/bin/ && \
    cp /bwa-0.7.18/bwakit/typeHLA.sh  /usr/local/bin/

# install samblaster
RUN cd / && \
    curl -LO https://github.com/GregoryFaust/samblaster/releases/download/v.0.1.26/samblaster-v.0.1.26.tar.gz && \
    tar -zxvf /samblaster-v.0.1.26.tar.gz && rm /samblaster-v.0.1.26.tar.gz && \
    cd /samblaster-v.0.1.26/ && \
    make && \
    cp /samblaster-v.0.1.26/samblaster /usr/local/bin/

RUN apt-get install -y default-jdk

ENV TAFFISH_ENV=TAFFISH
ENV TAFFISH_NAME=haphic
