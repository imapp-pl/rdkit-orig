# this file was created by modifying ethereum/cpp-build-env Dockerfile to use
# a stable Debian as a base and removing tools imapp builds do not need

FROM debian:10.3-slim

LABEL maintainer="imapp"
LABEL version="1.2"
LABEL description="Build environment for RDKIT"

# Install packages
RUN export DEBIAN_FRONTEND=noninteractive \
  && apt-get -qq update \
  && apt-get install -yq --no-install-recommends \
    curl \
    dirmngr \
    gnupg2 \
    sudo \
    # Build tools
    git \
    cmake \
    make \
    ninja-build \
    python3.7 \
    python3-pip \
    python3-requests \
    python3-git \
    ccache \
    doxygen \
    # Compilers
    g++ \
    llvm-6.0-dev \
    libncurses-dev \
    libz-dev \
    # Dependencies
    libleveldb-dev \
    libpython3-all-dev \
    libboost-all-dev \
    zlib1g-dev \
  && rm -rf /var/lib/apt/lists/*

# Set up python 3.7 as default, 2.7 as an alternative
RUN update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1 && \
  update-alternatives --install /usr/bin/python python /usr/bin/python3.7 2

# Install dependencies
RUN python -m pip install \
  setuptools==46.1.3 \
  codecov==2.0.22 \
  codespell==1.16.0 \
  numpy==1.18.3 \
  pandas==0.25.3 \
  pillow==7.1.1

# Add builder user
RUN adduser --disabled-password --gecos '' builder && adduser builder sudo && \
  printf 'builder\tALL=NOPASSWD: ALL\n' >> /etc/sudoers

USER builder
WORKDIR /home/builder
