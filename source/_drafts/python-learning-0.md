---
title: python基础知识-0
date: 2017-09-06 03:22:25
updated: 2019-01-06 10:32:18
description:
tags:
- python
- basic
categories: 学科笔记
thumbnail: http://orkqx44nq.bkt.clouddn.com/2017-09-08-15048024538436.jpg?imageView2/0/q/42|imageslim
---
 
python 学习笔记系列



# 辨析 is 和 == 

is

is will return True if two variables point to the same object, == if the objects referred to by the variables are equal.

| is | == |
| :-: | :-: |
| **is** will return True if two variables point to the same object | **==** if the objects referred to by the variables are equal. |
|is 只有当两者指向同一个对象的时候才为True|== 当两者的值相等时即为 True|
 
示例
 
```python
>>> a = [1, 2, 3]
>>> b = a
>>> b is a 
True
>>> b == a
True
>>> b = a[:]
>>> b is a
False
>>> b == a
True
```
## 对象的缓存机制


python中, 小整数([-5, 120])和短字符串对象会被缓存, 方便下次快速调用, 比如:

```python
>>> a = 1
>>> b = 1
>>> a is b
True
```
这里的1就被缓存起来了. 字符串的缓存有点小复杂:

```python
>>> a = "短字符串"
>>> b = "短字符串"
>>> a is b
True
>>> a = "长字符串"*1000
>>> b = "长字符串"*1000
>>> a is b
False
>>> a = "短 字符串"
>>> b = "短 字符串"
>>> a is b
False

```
python会缓存短字符串, 但是如果短字符串中有空格则不会被缓存orz.个人理解, 使用比较频繁的字符串就是变量名了(字母、数字、下划线), 所以进行缓存. 毕竟缓存也是需要内存开销的, 所以缓存大整数、长字符串就得不偿失了.



## 参考
* https://neo1218.github.io/pymemory/
* https://stackoverflow.com/questions/132988/is-there-a-difference-between-and-is-in-python

