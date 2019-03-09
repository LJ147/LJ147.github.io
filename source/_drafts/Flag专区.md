---
title: Flag专区-第一周
description:  
tags: [flag,每周记录]
date: 2017-09-17 03:46:26
updated: 2017-09-19 16:38:15
categories: 每周记录
thumbnail:
---

这里准备把flag专区做成每周记录，7天一次更新。算是对自己的鞭策。

# 2017-09-21
## 待办

- [x] 吴恩达教程
- [x] 锻炼

# 2017-09-20
## 待办

- [ ] 论文
- [ ] 算法
- [ ] 扇贝打卡
- [ ] 数据结构
- [ ] cs231n 
- [ ] 吴恩达教程
- [ ] 锻炼


# 2017-09-19
## 待办

- [x] 算法
- [x] 扇贝打卡
- [x] 数据结构
- [x] 锻炼
<!-- more -->
 
<center>一张很有意思的slide</center>
### Top N 问题
从N个数中找到前k个最大数

### 堆排序
维基百科代码
更多参见我之前的文章：[如何选择恰当的排序算法](http://hellogod.cn/2017-09-14/%E5%A6%82%E4%BD%95%E9%80%89%E6%8B%A9%E6%9C%80%E6%81%B0%E5%BD%93%E7%9A%84%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95%EF%BC%9F/)

```python
#!/usr/bin/env python
#-*-coding:utf-8-*-

def heap_sort(lst):
    def sift_down(start, end):
        """最大堆调整"""
        root = start
        while True:
            child = 2 * root + 1
            if child > end:
                break
            if child + 1 <= end and lst[child] < lst[child + 1]:
                child += 1
            if lst[root] < lst[child]:
                lst[root], lst[child] = lst[child], lst[root]
                root = child
            else:
                break

    # 创建最大堆
    for start in xrange((len(lst) - 2) // 2, -1, -1):
        sift_down(start, len(lst) - 1)

    # 堆排序
    for end in xrange(len(lst) - 1, 0, -1):
        lst[0], lst[end] = lst[end], lst[0]
        sift_down(0, end - 1)
    return lst
            
def main():
    l = [9,2,1,7,6,8,5,3,4]
    print l
    heap_sort(l)
    print l

if __name__ == "__main__":
    main()
```
python2.x

|  range | xrange |  
|  --- |  --- | 
| return a list | a sequence object that evaluates lazily. | 

to see more details

    >>> print xrange.__doc__
    


 
 
# 2017-09-18
## 待办

- [x] 扇贝打卡
- [x] 数据结构
- [x] 锻炼

- [Python 2 和 Python 3 有哪些主要区别？](https://www.zhihu.com/question/19698598)
- [谈谈数据结构] ( http://dwz.cn/6wv1UV)
- python list 部分源码 
 
 

# 2017-09-17
## 待办
- [ ] 论文
- [ ] 算法
- [x] 扇贝打卡
- [x] 锻炼
- [ ] 数据结构

- zsh iTerm2 基础学习      

- [NIPS 2016最全盘点：主题详解、前沿论文及下载资源](https://zhuanlan.zhihu.com/p/24347256)
- [吴恩达 NIPS 2016 :如何使用深度学习开发人工智能应用?](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650721081&idx=1&sn=d557968703d4af879b5cf6461069dacd&chksm=871b0f47b06c865185865fcd5ef92af7726e84ae9e689b7ced9986a08c9fe3113df296a8469a&scene=21#wechat_redirect)

