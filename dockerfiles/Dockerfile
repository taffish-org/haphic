FROM ghcr.io/taffish-org/intel-oneapi:2025.0.2-0-devel-ubuntu24.04

LABEL maintainer="taffish@163.com"

RUN apt-get update && apt-get install -y curl git gcc g++ make python3-dev python3-pip python3-venv && \
    cd / && python3 -m venv haphicenv && . /haphicenv/bin/activate && \
    pip install --upgrade pip && pip install pysam portion numpy scipy scikit-learn networkx sparse_dot_mkl matplotlib

RUN cd / && git clone https://github.com/zengxiaofei/HapHiC.git && \
    ln -s /HapHiC/haphic /usr/local/bin/haphic && \
    haphic check

ENV TAFFISH_ENV=TAFFISH
ENV TAFFISH_NAME=haphic
