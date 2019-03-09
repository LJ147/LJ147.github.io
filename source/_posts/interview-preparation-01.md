---
title: 机器学习秋招面试准备-01
tags:
  - 机器学习
  - 数据挖掘
  - 面试
  - 深度学习
categories: 面试
date: 2018-07-19 15:17:38
updated: 2018-09-04 05:11:39
description: 根据前人面经整理
keyword: 
---

![](https://ws1.sinaimg.cn/large/006tKfTcgy1ftvjr55tfej30wm08eac4.jpg)

本篇大部分面试题来自[知乎-熊风回答](https://www.zhihu.com/question/23437871)，部分来自其余面经，少量为自己的面经。

只适合作为面经回顾，不适合日常学习。
<!-- more -->





#  机器学习


## 损失函数

- 线性回归损失函数？LR的损失函数？线性回归损失函数的两种损失函数的比较？最大似然在逻辑回归当中的应用？梯度下降在逻辑回归中的应用？

-  讲一下常用的损失函数以及各自的适用场景。

对于第一项Loss函数，如果是Square loss，那就是最小二乘了；如果是Hinge Loss，那就是著名的SVM了；如果是exp-Loss，那就是牛逼的 Boosting了；如果是log-Loss，那就是Logistic Regression了。

###  回归损失函数

对于二分类问题，![](https://ws2.sinaimg.cn/large/006tNbRwly1fuvpg4l95uj306002gdfq.jpg) ，损失函数常表示为关于 yf(x) 的单调递减形式。

yf(x) 被称为margin，其作用类似于回归问题中的残差 y-f(x) 。

可以看到如果 yf(x) > 0 ，则样本分类正确， yf(x) < 0 则分类错误，而相应的分类决策边界即为 f(x) = 0 。所以最小化损失函数也可以看作是最大化margin的过程，任何合格的分类损失函数都应该对margin<0的样本施以较大的惩罚。

![](https://ws1.sinaimg.cn/large/006tNbRwly1fuvpayhll9j316q0jctaw.jpg)

### 分类损失函数

![](https://ws1.sinaimg.cn/large/006tNbRwly1fuvphqgte0j31800fy77n.jpg)

![](https://ws2.sinaimg.cn/large/006tNbRwly1fuvpi2w0rxj30pk076t91.jpg)

sigmod函数

1.饱和的神经元导致梯度无法更新
2.sigmod的输出不是zero-centered
3.exp()操作计算量偏大

![](https://ws1.sinaimg.cn/large/0069RVTdly1fux1plkd7zj31ax0nf7aq.jpg)

![](https://ws3.sinaimg.cn/large/006tNbRwly1fuvpiais18j31as0ekq5a.jpg)

![](https://ws3.sinaimg.cn/large/006tNbRwly1fuvpiqtyqyj31980oate7.jpg)

![](https://ws4.sinaimg.cn/large/006tNbRwly1fuvpiwsulqj31520j042f.jpg)

- [机器学习-损失函数](http://www.csuldw.com/2016/03/26/2016-03-26-loss-function/)
- [常见回归和分类损失函数比较](https://zhuanlan.zhihu.com/p/36431289)

## 树类模型

过拟合问题？ OOB？

随机森林的特征选择、数据选择都有一定的随机性，所以本身不易过拟合。

更多参见：https://blog.csdn.net/zhufenglonglove/article/details/51785220

- 决策树 决策树如何避免过拟合

先剪枝的方法

有多种不同的方式可以让决策树停止生长，下面介绍几种停止决策树生长的方法：

限制决策树的高度和叶子结点处样本的数目

1.定义一个高度，当决策树达到该高度时就可以停止决策树的生长，这是一种最为简单的方法；

2.达到某个结点的实例具有相同的特征向量，即使这些实例不属于同一类，也可以停止决策树的生长。这种方法对于处理数据中的数据冲突问题非常有效；

3.定义一个阈值，当达到某个结点的实例个数小于该阈值时就可以停止决策树的生长；

4.定义一个阈值，通过计算每次扩张对系统性能的增益，并比较增益值与该阈值的大小来决定是否停止决策树的生长。


1)Reduced-Error Pruning（REP）方法是一种比较简单的后剪枝的方法，在该方法中，可用的数据被分成两个样例集合：一个训练集用来形成学习到的决策树，一个分离的验证集用来评估这个决策树在后续数据上的精度，确切地说是用来评估修剪这个决策树的影响。这个方法的动机是：即使学习器可能会被训练集中的随机错误和巧合规律所误导，但验证集合不大可能表现出同样的随机波动。所以验证集可以用来对过度拟合训练集中的虚假特征提供防护检验。

该剪枝方法考虑将书上的每个节点作为修剪的候选对象，决定是否修剪这个结点有如下步骤组成：

1：删除以此结点为根的子树

2：使其成为叶子结点

3：赋予该结点关联的训练数据的最常见分类

4：当修剪后的树对于验证集合的性能不会比原来的树差时，才真正删除该结点

因为训练集合的过拟合，使得验证集合数据能够对其进行修正，反复进行上面的操作，从底向上的处理结点，删除那些能够最大限度的提高验证集合的精度的结点，直到进一步修剪有害为止(有害是指修剪会减低验证集合的精度)。

REP是最简单的后剪枝方法之一，不过由于使用独立的测试集，原始决策树相比，修改后的决策树可能偏向于过度修剪。这是因为一些不会再测试集中出现的很稀少的训练集实例所对应的分枝在剪枝过如果训练集较小，通常不考虑采用REP算法。

- TF-IDF的原理是？ TF和IDF的计算公式？idf中为什么要取对数？
- GBDT与XGBoost的区别？



# Topic Model


- LDA解释一下？推导公式？ LDA主题个数如何确定？

主题个数：https://blog.csdn.net/yt71656/article/details/50016067

1.用perplexity-topic number曲线
2.用topic_number-logP(w|T)曲线
3.计算topic之间的相似度  其中第三节提出一个定理：当主题结构的平均相似度最小时，对应的模型最优。
4. 利用HDP(层次狄利克雷过程)




- Bagging（bootstrap aggregating）和Boosting的区别

Bagging，Boosting二者之间的区别

Bagging和Boosting的区别：

1）样本选择上：

Bagging：训练集是在原始集中有放回选取的，从原始集中选出的各轮训练集之间是独立的。

Boosting：每一轮的训练集不变，只是训练集中每个样例在分类器中的权重发生变化。而权值是根据上一轮的分类结果进行调整。

2）样例权重：

Bagging：使用均匀取样，每个样例的权重相等

Boosting：根据错误率不断调整样例的权值，错误率越大则权重越大。

3）预测函数：

Bagging：所有预测函数的权重相等。

Boosting：每个弱分类器都有相应的权重，对于分类误差小的分类器会有更大的权重。

4）并行计算：

Bagging：各个预测函数可以并行生成

Boosting：各个预测函数只能顺序生成，因为后一个模型参数需要前一轮模型的结果。

- 逻辑回归和线性回归对比有什么优点？
- 逻辑回归可以处理非线性问题吗？
- 分类问题有哪些评价指标？每种的适用场景。

 https://blog.csdn.net/PacosonSWJTU/article/details/58651726
 
- 讲一下正则化，L1和L2正则化各自的特点和适用场景。

http://www.csuldw.com/2016/03/26/2016-03-26-loss-function/



- 讲一下决策树和随机森林

常见的决策树有ID3、C4.5,CART等，决策树思想，实际上就是寻找最纯净的划分方法，数学上称为纯度。
ID3使用信息增益作为不纯度，C4.5使用信息增益率作为不纯度，CART使用基尼系数作为不纯度。


| 树种类 | 划分属性依据 | 公式 |
| --- | --- | --- |
| ID3 | 信息熵 | ![](https://ws2.sinaimg.cn/large/801b780agy1ftt36spv9wj205f01kmx3.jpg) ![](http://orkqx44nq.bkt.clouddn.com/15330230324346.jpg)
 |
| C4.5 | 增益率 | ![](https://ws2.sinaimg.cn/large/801b780agy1ftt37g1tv4j20ko08aq3k.jpg) |
| CART | 基尼系数 |  ![](https://ws1.sinaimg.cn/large/801b780agy1ftt37v0l0sj20t40j2mz2.jpg)|

建树和剪枝

代价-复杂度剪枝（Cost-Complexity Pruning，简称CCP）等方案。分类与回归树采用的是代价-复杂度剪枝算法

- 讲一下GBDT的细节，写出GBDT的目标函数。 GBDT和Adaboost的区别与联系
- 手推softmax loss公式


- [Softmax 输出及其反向传播推导](http://shuokay.com/2016/07/20/softmax-loss/)
- [softmax 推导](https://blog.csdn.net/qian99/article/details/78046329)


- 讲一下SVM, SVM与LR有什么联系。

第一，本质上是其loss function不同。

LR采用的是log loss，svm则是hinge loss

![](https://ws4.sinaimg.cn/large/006tNbRwgy1fuiwb5571aj31fk0tqtct.jpg)

第二，支持向量机只考虑局部的边界线附近的点，而逻辑回归考虑全局（远离的点对边界线的确定也起作用）。
第三，在解决非线性问题时，支持向量机采用核函数的机制，而LR通常不采用核函数的方法。
第四，​线性SVM依赖数据表达的距离测度，所以需要对数据先做normalization，LR不受其影响。

- 讲一下PCA的步骤。PCA和SVD的区别和联系
- 讲一下ensemble
- 偏差和方差的区别。ensemble的方法中哪些是降低偏差，哪些是降低方差？


- 回归分析

![](https://ws2.sinaimg.cn/large/006tKfTcgy1ftf92nioxnj315m0paju8.jpg)


实际上，机器学习的有监督学习的所有模型大体上可以划分为两大类：一类是判别模型，另一类是生成模型。

![](https://ws1.sinaimg.cn/large/006tNbRwly1fuul8khhomj31fm0xm4aa.jpg)

- **常见的判别模型：**

线性回归、对数回归、线性判别分析、SVM、Boosting、CRF、神经网络等
![](https://ws3.sinaimg.cn/large/006tKfTcgy1ftf9eymzmcj31i60ci77x.jpg)

- **常见的生成模型：**


隐马尔可夫模型、朴素贝叶斯模型、高斯混合模型、主题模型（LDA等）、受限波尔斯曼机等
![](https://ws2.sinaimg.cn/large/006tKfTcgy1ftf9faq5e6j31gu08s40o.jpg)


![](https://ws1.sinaimg.cn/large/006tKfTcgy1ftfa3l3ws6j30p60g2gna.jpg)

#  深度学习


- 手推BP
- 手推RNN和LSTM结构
- LSTM中每个gate的作用是什么，为什么跟RNN比起来，LSTM可以防止梯度消失
- 讲一下pooling的作用， 为什么max pooling要更常用？哪些情况下，average pooling比max pooling更合适？
- 梯度消失和梯度爆炸的原因是什么？ 有哪些解决方法？




-  CNN和RNN的梯度消失是一样的吗？   

深度学习主要思想为统计不变性（最主要的是**权重共享**，大大降低神经网络中的向量维数，一定程度上可以避免过拟合同时也能降低计算量），表现在**空间上**权重共享上体现为CNN（Convolutional Neural Network），**时间上**权重共享体现为RNN（Recurrent Neural Networks）

- 有哪些防止过拟合的方法？

![](https://ws2.sinaimg.cn/large/006tKfTcgy1ftvlqjlmw0j30pk0lo0w3.jpg)

详情参加我之前的文章：  [机器学习面试基础知识 & 扩展-01](https://hellogod.cn/2017-10-09/basic-deep-learning-01/)



- 讲一下激活函数sigmoid，tanh，relu. 各自的优点和适用场景？ 
- relu的负半轴导数都是0，这部分产生的梯度消失怎么办？
- batch size对收敛速度的影响。
- 讲一下batch normalization 
- CNN做卷积运算的复杂度。如果一个CNN网络的输入channel数目和卷积核数目都减半，总的计算量变为原来的多少？
- 讲一下AlexNet的具体结构，每层的作用
- 讲一下你怎么理解dropout，分别从bagging和正则化的角度

- data augmentation 

1.Color Jittering：对颜色的数据增强：图像亮度、饱和度、对比度变化（此处对色彩抖动的理解不知是否得当）；
2.PCA  Jittering：首先按照RGB三个颜色通道计算均值和标准差，再在整个训练集上计算协方差矩阵，进行特征分解，得到特征向量和特征值，用来做PCA Jittering；
3.Random Scale：尺度变换；
4.Random Crop：采用随机图像差值方式，对图像进行裁剪、缩放；包括5.Scale Jittering方法（VGG及ResNet模型使用）或者尺度和长宽比增强变换；
6.Horizontal/Vertical Flip：水平/垂直翻转；
7.Shift：平移变换；
8.Rotation/Reflection：旋转/仿射变换；
9.Noise：高斯噪声、模糊处理；
10.Label shuffle：类别不平衡数据的增广，参见海康威视ILSVRC2016的report；另外，文中提出了一种Supervised Data Augmentation方法，有兴趣的朋友的可以动手实验下。

- 讲一下你了解的优化方法，sgd, momentum, rmsprop, adam的区别和联系
- 如果训练的神经网络不收敛，可能有哪些原因？    

1.数据量过小
2.learning rate过大

- 说一下你理解的卷积核， 1x1的卷积核有什么作用？

1x1卷积的主要作用有以下几点：
1、降维和降维（ dimension reductionality ）。比如，一张500 * 500且厚度depth为100 的图片在20个filter上做1x1的卷积，那么结果的大小为500x500x20。
2、加入非线性。卷积层之后经过激励层，1x1的卷积在前一层的学习表示上添加了非线性激励（ non-linear activation ），提升网络的表达能力；
3.增加模型深度，一定程度上提升模型的表征能力；
4.这样做可以理解为一根筷子插了3本书，相比较于传统全连接层，1x1卷积保留了空间信息。
主要用于降维，减少参数个数，做特征变换，以及增加宽度。


#  科研上的开放性问题

- 选一个计算机视觉、深度学习、机器学习的子领域，讲一下这个领域的发展脉络，重点讲出各种新方法提出时的motivation，以及谈谈这个领域以后会怎么发展。
-  讲一下你最近看的印象比较深的paper
- 讲一下经典的几种网络结构， AlexNet， VGG，GoogleNet， Residual Net等等，它们各自最重要的contribution
-  你看过最近很火的XXX paper吗? 你对这个有什么看法？ 

# 编程

- hashmap的实现、hashtable
- 说一下快排？ 时间复杂度nlogn怎么来的


# 大数据相关

- spark 任务调度 job、stage、task划分
![](https://ws4.sinaimg.cn/large/801b780agy1ftt5mhiievj218a0ikaco.jpg)
    - Worker Node：物理节点，上面执行executor进程
    - Executor：Worker Node为某应用启动的一个进程，执行多个tasks
    - Jobs:action 的触发会生成一个job, Job会提交给DAGScheduler,分解成Stage,
    - Stage:DAGScheduler 根据shuffle将job划分为不同的stage，同一个stage中包含多个task，这些tasks有相同的 shuffle dependencies。
    - Task:被送到executor上的工作单元，task简单的说就是在一个数据partition上的单个数据处理流程。

![](https://ws2.sinaimg.cn/large/801b780agy1ftt5n3bn11j216k0gsdi0.jpg)


#  数学题

- 如果一个女生说她集齐了十二个星座的前男友，她前男友数量的期望是多少？
- 两个人玩游戏。有n堆石头，每堆分别有a1, a2, a3.... an个石头，每次一个游戏者可以从任意一堆石头里拿走至少一个石头，也可以整堆拿走，
但不能从多堆石头里面拿。无法拿石头的游戏者输，请问这个游戏是否有先手必胜或者后手必胜的策略？ 如果有，请说出这个策略，并证明这个策略能保证必胜。
- 一个一维数轴，起始点在原点。每次向左或者向右走一步，概率都是0.5. 请问回到原点的步数期望是多少？
- 一条长度为1的线段，随机剪两刀，求有一根大于0.5的概率。
- 讲一下你理解的矩阵的秩。低秩矩阵有什么特点？ 在图像处理领域，这些特点有什么应用？
- 讲一下你理解的特征值和特征向量。
- 为什么负梯度方向是使函数值下降最快的方向？简单数学推导一下

# 参考

- [第05章：深入浅出ML之Bayes-Based家族](http://www.52caml.com/head_first_ml/ml-chapter5-bayes-based-family/)
- [概率论6大分布](https://blog.csdn.net/cc1949/article/details/78906044)
- [Spark中job、stage、task的划分+源码执行过程分析](https://blog.csdn.net/hjw199089/article/details/77938688)
- [知乎-熊风回答](https://www.zhihu.com/question/23437871)
- [决策树和随机森林](https://www.cnblogs.com/fionacai/p/5894142.html)
- [详解深度学习中的梯度消失、爆炸原因及其解决方法](https://zhuanlan.zhihu.com/p/33006526)
- [【深度学习】深度学习中RNN梯度消失](https://blog.csdn.net/qq_29340857/article/details/70556307)
- [生成模型与判别模型](http://charleshm.github.io/2016/02/Discriminative-vs-Generative/)



