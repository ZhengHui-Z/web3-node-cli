# The GPU options are NVIDIA CUDA developer images

ARG BASE_IMAGE="nvidia/cuda:11.8.0-cudnn8-devel-ubuntu20.04"

FROM ${BASE_IMAGE}


# FROM directive resets ARG
ARG DEBIAN_FRONTEND=noninteractive

ENV TZ=Asia/Shanghai


ARG HOSTTYPE=${HOSTTYPE:-x86_64}


USER $USER_UID
ENV HOME=/root


RUN apt-get update -y && apt-get upgrade -y \
    && apt-get install -y \
    tzdata \
    vim \
    git \
    wget \
    curl \
    screen \
    openssh-server \
    build-essential \
    ca-certificates \
    make \
    pkg-config \
    libssl-dev \
    locales \
    && locale-gen en_US.UTF-8 \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

ENV LANG=en_US.UTF-8

# 安装Python
ARG PYTHON_VERSION=py310_23.10.0-1
RUN wget \
    --quiet "https://repo.anaconda.com/miniconda/Miniconda3-${PYTHON_VERSION}-Linux-${HOSTTYPE}.sh" \
    -O /tmp/miniconda.sh \
    # -b           run install in batch mode (without manual intervention),
    # it is expected the license terms (if any) are agreed upon
    # -f           no error if install prefix already exists
    # -h           print this help message and exit
    # -p PREFIX    install prefix, defaults to /home/user/miniconda3, must not contain spaces.
    # -s           skip running pre/post-link/install scripts
    # -u           update an existing installation
    # -t           run package tests after installation (may install conda-build)
    && /bin/bash /tmp/miniconda.sh -b -u -p $HOME/anaconda3 \
    && $HOME/anaconda3/bin/conda init \
    && echo 'export PATH=$HOME/anaconda3/bin:$PATH' >> /root/.bashrc \
    && rm /tmp/miniconda.sh \
    && $HOME/anaconda3/bin/conda clean -y --all

ENV PATH "/root/anaconda3/bin:$PATH"

# 安装Nodejs
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | -E bash - && \
    apt-get install -y nodejs


# 安装Go
RUN rm -rf /usr/local/go && \
    curl -L https://go.dev/dl/go1.22.0.linux-amd64.tar.gz | tar -xzf - -C /usr/local && \
    echo 'export PATH=$PATH:/usr/local/go/bin' >> /root/.bashrc

# 安装rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

# ENV PATH=$PATH:/usr/local/go/bin:/home/user/anaconda3/bin

WORKDIR /app
