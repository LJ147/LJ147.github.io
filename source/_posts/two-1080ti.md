---
title: 为什么深度学习需要使用GPU？
tags:
  - 深度学习
  - 显卡
categories: 深度学习
date: 2017-12-17 15:38:50
updated: 2018-12-27 13:15:42
description: 为什么在部分机器学习中训练模型时使用GPU的效果比CPU更好？
keyword:
---

总算是有了一个初级炼丹炉吧，虽然是实验室的233

 ![](https://ws4.sinaimg.cn/large/006tKfTcly1fs3v0m75k5j31kw0nnjzi.jpg)

希望自己能够善用炼丹炉，早日成为一名合格的炼丹师！

后面针对GPU来整理一下相关的资料。

来填之前挖的坑了。
 
# 如何选购GPU
 
![](https://ws4.sinaimg.cn/large/006tNbRwgy1fyl8b7t9glj31560ouady.jpg)

其实关于GPU，之前李沐有很好的科普帖： [GPU 购买指南](https://zh.diveintodeeplearning.org/chapter_appendix/buy-gpu.html)

这里摘录一部分：[1]

GPU 的性能主要由以下三个参数构成：

计算能力。通常我们关心的是 32 位浮点计算能力。16 位浮点训练也开始流行，如果只做预测的话也可以用 8 位整数。

- 内存大小。当模型越大，或者训练时的批量越大时，所需要的 GPU 内存就越多。
- 内存带宽。只有当内存带宽足够时才能充分发挥计算能力。
- 对于大部分用户来说，只要考虑计算能力就可以了。GPU 内存尽量不小于 4GB。但如果 GPU 要同时显示图形界面，那么推荐的内存大小至少为 6GB。内存带宽通常相对固定，选择空间较小。

李沐： “1050ti，1080ti和titan xp性价比都不错”

# 为什么深度学习要用GPU  


1.多核并行：GPU最早是用于图形渲染、计算，多核并行提高渲染速度，NVIDIA有一个非常形象生动的视频：

<embed src='http://player.youku.com/player.php/sid/XNjY3MTY4NjAw/v.swf' allowFullScreen='true' quality='high' width='600' height='400' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash'></embed>



2.计算类型简单统一：CPU和GPU之所以大不相同，是由于其设计目标的不同，它们分别针对了两种不同的应用场景。CPU需要很强的通用性来处理各种不同的数据类型，同时又要逻辑判断又会引入大量的分支跳转和中断的处理。这些都使得CPU的内部结构异常复杂。而GPU面对的则是类型高度统一的、相互无依赖的大规模数据和不需要被打断的纯净的计算环境。[4] 

可参考下图的设计理念：[5]

![](https://ws3.sinaimg.cn/large/006tNbRwgy1fyl8lflh0bj30k008e0tx.jpg)

![](https://ws3.sinaimg.cn/large/006tNbRwgy1fyl8ltzdrpj30k008aabg.jpg)

部分机器学习算法，比如遗传算法，神经网络等，也具有这种分布式及局部独立的特性（e.g.比如说一条神经网络中的链路跟另一条链路之间是同时进行计算，而且相互之间没有依赖的），这种情况下可以采用大量小核心同时运算的方式来加快运算速度。[6]




<!-- more -->


# 参考

- [1] [动手学深度学习](https://zh.diveintodeeplearning.org)
- [2] [为什么GPU运算速度比CPU的运算速度快](https://www.zhihu.com/question/19717029)
- [3] [CPU和GPU的区别是什么](https://www.zhihu.com/question/19903344)
- [4] [1.2CPU和GPU的设计区别](http://www.cnblogs.com/biglucky/p/4223565.html)
- [5] [NVIDIA: 什么是 GPU 加速计算？](https://www.nvidia.cn/object/what-is-gpu-computing-cn.html)
- [6] [为什么在部分机器学习中训练模型时使用GPU的效果比CPU更好？](https://www.zhihu.com/question/35063258)

