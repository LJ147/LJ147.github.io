---
title: 本周进展：强化学习初探（0）
tags:
  - paper
  - 推荐系统
  - 强化学习
categories: 学习周报
date: 2018-12-26 23:40:01
updated: 2018-12-26 23:40:01
description: 了解强化学习的基础理论
keyword:
---

![](https://ws1.sinaimg.cn/large/006tNbRwly1fyl4pvpxloj30jg07ijrv.jpg)

最近开始跟杜博老师做毕设相关事情，暂定方向为基于深度强化学习的推荐系统。

按照规划，我会每周发布一篇进度报告（这是第0篇），总结本周的进展和问题，方便和高博士交流以及自我总结。

# 本周概要

## 完成

- 阅读李航《统计学习方法》第10章隐马尔科夫模型
- 阅读周志华《机器学习》第16章强化学习
- 斯坦福cs231n Reinforcement Learning 章节
- 阅读高博士指定的两篇论文


## 下周任务

- 制定学习计划，以周为单位
- 阅读高博士指定的中文论文
- 选择性学习OpenAI推出的Spining Up强化学习课程
- 理解强化学习应用于推荐系统的优势、劣势


## 问题

- 数据集是什么？数据形式是什么？ 数据集正在准备，数据形式未知
- 最终预期产出？ Demo + 论文



# 知识总结

- 马尔科夫性质（无后效性）[2]：指系统的下个状态只与当前状态信息有关，而与更早之前的状态无关。

- 马尔可夫决策过程（Markov Decision Process, MDP）[3]

![](https://ws2.sinaimg.cn/large/006tNbRwgy1fyl4weg9etj31am0fm43l.jpg)

- 马尔科夫模型的几类子模型对比

|   | 不考虑动作 | 考虑动作 |
| --- | --- | --- |
| 状态完全可见 | 马尔科夫链(MC) |  马尔可夫决策过程(MDP)
| 状态不完全可见 | 隐马尔可夫模型(HMM)|  不完全可观察马尔可夫决策过程(POMDP)


<!-- more -->







# 如何读论文？

- 选择恰当的文献
- 首先看题目、关键词和摘要，有选择性的阅读内容，有详有略。
- 做好论文笔记  

# 论文简要笔记

- Extracting Action Sequences from Texts Based on Deep Reinforcement Learning
- Toward Diverse Text Generation with Inverse Reinforcement Learning
- 强化学习在淘宝锦囊推荐系统中的应用

# 思考


# 实验部分

# 问题

# 引用

- [1] Zhao X, Zhang L, Ding Z, et al. Deep Reinforcement Learning for List-wise Recommendations[J]. arXiv preprint arXiv:1801.00209, 2017.
- [2] [增强学习（二）----- 马尔可夫决策过程MDP](https://www.cnblogs.com/jinxulin/p/3517377.html)
- [3] [马尔可夫决策过程](http://staff.ustc.edu.cn/~jianmin/lecture/ai/mdp_slides.pdf)



