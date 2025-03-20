FROM ghcr.io/taffish-org/python:3.12.9

LABEL maintainer="taffish@163.com"

WORKDIR /root

RUN apt-get update && apt-get install -y curl git gcc g++ make

RUN pip install --upgrade pip && pip install pysam portion numpy scipy scikit-learn networkx sparse_dot_mkl matplotlib

RUN git clone https://github.com/zengxiaofei/HapHiC.git && \
    ln -s /root/HapHiC/haphic /usr/local/bin/haphic

ENV TAFFISH_ENV=TAFFISH
ENV TAFFISH_NAME=haphic
