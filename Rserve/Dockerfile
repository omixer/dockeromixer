FROM ubuntu:18.04

LABEL description="Builds R from source and installs Rserve, mixOmics, and phyloseq "
LABEL maintainer="youssef.darzi@gmail.com"

# Define a mirror for R, CRAN and BioC
ENV cran https://cran.ism.ac.jp/
ENV bioc https://bioc.ism.ac.jp/
# Set a target R version
ENV r_version R-3.4.2
# Disable deb interactivity (will assume that timezone is CET )
ENV DEBIAN_FRONTEND noninteractive
# add wget to download R
RUN  apt-get update \
  && apt-get install -y wget \
  && rm -rf /var/lib/apt/lists/*
# Add build tools to compile R from source (required for Rserve) and dependencies for mixOmics
RUN  apt-get update \
  && apt-get install -y --no-install-recommends build-essential gfortran zlib1g-dev libcurl4-gnutls-dev libbz2-dev libpcre3-dev libblas-dev liblzma-dev \
     libmagick++-dev libglu1-mesa-dev libgl1-mesa-dev libssl-dev tk-dev \
  && rm -rf /var/lib/apt/lists/*

RUN wget ${cran}/src/base/R-3/${r_version}.tar.gz
 && tar xzvf ${r_version}.tar.gz
 && rm ${r_version}.tar.gz
  
RUN cd ${r_version} \
 && ./configure --enable-R-shlib --enable-shared --with-readline=no --with-x=no --with-cairo --with-libpng --with-jpeglib \
 && make \
 && make install
 
RUN cd .. && ${r_version}

RUN R -e 'install.packages("mixOmics", repos="'${cran}'",dependencies=TRUE, verbose=T, quiet=T, clean=T)' && rm -rf /tmp/Rtmp*
RUN R -e 'install.packages("Rserve", repos="'${cran}'",dependencies=TRUE, verbose=T, quiet=T, clean=T)' && rm -rf /tmp/Rtmp*
RUN R -e 'install.packages("clusterSim", repos="'${cran}'",dependencies=TRUE, verbose=T, quiet=T, clean=T)' && rm -rf /tmp/Rtmp*

RUN R -e 'options("BioC_mirror" = "'${bioc}'");source("http://bioconductor.org/biocLite.R");biocLite("phyloseq", clean=T)' && rm -rf /tmp/Rtmp*

EXPOSE 6311
ENTRYPOINT R -e "Rserve::run.Rserve(remote=TRUE)"