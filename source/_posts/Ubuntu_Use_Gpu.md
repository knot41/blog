---
title: 在Ubuntu系统下，利用GPU加速计算
date: 2025/2/5
# update: 2025/1/2
categories:
  - Ubuntu
  - GPU
---
介绍在Ubuntu系统下，如何利用GPU加速计算，以进行深度学习、本地运行大模型等高性能任务。
<!-- more -->

我的本地配置参考如下：
- Ubuntu 22.04
- NVIDIA GEFORCE RTX 4060 Laptop

使用的依赖版本如下：
- nvidia-driver-550
- CUDA VERSION：12.4
- PyTorch Build: Stable(2.6.0)

# 安装NVIDIA驱动

可以从[NVIDIA]()官网手动下载，限定自己NVIDIA显卡的型号，可以查询到对应显卡支持的NVIDIA驱动。

这里介绍一种更方便的图形化的安装方式，打开Ubuntu系统的Software & Updates，其中的Additonal Drivers选项就是英伟达的显卡驱动。一般可以直接选择带有“tested”选项的驱动，然后安装重启系统即可。

<img src="/images/Ubuntu/Additional_Drivers.png" alt="Addtional Drivers" width="1000">

# 安装CUDA ToolKit