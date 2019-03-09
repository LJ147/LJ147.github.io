---
title: 机器学习秋招面试准备-02
tags:
  - 日常
  - 面试
  - 机器学习
categories: 面试
date: 2018-09-07 02:36:32
updated: 2018-09-07 02:36:32
description:
keyword:
---

查漏补缺


<!-- more -->


## 归一化


- 为什么要做归一化？

1.提高梯度下降求最优解的速度，未归一化的之后梯度下降可能走“之”字，很难收敛；
2.逻辑回归等模型先验假设数据服从正态分布；
3.  

- 归一化通常是哪些操作？

![](https://ws3.sinaimg.cn/large/0069RVTdly1fv0e82tdglj30yk08amyb.jpg)

- 归一化为什么能提高梯度下降法求解最优解的速度？

未归一化：
![](https://ws4.sinaimg.cn/large/0069RVTdly1fv0e6kxvilj30ek08ljrr.jpg)
归一化：

![](https://ws1.sinaimg.cn/large/0069RVTdly1fv0e6oq0tzj30ga081jrs.jpg)


- https://www.zhihu.com/question/20455227

# 参考



