FROM ubuntu:xenial

ENV IOTIVITY_VERSION 1.1-rel

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

RUN apt-get -y update && apt-get install -y \
      git-core \
      scons \
      ssh \
      build-essential \
      g++ \
      doxygen \
      valgrind \
      libboost-dev \
      libboost-program-options-dev \
      libboost-thread-dev \
      uuid-dev \
      libssl-dev \
      libtool \
      libglib2.0-dev \
      unzip \
      curl && \
    rm -rf /var/lib/apt/lists/*

RUN [ "x${RELEASE}" = "xtrue" ] && branch='release' || branch='debug' && \
    git clone https://gerrit.iotivity.org/gerrit/p/iotivity.git --branch ${IOTIVITY_VERSION} && \
    cd iotivity && \
      git clone https://github.com/01org/tinycbor.git extlibs/tinycbor/tinycbor --branch v0.2.1 && \
      scons SECURED=${SECURED} RELEASE=${RELEASE} LOGGING=${LOGGING} --prefix=${PREFIX} && \
      scons SECURED=${SECURED} RELEASE=${RELEASE} LOGGING=${LOGGING} install --prefix=${PREFIX} && \
      install \
        out/linux/x86_64/${branch}/resource/csdk/stack/samples/linux/SimpleClientServer/occlient \
        out/linux/x86_64/${branch}/resource/csdk/stack/samples/linux/SimpleClientServer/ocserver \
        out/linux/x86_64/${branch}/resource/csdk/stack/samples/linux/secure/ocserverbasicops \
        out/linux/x86_64/${branch}/resource/csdk/stack/samples/linux/secure/occlientbasicops \
        ${PREFIX}/bin/ && \
      cd .. && \
    rm -r iotivity/
