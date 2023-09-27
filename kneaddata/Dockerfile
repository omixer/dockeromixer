FROM ubuntu:22.04

LABEL maintainer="youssef.darzi@omixer.io"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
 && apt-get install -y python3 python3-dev python3-pip apt-transport-https openjdk-17-jre wget zip \
 && rm -rf /var/lib/apt/lists/*

# RUN pip3 install boto3 cloudpickle awscli
# RUN pip3 install anadama2

# install kneaddata and dependencies
RUN pip3 install kneaddata==0.12.0 --no-binary :all:

# install TRF
RUN wget  https://github.com/Benson-Genomics-Lab/TRF/releases/download/v4.09.1/trf409.linux64 \
 && chmod 755 trf409.linux64 \
 && mv trf409.linux64 /usr/local/bin/trf

# install fastqc
RUN wget https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.12.0.zip \
 && unzip fastqc_v0.12.0.zip \
 && chmod 755 FastQC/fastqc \
 && mv FastQC /usr/local/bin/ \
 && ln -s /usr/local/bin/FastQC/fastqc /usr/local/bin/fastqc \
 && rm fastqc_v0.12.0.zip

WORKDIR /tmp