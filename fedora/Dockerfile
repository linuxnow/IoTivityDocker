FROM fedora:latest

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
RUN dnf -y update && dnf install -y \
      git \
      scons \
      openssh \
      make \
      gcc \
      gcc-c++ \
# Install external libraries
      boost-devel \
      libuuid-devel \
      glib2-devel \
# Install other required packaes
      unzip \
      tar \
      bzip2 \
      curl \
# Cleanup
    && dnf clean all

# Download and build iotivity C/C++ libs and examples
RUN [ "x${RELEASE}" = "xtrue" ] && branch='release' || branch='debug' && \
    git clone https://gerrit.iotivity.org/gerrit/p/iotivity.git --branch ${IOTIVITY_VERSION} && \
    cd iotivity && \
      git clone https://github.com/01org/tinycbor.git extlibs/tinycbor/tinycbor && \
      git clone https://github.com/ARMmbed/mbedtls.git extlibs/mbedtls/mbedtls && \
      scons SECURED=${SECURED} RELEASE=${RELEASE} LOGGING=${LOGGING} --prefix=${PREFIX} && \
      scons SECURED=${SECURED} RELEASE=${RELEASE} LOGGING=${LOGGING} install --prefix=${PREFIX} && \
      cd ..
