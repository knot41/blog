---
title: 安装Docker Desktop
date: 2025/2/7
categories:
  - 学习笔记
---
最近看到很多开源项目会在 GitHub 上提供 Docker 支持，在试着使用的过程，我感受到docker工具的魅力。所以记录下Docker Desktop的安装并给出一些可用的配置。
<!-- more -->

# 说明

Docker Desktop 是一个开发者工具，主要用于在本地机器上运行和管理 Docker 容器。其内部包含了 Docker Engine 和 Docker CLI，还提供了 Kubernetes 集群支持，方便开发人员在本地进行容器编排与管理。简而言之，它让开发人员可以在本地环境中便捷地运行 Docker 容器，进行应用开发和测试。

# 下载

我本地的操作系统是Ubuntu系统，如果是其他系统，可前往[Docker Desktop官网](https://docs.docker.com/desktop/)自行安装。

*TIP*: Docker Desktop已经自带了Docker Engine，如果本地有Docker Engine，一定要注意两者不能冲突！！！

## 设置docker的软件包存储库

在终端输入以下命令：
```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

## 下载最新的DEB软件包

可前往[Docker Desktop发行说明](https://docs.docker.com/desktop/release-notes/)进行下载。

## 使用apt安装软件包

在终端输入以下命令：
```bash
sudo apt-get update
sudo apt-get install ./docker-desktop-amd64.deb
```

# 检验安装

在执行完下载步骤后，可在终端得到和我类似的内容。

<img src="/images/Ubuntu/Docker_Desktop.png" alt="Docker Desktop" width="1000">

# 设置代理和镜像源

安装好后，往往会遇到网络无法访问的问题。于是就需要设置docker的代理和镜像源了。

- 代理确保 Docker 能通过公司网络或墙外网络。
- 镜像源确保 Docker 镜像能够快速拉取，避免 Docker Hub 访问缓慢。

## 代理设置

<img src="/images/Ubuntu/docker_proxy.png" alt="docker_proxy" width="1000">

端口号要设置为自己代理客户端运行的端口号。

## 镜像源设置

这些镜像源目前是可用的，后续或许也会寄。

<img src="/images/Ubuntu/docker_mirros.png" alt="docker_mirros" width="1000">

设置好后，如果可以 sign in 或者可以 pull hello-world 镜像那就说明没有问题啦。