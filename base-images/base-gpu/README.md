# web3节点Cuda基础镜像（支持GPU）

## 已安装基础库

```shell
apt-get install -y \
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
locales 
```

## 安装语言环境

### Nodejs

```shell
curl -fsSL <https://deb.nodesource.com/setup_16.x> | sudo -E bash -
```

### Go

```shell
curl -L <https://go.dev/dl/go1.22.0.linux-amd64.tar.gz> | sudo tar -xzf - -C /usr/local && \
```

### Rust

```shell
curl --proto '=https' --tlsv1.2 -sSf <https://sh.rustup.rs> | sh
```
