---
title: 基于强化学习的推荐系统概述
tags:
  - 综述
  - 强化学习
  - 推荐系统
categories: 推荐系统
date: 2019-01-10 17:13:38
updated: 2019-01-10 17:13:38
description: 增强学习在推荐系统上的应用
keyword: 
  - 强化学习
  - 推荐系统
---

![](https://ws1.sinaimg.cn/large/006tNc79ly1fz1mmtg4iij30xc0fkju1.jpg)

<!-- more -->

# 1.介绍

待完善



# 2.论文

## 2.1 公司成果

- [美团：强化学习在美团“猜你喜欢”的实践 [2018] ](https://tech.meituan.com/reinforcement_learning_in_mt_recommend_system.html)
- [阿里：强化学习在淘宝锦囊推荐系统中的应用 [2018]](https://link.zhihu.com/?target=http%3A//techforum-img.cn-hangzhou.oss-pub.aliyun-inc.com/1517812754285/reinforcement_learning.pdf)
- [阿里：Reinforcement Learning to Rank in E-Commerce Search Engine: Formalization, Analysis, and Application.[2018]](https://arxiv.org/abs/1803.00710) 
- [微软：DRN: A Deep Reinforcement Learning Framework for News Recommendation. [2018]](http://www.personal.psu.edu/~gjz5038/paper/www2018_reinforceRec/www2018_reinforceRec.pdf)
- [京东：Deep Reinforcement Learning for List-wise Recommendations. [2017]](https://arxiv.org/abs/1801.00209)
- [京东：Optimizing Gross Merchandise Volume via DNN-MAB Dynamic Ranking Paradigm.[2017]](https://arxiv.org/abs/1708.03993)
- [京东：Recommendations with Negative Feedback via Pairwise Deep Reinforcement Learning.[2018] ](https://arxiv.org/abs/1802.06501)
- [京东：Deep Reinforcement Learning for Page-wise Recommendations. [2018]](https://arxiv.org/abs/1805.02343)



## 2.2 其它论文

- [2018 - Recommendations with Negative Feedback via Pairwise Deep Reinforcement Learning](https://arxiv.org/abs/1802.06501)
- [2018 - Recent Advances in Recommender Systems: Matrices, Bandits, and Blenders](https://openproceedings.org/2018/conf/edbt/georgiakoutrika.pdf)
- [2015 - Collaborative Filtering Bandits](https://arxiv.org/abs/1502.03473)
- [2014 - Bandits Warm-up Cold Recommender Systems](https://arxiv.org/abs/1407.2806)
- [2010 - A Contextual-Bandit Approach to Personalized News Article Recommendation](https://arxiv.org/abs/1003.0146)



# 3.应用场景

一般用于连续翻页的多轮交互场景

# 4.优缺点

## 4.1 优点

- exploit与explore问题，对已知信息合理利用的基础上进行适当探索，提升用户体验
- cold start 问题

## 4.2 缺点

强化学习训练不稳定、难以收敛、学习效率低、要求海量训练数据