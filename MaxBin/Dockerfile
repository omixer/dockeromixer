FROM ubuntu:18.04

LABEL description="MaxBin, a binning software for metagenomic datasets"
LABEL maintainer="youssef.darzi@gmail.com"

ENV version 2.2.5
# Disable deb interactivity (will assume that timezone is CET )
ENV DEBIAN_FRONTEND noninteractive
# Install build essentials and other tools required for compiling MaxBin and dependencies
RUN apt-get update \
 && apt-get install -y --no-install-recommends build-essential wget autoconf unzip ca-certificates \
 && rm -rf /var/lib/apt/lists/*
# Download 
RUN wget --no-check-certificate https://sourceforge.net/projects/maxbin/files/MaxBin-${version}.tar.gz/download \
 && tar -xzvf download \
 && rm download

ENV PATH $PATH:.
# Build MaxBin and dependencies  
RUN cd MaxBin-${version}/src \
 && make \
 && cd .. \
 && ./autobuild_auxiliary \
 && cd auxiliary/hmmer-3.1b1/ \
 && make install \
 && cd .. \
 && mv bowtie2-*/bowtie2* /usr/local/bin/ \
 && mv idba-*/bin/ /opt/idba \
 && mv FragGeneScan1.30 /opt/FragGeneScan \
 && rm -rf /opt/FragGeneScan/example \
 && rm -rf auxiliary

# Configure PATH
ENV PATH $PATH:/opt/FragGeneScan/:/opt/idba/

## Remove the settings files that contains hardcoded path to aux tools
RUN rm /MaxBin-${version}/setting

WORKDIR /MaxBin-${version}/

ENTRYPOINT ["run_MaxBin.pl"]