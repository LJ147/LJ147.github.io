---
title: Python开发笔记-01
tags:
  - python
  - 
categories: 开发笔记
date: 2018-06-13 13:09:10
updated: 2018-06-13 13:09:10
description: 记录踩过的坑，尽管很多都很弱智
keyword:
---

py少年欢乐多


<!-- more -->

# 包名不能随便起

譬如我新建了一个包 `elasticsearch`，之后想引入一个新的包：

```
from elasticsearch import Elasticsearch
```

这个在`PyCharm`里面是不被允许的，需要更换包名，很弱智的问题，这里记录下来。

