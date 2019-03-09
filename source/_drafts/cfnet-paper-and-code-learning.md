---
title: cfnet视频目标跟踪论文和代码笔记
tags:
  - tracking
categories: 深度学习
date: 2018-10-10 19:20:01
updated: 2018-10-10 19:20:01
description: End-to-end representation learning for Correlation Filter based tracking
keyword: tracking
---


近期秋招告一段落，休息了一段时间之后，开始准备一些科研相关的事情。

初步选定的方向为Object Tracking，之前接触过一些detection的内容，有些东西还是互通，理解起来没有那么困难。经S学姐推荐，阅读了一些论文，这里重点记录cfnet的论文、代码笔记。

<!-- more -->

其实很惭愧，自己虽说是从事算法方向，但是科研经历较少（大一二过于懵懂，大三开始忙于实习），所以拖到大四才开始静下心来做一些学术相关的事情。

第一个问题自然是论文，刚开始啃论文，很是头疼，不知从哪里下手，加上自己之前看小说养成的一目十行的坏习惯，到了这里，就很惨。而且之前常常会有只抓大局，不注重细节的问题，这时候都要慢慢修正。

# 论文

主要理解几个核心概念

## 相关滤波

## 快速傅里叶变换（FFT）

# 代码


## 环境

- Ubuntu 16.04.1 LTS
- MATLAB 2016b
- CUDA Version 9.0.176
- cuDNN v7
- MatConvNet 1.0-beta25 



## 步骤

cfnet： https://github.com/bertinetto/cfnet
matconvnet： http://www.vlfeat.org/matconvnet/install/

按照步骤一步步执行即可。

## 踩过的坑

### 一、编译matconvnet

1.下载源码之后，cd 到 MatConvNet目录下，进入matlab命令行，执行：

`mex -setup`

`mex -setup C++`

`注`：mex是Matlab提供的一种混合编程方式。通过mex，用户可以在Matlab中调用C/C++或者Fortran编写的计算程序，加速Matlab内部的矩阵运算（尤其是加速Matlab代码中的for循环）。mex本质上是一个动态链接库文件，可以被Matlab动态加载并执行。



2.编译

```
vl_compilenn('enableGpu', true,  'cudaRoot', '/usr/local/cuda-9.0','cudaMethod', 'nvcc','enableCudnn',true)
```

3.编译完成之后，执行 `vl_testnn('gpu', true)`，最后显示全部通过，证明编译正确无误（该步骤测试过程耗时较长）。

### 二、数据集下载

下载测试训练集（4.3GB）的时候，文件好几次下载失败，上迅雷解决。（ https://bit.ly/cfnet_validation）

### 三、Segmentation violation 


![](https://ws1.sinaimg.cn/large/006tNbRwly1fw3dfthr55j31kw11swly.jpg)

暂未解决

# 参考


- [CFNet视频目标跟踪源码运行笔记（1）——only tracking](https://blog.csdn.net/discoverer100/article/details/79758131)
- [End-to-end representation learning for Correlation Filter based tracking](https://arxiv.org/pdf/1704.06036)


