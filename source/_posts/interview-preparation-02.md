---
title: 机器学习秋招面试准备-02
tags:
  - 面试
categories: 面试
date: 2018-08-07 23:41:54
updated: 2018-09-04 05:11:31
description:
keyword:
---


以秋招之名，督回顾之实，切不可舍本逐末。

在回顾的过程中不断总结，不断思考和提升。

因为以面试为主，所以多数但求快速全面，难免多求助了一些“嚼过的馒头”，只有涉及到具体细节，才会回到论文，仔细琢磨，不过总归也算有多得。



![](https://ws2.sinaimg.cn/large/006tNbRwly1fuulgxf70xj314w0v6q9j.jpg)

<!-- more -->

初中的时候，老师总喜欢距离说，知识是要串起来的，学习的时候要学习“一提提起来一串知识”，现在再回头想，非常有道理。独立的看某个知识点是远远不够的，必须要有知识体系，例如看到树模型，自然而然的想到同系列的一串模型、优缺点、损失函数、推导等，这样应该能帮助自己理解的更好。

自己在复习准备的时候，经常是看到A发现不甚了解，于是Google A，之后在A的解释中发现B不懂，继续Google B，循环往复，有如递归，或者二叉树之类。回退的时候，成本也很大。自己还是要控制树的深度，不然树过深之后，横向长度就显得不够。




# 深度学习

## 激活函数

- 激活函数总览
![](https://ws3.sinaimg.cn/large/0069RVTdly1fux1vg7sycj31b30n9q8z.jpg)

- Sigmoid
![](https://ws4.sinaimg.cn/large/0069RVTdly1fux1wwwlkfj319x0neagh.jpg)
- tanh(x)
![](https://ws3.sinaimg.cn/large/0069RVTdly1fux1xi0dguj319z0nctbx.jpg)

- ReLu
![](https://ws2.sinaimg.cn/large/0069RVTdly1fux1uv5nsbj319u0h742t.jpg)

- Leaky ReLU
![](https://ws3.sinaimg.cn/large/0069RVTdly1fux1ywx3naj31ab0n3ajg.jpg)

- Maxout  
![](https://ws2.sinaimg.cn/large/0069RVTdly1fux22anaivj31ab0m5tfp.jpg)

## Batch Normalization



- 作用

（1）加速收敛 
（2）控制过拟合，可以少用或不用Dropout和正则 
（3）降低网络对初始化权重不敏感 
（4）允许使用较大的学习率
![](https://ws4.sinaimg.cn/large/0069RVTdly1fux2b16kpgj319y0n515y.jpg)

需要注意的是，BN的mean和std在train和test阶段是不一样的，前者基于每个batch，后者基于整体数据。
- code 

``` python
m = K.mean(X, axis=-1, keepdims=True)#计算均值
std = K.std(X, axis=-1, keepdims=True)#计算标准差
X_normed = (X - m) / (std + self.epsilon)#归一化
out = self.gamma * X_normed + self.beta#重构变换

```

paper：[Batch Normalization: Accelerating Deep Network Training by  Reducing Internal Covariate Shift](https://arxiv.org/pdf/1502.03167.pdf)

## 调参
- Grid Search

![](https://ws3.sinaimg.cn/large/0069RVTdly1fux2sjw2ecj315q0l0dpc.jpg) 

## 池化与反池化、卷积与反卷积

![](https://ws2.sinaimg.cn/large/006tNbRwly1fuulgxf70xj314w0v6q9j.jpg)


## CNN参数、连接和输出计算

- 卷积层
![](https://ws3.sinaimg.cn/large/006tNbRwly1fuv8axu284j30mq0bc40b.jpg)

例子：
![](https://ws3.sinaimg.cn/large/006tNbRwly1fuv8ikswnjj31go0qa7ap.jpg)

- 池化层
![](https://ws4.sinaimg.cn/large/006tNbRwly1fuv8hbg3c9j31180kqk2x.jpg)
例子：
![](https://ws2.sinaimg.cn/large/006tNbRwly1fuv8hzueaaj31hc0qqdjf.jpg)

卷积计算复杂度

![](https://ws3.sinaimg.cn/large/0069RVTdly1fuwwcatjhmj30oc0g2ae8.jpg)

##  1*1 卷积核的作用？

1、降维（ dimension reductionality ）。比如，一张500 * 500且厚度depth为100 的图片在20个filter上做1 * 1 的卷积，那么结果的大小为500*500*20。

2、加入非线性。卷积层之后经过激励层，1*1的卷积在前一层的学习表示上添加了非线性激励（ non-linear activation ），提升网络的表达能力；




## 激活函数概述


神经网络中激活函数的主要作用是提供网络的非线性建模能力，如不特别说明，激活函数一般而言是非线性函数。假设一个示例神经网络中仅包含线性卷积和全连接运算，那么该网络仅能够表达线性映射，即便增加网络的深度也依旧还是线性映射，难以有效建模实际环境中非线性分布的数据。加入（非线性）激活函数之后，深度神经网络才具备了分层的非线性映射学习能力。因此，激活函数是深度神经网络中不可或缺的部分。

图示from cs231n

### Sigmod  

![](https://ws2.sinaimg.cn/large/0069RVTdgy1fu5waoqdofj30x80pqq9a.jpg)

优点：物理意义上最接近神经元，0，1输出可以用作表示概率，或用于输出的归一化（如）。
缺点：

### Tanh
![](https://ws1.sinaimg.cn/large/006tNbRwly1fuv92kjq9tj3079025dfs.jpg)

### Rectified Linear Unit(ReLU) 

![](https://ws3.sinaimg.cn/large/006tNbRwly1fuv92qxkh1j30490113ye.jpg)

- 优点：
- 缺点：
![](https://ws4.sinaimg.cn/large/006tNbRwly1fuum1rdrtkj31760e2n26.jpg)

即梯度可能会失活，梯度永远为0

如果使用 ReLU，要小心设置 learning rate，注意不要让网络出现很多 “dead” 神经元，如果不好解决，可以试试 Leaky ReLU、PReLU 或者 Maxout.



### Softmax

![](https://ws4.sinaimg.cn/large/006tNbRwly1fuv953stcaj305n021t8n.jpg)

一个具体的例子

![](https://ws2.sinaimg.cn/large/006tNbRwly1fuv958fe41j30hv0army9.jpg)

softmax建模使用的分布是多项式分布，而logistic则基于伯努利分布

多个logistic回归通过叠加也同样可以实现多分类的效果，但是 softmax回归进行的多分类，类与类之间是互斥的，即一个输入只能被归为一类；多个logistic回归进行多分类，输出的类别并不是互斥的，即"苹果"这个词语既属于"水果"类也属于"3C"类别。


# 机器学习

##  逻辑回归

- 逻辑回归损失函数推导

![](https://ws3.sinaimg.cn/large/0069RVTdly1fuwthqi5aej30ht0i7go9.jpg)

## 机器学习基础

- 模型评估指标

1.准确率 accuracy 

准确率(accuracy) =  (TP + TN) / (TP + FP + TN + FN)

2.精确率precision 查准率 =  TP/(TP+FP)

3.召回recall 查全率 =  TP/(TP+FN) 

4.F1 score

F1 Score = P*R/2(P+R)

![](https://ws4.sinaimg.cn/large/006tNbRwgy1fu4h9rdexsj30g806gglu.jpg)

![](https://ws3.sinaimg.cn/large/006tNbRwly1fuvloahxbkj31120m8jvg.jpg)


- adaboost为什么不容易过拟合呢？



## 随机森林、GBDT和XGBoost

- GBDT和XGBoost的区别？

1.GBDT以CART回归树为主，后者支持线性分类器，这个时候XGBoost相当于L1和L2正则化的逻辑斯蒂回归（分类）或者线性回归（回归）；

2.传统的GBDT在优化的时候只用到一阶导数信息，XGBoost则对代价函数进行了**二阶泰勒展开**，得到一阶和二阶导数；
3.XGBoost在代价函数中加入了**正则项**，用于控制模型的复杂度。从权衡方差偏差来看，它降低了模型的方差，使学习出来的模型更加简单，放置过拟合，这也是XGBoost优于传统GBDT的一个特性；
4.**shrinkage**（缩减），相当于学习速率（XGBoost中的eta）。XGBoost在进行完一次迭代时，会将叶子节点的权值乘上该系数，主要是为了削弱每棵树的影响，让后面有更大的学习空间。（GBDT也有学习速率）；
5.**列抽样**。XGBoost借鉴了随机森林的做法，支持列抽样，不仅防止过拟合，还能减少计算；
6.**对缺失值的处理**。对于特征的值有缺失的样本，XGBoost还可以自动学习出它的分裂方向；
7.XGBoost工具支持并行。Boosting不是一种串行的结构吗?怎么并行的？注意XGBoost的并行不是tree粒度的并行，XGBoost也是一次迭代完才能进行下一次迭代的（第t次迭代的代价函数里包含了前面t-1次迭代的预测值）。XGBoost的并行是在特征粒度上的。
我们知道，决策树的学习最耗时的一个步骤就是对特征的值进行排序（因为要确定最佳分割点），XGBoost在训练之前，预先对数据进行了排序，然后保存为block结构，后面的迭代中重复地使用这个结构，大大减小计算量。这个block结构也使得并行成为了可能，在进行节点的分裂时，需要计算每个特征的增益，最终选增益最大的那个特征去做分裂，那么各个特征的增益计算就可以开多线程进行。


- XGBoost和lightGBM的对比？

lightGBM包含两个关键点：light即轻量级，GBM 梯度提升机。

LightGBM 是一个梯度 boosting 框架，使用基于学习算法的决策树。它可以说是分布式的，高效的，有以下优势：

1. 更快的训练效率
2. 低内存使用
3. 更高的准确率
4. 支持并行化学习
5. 可处理大规模数据

概括来说，lightGBM主要有以下特点：

1. 基于Histogram的决策树算法

2. 带深度限制的Leaf-wise的叶子生长策略

3. 直方图做差加速

4. 直接支持类别特征(Categorical Feature)

5. Cache命中率优化

6. 基于直方图的稀疏特征优化

7. 多线程优化

前2个特点使我们尤为关注的。

**Histogram算法**

直方图算法的基本思想：先把连续的浮点特征值离散化成k个整数，同时构造一个宽度为k的直方图。遍历数据时，根据离散化后的值作为索引在直方图中累积统计量，当遍历一次数据后，直方图累积了需要的统计量，然后根据直方图的离散值，遍历寻找最优的分割点。

带深度限制的**Leaf-wise的叶子生长策略**

Level-wise过一次数据可以同时分裂同一层的叶子，容易进行多线程优化，也好控制模型复杂度，不容易过拟合。但实际上Level-wise是一种低效算法，因为它不加区分的对待同一层的叶子，带来了很多没必要的开销，因为实际上很多叶子的分裂增益较低，没必要进行搜索和分裂。

Leaf-wise则是一种更为高效的策略：每次从当前所有叶子中，找到分裂增益最大的一个叶子，然后分裂，如此循环。因此同Level-wise相比，在分裂次数相同的情况下，Leaf-wise可以降低更多的误差，得到更好的精度。

Leaf-wise的缺点：可能会长出比较深的决策树，产生过拟合。因此LightGBM在Leaf-wise之上增加了一个最大深度限制，在保证高效率的同时防止过拟合。

xgboost在实现时还做了许多优化：

1. 在寻找最佳分割点时，考虑传统的枚举每个特征的所有可能分割点的贪心法效率太低，xgboost实现了一种近似的算法。大致的思想是根据百分位法列举几个可能成为分割点的候选者，然后从候选者中根据上面求分割点的公式计算找出最佳的分割点。
2. xgboost考虑了训练数据为稀疏值的情况，可以为缺失值或者指定的值指定分支的默认方向，这能大大提升算法的效率，paper提到50倍。
3. 特征列排序后以块的形式存储在内存中，在迭代中可以重复使用；虽然boosting算法迭代必须串行，但是在处理每个特征列时可以做到并行。
4. 按照特征列方式存储能优化寻找最佳的分割点，但是当以行计算梯度数据时会导致内存的不连续访问，严重时会导致cache miss，降低算法效率。paper中提到，可先将数据收集到线程内部的buffer，然后再计算，提高算法的效率。
5. xgboost 还考虑了当数据量比较大，内存不够时怎么有效的使用磁盘，主要是结合多线程、数据压缩、分片的方法，尽可能的提高算法的效率。

- 随机森林和GBDT的区别？

随机森林是一个用随机方式建立的，包含多个决策树的集成分类器。其输出的类别由各个树投票而定（如果是回归树则取平均）。假设样本总数为n，每个样本的特征数为a，则随机森林的生成过程如下：

1.从原始样本中采用有放回抽样的方法选取n个样本；
2.对n个样本选取a个特征中的随机k个，用建立决策树的方法获得最佳分割点；
3.重复m次，获得m个决策树；
4.对输入样例进行预测时，每个子树都产生一个结果，采用多数投票机制输出。

随机森林的**随机性**主要体现在两个方面：

1.数据集的随机选取：从原始的数据集中采取有放回的抽样（bagging），构造子数据集，子数据集的数据量是和原始数据集相同的。不同子数据集的元素可以重复，同一个子数据集中的元素也可以重复。
2.待选特征的随机选取：与数据集的随机选取类似，随机森林中的子树的每一个分裂过程并未用到所有的待选特征，而是从所有的待选特征中随机选取一定的特征，之后再在随机选取的特征中选取最优的特征。
以上两个随机性能够使得随机森林中的决策树都能够彼此不同，提升系统的多样性，从而提升分类性能。


- 样本比例不均衡？

 1.过抽样（over-sampling）和欠抽样（under-sampling）：前者一般指简单复制少数类样本形成多条记录，缺点是容易过拟合，改进方案是：加入随机噪声、干扰数据或通过一定规则产生新的合成样本；随机减少多数类样本，缺点是丢失部分重要信息，学习的到不能代表大盘。
 
因为下采样会丢失信息，如何减少信息的损失呢？第一种方法叫做**EasyEnsemble**，利用模型融合的方法（Ensemble）：多次下采样（放回采样，这样产生的训练集才相互独立）产生多个不同的训练集，进而训练多个不同的分类器，通过组合多个分类器的结果得到最终的结果。第二种方法叫做BalanceCascade，利用**增量训练**的思想（Boosting）：先通过一次下采样产生训练集，训练一个分类器，对于那些分类正确的大众样本不放回，然后对这个更小的大众样本下采样产生训练集，训练第二个分类器，以此类推，最终组合所有分类器的结果得到最终结果。第三种方法是利用**KNN**试图挑选那些最具代表性的大众样本，叫做NearMiss，这类方法计算量很大，感兴趣的可以参考“Learning from Imbalanced Data”这篇综述的3.2.1节。
 
2.通过对正负样本分别加权，基于类别数量的加权处理。
3.数据合成
4.一分类（One Class Learning）、异常检测（Novelty Detection）     
    
## 特征选择的方案


## 优化算法

梯度下降，牛顿法与拟牛顿法
![](https://ws2.sinaimg.cn/large/006tNbRwgy1fu4grkvaxrj313k0q0gp2.jpg)
![](https://ws2.sinaimg.cn/large/006tNbRwgy1fu4gr0wwmgj31d213m7b6.jpg)
拟牛顿法

![](https://ws3.sinaimg.cn/large/006tNbRwgy1fu4gxco0z0j31dm07gq6p.jpg)

优化的常见问题：

- 局部最小
- ill-condition病态（对数据微笑变化的敏感度过高，数据稍有变化，输出改变很大）

![](https://ws3.sinaimg.cn/large/006tNbRwgy1fu4jeyveq4j31e412mnak.jpg)

# NLP

## Word2vec

2013 年，Google 团队发表了 word2vec 工具 。word2vec 工具主要包含两个模型：跳字模型（skip-gram）和连续词袋模型（continuous bag of words，简称 CBOW），以及两种   近似训练法：负采样（negative sampling）和层序 softmax（hierarchical softmax）。值得一提的是，word2vec 的词向量可以较好地表达不同词之间的相似和类比关系。



 - 为什么传统的one-hot不适用？

# 参考


1. [知乎：如何解释召回率与准确率？](https://www.zhihu.com/question/19645541)
2. [机器学习性能评估指标](http://charleshm.github.io/2016/03/Model-Performance/)
3. [http://wepon.me/](http://wepon.me/) 
4. [LightGBM的并行优化](https://blog.csdn.net/ictcxq/article/details/78736442)
5. [常见回归和分类损失函数比较](https://zhuanlan.zhihu.com/p/36431289)
6. [正负样本不均衡的解决办法](http://blog.csdn.net/lujiandong1/article/details/52658675)
7. [特征工程之特征选择](https://www.cnblogs.com/pinard/p/9032759.html)
8. [李沐团队：词嵌入：word2vec](http://zh.gluon.ai/chapter_natural-language-processing/word2vec.html)
9. [梯度下降，牛顿法与拟牛顿法](https://blog.csdn.net/haolexiao/article/details/60780350)
10. [机器学习岗面试总结](https://blog.csdn.net/zhihua_oba/article/details/78333650)
11. [深度学习中的激活函数导引](https://zhuanlan.zhihu.com/p/22142013)
12. [lightGBM原理、改进简述](https://blog.csdn.net/niaolianjiulin/article/details/76584785)
13. [陈天奇：XGBoost 与 Boosted Tree](http://www.52cs.org/?p=429)
14. [规范化BatchNormalization](https://keras-cn.readthedocs.io/en/latest/layers/normalization_layer/)
15. [卷积神经网络中用1*1 卷积有什么作用或者好处呢？](https://www.zhihu.com/question/56024942)
16. [CS231n](http://cs231n.github.io/)
17. [激活函数对比](https://www.jianshu.com/p/22d9720dbf1a)

    








