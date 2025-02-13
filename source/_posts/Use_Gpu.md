---
title: 利用GPU加速计算
date: 2025/2/5
categories:
  - 学习笔记
---
以Ubuntu系统为例，介绍如何利用GPU加速计算，以进行深度学习、本地运行大模型等高性能任务。
<!-- more -->

我的本地配置参考如下：
- Ubuntu 22.04
- NVIDIA GEFORCE RTX 4060 Laptop

使用的依赖版本如下：
- nvidia-driver-550
- CUDA VERSION：12.4
- PyTorch Build: Stable(2.6.0)

# 说明

要使用英伟达显卡的GPU，首先要确保安装**英伟达驱动**，该驱动能够让操作系统识别并使用英伟达显卡，例如用于图形渲染等功能。然后，需要安装**CUDA工具包**。CUDA允许PyTorch直接与显卡的GPU交互，并让你能够在GPU上执行并行计算任务。没有CUDA，PyTorch就无法利用GPU进行加速。至于**Pytorch**，可理解为是一个流行的深度学习框架，广泛用于训练和推理神经网络。它支持在CPU和GPU上运行。为了利用GPU加速计算，PyTorch需要CUDA来进行GPU上的计算。

但在安装这三者依赖的时候，我们要注意对应版本的支持关系，可在各自官网上查看。以我使用的依赖版本为例，我是4060系列笔记本类的英伟达显卡。它支持550的英伟达驱动，该驱动支持12.4的CUDA工作包版本，而恰好在Linux系统下，PyTorch有支持此CUDA工作包12.4版本的稳定框架。三种对应版本如果支持不上，不但使用不了GPU，而且本地环境会比较混乱，所以找到一套对应关系**十分重要**。

## 安装NVIDIA驱动

可以从[NVIDIA驱动](https://www.nvidia.cn/geforce/drivers/)官网手动下载，限定自己NVIDIA显卡的型号，可以查询到对应显卡支持的NVIDIA驱动。

这里介绍一种更方便的图形化的安装方式，打开Ubuntu系统的Software & Updates，其中的Additonal Drivers选项就是英伟达的显卡驱动。一般可以直接选择带有“tested”选项的驱动，然后安装重启系统即可。

<img src="/images/Ubuntu/Additional_Drivers.png" alt="Addtional Drivers" width="1000">

## 安装CUDA ToolKit

首先确保自己安装了英伟达驱动，可在终端输入以下命令：
```bash
nvidia-smi
```
如果安装成功，你可以看到自己显卡驱动的版本，并且能够看到支持的CUDA的最大版本以及显卡的具体配置等。

<img src="/images/Ubuntu/nvidia-smi.png" alt="nvidia-smi" width="1000">

然后进入[CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit)官网，按照自己需要安装的版本号，选择对应的操作系统及相关内容就能下载了。

<img src="/images/Ubuntu/CUDA_Toolkit.png" alt="CUDA_Toolkit" width="1000">

这里需要注意的是最后在终端执行下载时，会选择需要安装的内容，这里就不再赘述了。

## 安装PyTorch

进入[PyTorch下载](https://pytorch.org/get-started/locally/)官网，也是选择相应的前提条件后就能够进行下载了。

<img src="/images/Ubuntu/PyTorch.png" alt="PyTorch" width="1000">

# 检验安装

三者依赖安装完后，可以在终端输入一下命令进行测试是否安装成功:
```bash
python3 -c "import torch; print(torch.__version__); print(torch.cuda.is_available())"
```
如果安装成功，可以看到终端输出PyTorch和CUDA Toolkit的版本，并且返回“True”

<img src="/images/Ubuntu/test.png" alt="test" width="1000">