FROM ubuntu:yakkety

ENV IOTIVITY_VERSION 1.2-rel

WORKDIR /root

# params that can be overridden at build time

ARG SECURED
ENV SECURED ${SECURED:-1}

ARG RELEASE
ENV RELEASE ${RELEASE:-true}

ARG LOGGING
ENV LOGGING ${LOGGING:-true}

ARG PREFIX
ENV PREFIX ${PREFIX:-/usr}

# Based on instructions on iotivity/Readme.scons.txt

# Install build tools
RUN apt-get -y update && apt-get install -y \
      git-core \
      scons \
      ssh \
      build-essential \
      g++ \
      doxygen \
      valgrind \
# Install external libraries
      libboost-dev \
      libboost-program-options-dev \
      libboost-thread-dev \
      uuid-dev \
      libssl-dev \
      libtool \
      libglib2.0-dev \
# Install other required packaes
      apt-utils \
      libcurl4-openssl-dev \
      unzip \
      curl \
# Cleanup
    && rm -rf /var/lib/apt/lists/*

# Download and build iotivity C/C++ libs and examples
RUN [ "x${RELEASE}" = "xtrue" ] && branch='release' || branch='debug' && \
    git clone https://gerrit.iotivity.org/gerrit/p/iotivity.git --branch ${IOTIVITY_VERSION} && \
    cd iotivity && \
      git clone https://github.com/01org/tinycbor.git extlibs/tinycbor/tinycbor && \
      git clone https://github.com/ARMmbed/mbedtls.git extlibs/mbedtls/mbedtls && \
      scons SECURED=${SECURED} RELEASE=${RELEASE} LOGGING=${LOGGING} --prefix=${PREFIX} && \
      scons SECURED=${SECURED} RELEASE=${RELEASE} LOGGING=${LOGGING} install --prefix=${PREFIX} && \
      cd ..
