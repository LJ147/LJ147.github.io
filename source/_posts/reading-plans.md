---
title: 近期学习计划 & 整理
tags:
  - 日常
categories: 学习计划
date: 2018-04-08 22:45:31
updated: 2018-04-23 22:19:23
description: 近两周的学习计划
keyword: 阅读
---


前一个月颇有些晕头转向的意思，虽说只是流鼻血并没有物理头晕，但精神上实际已经晕了，一时忘记要时刻学习。

于是制定一个简单的计划，附加一些技术名词的简单解释，不断更新。

<!-- more -->



> 本来确定的标题是读书计划，没想到写成了学习计划。


每当开始确立计划的时候，不免要担心是否能够顺利执行。

这种也只能让时间去检验。

我斗胆先把这些书单定在两周之内完成，两周后我来更新，看看完成了多少（这一点确实要向nica学习）。

机器学习这块，目前的首要任务是，形成系统的理解，不能单靠只言片语或者一些碎片知识，就像之前提到的，碎片知识依附于完整的知识体系。


暂定回顾书单：

- [x]《Hive编程指南》 
- [x]《dlbook_cn_v0.5-beta》
- [x]《机器学习》
- [ ]《Hadoop权威指南》 第三版  
- [x]《Spark快速大数据分析》


   `dlbook_cn`读起来很是激动啊，有种武侠小说里读武林秘籍的感觉，畅快淋漓，可惜不适应英文阅读，不然想来直接读原版肯定更佳。

讲道理Hadoop这本书是真的不好读，很难啃的一本书，Spark这本书则更像“快餐”。

新书单：

- [ ]《统计机器学习》
- [ ]《Spark The Definitive Guide》
- [ ]《Scala编程》  泛读



需要了解的相关技术和名词：

##   RPC、Protobuf、thrift
 
- 首先了解什么叫RPC，为什么要RPC，RPC是指远程过程调用，也就是说两台服务器A，B，一个应用部署在A服务器上，想要调用B服务器上应用提供的函数/方法，由于不在一个内存空间，不能直接调用，需要通过网络来表达调用的语义和传达调用的数据。来自 [知乎](https://www.zhihu.com/question/25536695)
 
-  Thrift是一种接口描述语言和二进制通讯协议，它被用来定义和创建跨语言的服务。

##    ETL 
 
 数据仓库技术，英文Extract-Transform-Load 的缩写，用来描述将数据从来源端经过抽取(extract)、转换(transform)、加载(load)至目的端的过程
##    maven
##    Hadoop YARN 
##    Cephfs
##    Spark、Zeppelin源码

- [http://scikit-learn.org/](http://scikit-learn.org/)


需要熟练掌握（熟悉API）：

##   numpy

 很好的学习链接：[101 NumPy Exercises for Data Analysis (Python)](https://www.machinelearningplus.com/python/101-numpy-exercises-python/)

##   pandas
##   matplotlib  
##   sql优化  
Hive任务如何更快的运行、如何抢占资源（是的，就这么直接）

这个部分其实之前一直有些误解，以为会用就够，其实更多的时候这些工具需要的是熟练度，快速对数据进行处理。

