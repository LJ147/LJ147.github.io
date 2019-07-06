---
title: cs224n-2019-lecture03-neuralnets
tags:
  - cs224n
  - nlp
date: 2019-07-02 14:24:51
updated: 2019-07-02 14:24:51
categories: cs224n
description: Word Window Classification, Word Vectors Neural Networks, and Matrix Calculus
---

![image-20190702143731790](http://ww2.sinaimg.cn/large/006tNc79ly1g4lhjc2x99j310h0qmjwk.jpg)

之前刷完一遍的 NLP 课程，视频课程的一个弊端就是没有沉淀，难以回顾，加上看得速度较快，第一遍很多地方都是抱着“不求甚解”的态度，重新看还是觉得写一些简单的笔记，加强理解，帮助形成整体的知识体系，图片基本引自课程课件。

这一章首先简单介绍了分类、神经网络的基础部分，接着介绍自然语言处理中的核心问题之一命名实体识别  （Named Entity Recognition, NER），最后介绍了矩阵积分。

![image-20190702143138248](http://ww3.sinaimg.cn/large/006tNc79ly1g4lhd7779oj30yg0ha0w0.jpg)

<!-- more -->

# 1.分类基础

这一部分，是对于基础机器学习知识的回顾。首先介绍一些常用概念和符号，一开始弄清楚这些，对于后续的理解至关重要。例如这里的输入$x_i$一般指词向量、句子和文档等，输出$y_i$一般是类别、其它的词或词串等。

![image-20190702144056807](http://ww4.sinaimg.cn/large/006tNc79ly1g4lhmv2gntj30z90ouq6s.jpg)

传统的分类或统计过程通常就是假设$x_i$固定，训练一个 softmax 或逻辑回归模型来确定决定边界，最后做出预测。

![image-20190702145006767](http://ww3.sinaimg.cn/large/006tNc79ly1g4lhwel4w0j30z70piteq.jpg)



介绍交叉熵损失函数$H(p,q)$ 

![image-20190702145300536](http://ww2.sinaimg.cn/large/006tNc79ly1g4lhzfardkj30zx0p4gqh.jpg)

# 2.神经网络

传统的逻辑回归、softmax 等算法，表达性不够，很多时候只有线性边界，所以出现了表现能力更强的神经网络。神经网络其实 = 多个逻辑回归的叠加

# 3.命名实体识别

命名实体识别的任务是找到文本中的实体并进行分类。

命名实体识别的难点在于难以界定实体的界限，例如 First National Bank，其含义究竟是第一个国家银行，还是第一国家银行呢？



# 4.矩阵积分

# 5.参考

- https://web.stanford.edu/class/cs224n/
- 