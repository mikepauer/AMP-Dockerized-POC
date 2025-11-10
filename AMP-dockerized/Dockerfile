FROM ghcr.io/linuxserver/baseimage-ubuntu:noble

ARG VERSION
ARG DEBIAN_FRONTEND="noninteractive"

ENV AMP_AUTO_UPDATE=true
ENV AMP_LICENCE=notset
ENV AMP_MODULE=ADS
ENV AMP_RELEASE_STREAM=Mainline
ENV AMP_SUPPORT_LEVEL=UNSUPPORTED
ENV AMP_SUPPORT_TOKEN=AST0/MTAD
ENV AMP_SUPPORT_TAGS="nosupport docker community unofficial unraid"
ENV AMP_SUPPORT_URL="https://github.com/MitchTalmadge/AMP-dockerized/"
ENV LD_LIBRARY_PATH="./:/opt/cubecoders/amp/:/AMP/"
ENV PORT=8080
ENV USERNAME=admin
ENV PASSWORD=password
ENV IPBINDING=0.0.0.0
        
RUN apt-get update && \
    apt-get install -y \
    bzip2 \
    gdb \
    git \
    git-lfs \
    iputils-ping \
    libc++-dev \
    libatomic1 \
    libgdiplus \
    liblua5.3-0 \
    libpulse-dev \
    numactl \
    software-properties-common \
    socat \
    tmux \
    unzip \
    xz-utils && \
    apt-get -y clean && \
    apt-get -y autoremove --purge && \
    rm -rf /tmp/* /var/lib/apt/lists/* /var/tmp/*

RUN curl -fsSL https://repo.cubecoders.com/archive.key | gpg --dearmor -o /usr/share/keyrings/cubecoders-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/cubecoders-archive-keyring.gpg] https://repo.cubecoders.com/ debian/" > /etc/apt/sources.list.d/cubecoders.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends --download-only ampinstmgr && \
    mkdir -p /tmp/ampinstmgr && \
    dpkg-deb -x /var/cache/apt/archives/ampinstmgr_*.deb /tmp/ampinstmgr && \
    mv /tmp/ampinstmgr/opt/cubecoders/amp/ampinstmgr /usr/local/bin/ampinstmgr && \
    apt-get -y clean && \
    apt-get -y autoremove --purge && \
    rm -rf /tmp/* /var/lib/apt/lists/* /var/tmp/*

COPY root/ /
EXPOSE 8080/tcp

VOLUME /home/amp
