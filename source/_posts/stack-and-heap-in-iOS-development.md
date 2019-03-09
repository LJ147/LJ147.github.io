---
title: 浅析iOS中的堆与栈
tags: [iOS]
categories: 学科笔记
date: 2017-06-24 02:24
updated: 2017-09-21 02:18:16
description:
keyword:
---



本文永久更新地址：http://hellogod.cn/stack-and-heap-in-iOS-development/


学习Objective-C的时候，很明显的一点感受就是这门语言和C++非常接近（这不废话吗QAQ）。虽然苹果爸爸对于底层的保护做的很好（封闭），让我们对于底层实现方式了解的不是很透彻，但还是能了解一二，相信对于之后的深入开发也很有帮助。

下面是之前做的一个关于iOS中堆栈的小演示。

![Page1](https://ws1.sinaimg.cn/large/006tKfTcly1fs3uxt2687j30yg0nrn2n.jpg)
![Version 1](https://ws1.sinaimg.cn/large/006tKfTcly1fs3uxu0je3j30yg0nr78y.jpg)
![Version 2](https://ws2.sinaimg.cn/large/006tKfTcly1fs3uxuh7xgj30yg0nrgqh.jpg)

![Code](https://ws3.sinaimg.cn/large/006tKfTcly1fs3uxvekj9j30yg0nrn21.jpg)


![Heap VS Stack](https://ws1.sinaimg.cn/large/006tKfTcly1fs3uxwd35tj30yg0nr0y7.jpg)
![memory management](https://ws3.sinaimg.cn/large/006tKfTcly1fs3uxxas55j30yg0nrgtm.jpg)



顺便安利一发之前授课老师安利的小册子：[《高质量 C++/C 编程指南》](https://github.com/NapleC/Coding-Developer-Book/blob/master/C语言/林锐·高质量C%20%20编程指南.pdf)，可谓短小精悍。

主要讲解了C++中的一些核心问题，一些经常容易出现错误但又经常被忽略的地方。

十分推荐下载PDF反复阅读，同时请注意版权问题。
![高质量 C++/C 编程指南](https://ws3.sinaimg.cn/large/006tKfTcly1fs3uxy8qu5j30yg0syn0a.jpg)
<!-- more -->

