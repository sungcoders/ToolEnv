FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
    build-essential \
    libncurses5-dev \
    git \
    bzr \
    wget \
    unzip \
    bc \
    python3 \
    file \
    cpio \
    rsync \
    && rm -rf /var/lib/apt/lists/*

# add user 'sunglv'
RUN useradd -ms /bin/bash sunglv && echo "sunglv ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
USER sunglv

# workspace docker
WORKDIR /workspace
