---
title: 解决 macOS 10.15 根目录只读问题
tags:
  - macOS
date: 2019-10-07 11:16:19
updated: 2019-10-07 11:16:19
categories: 工作
description: 惨兮兮的 zzz
---

<!-- more -->

写在最前面，本人以惨痛教训告诉你，工作机不要乱升级，尤其是 10.15 这种级别的大更新。

如果是自己的日用机并且你喜欢折腾，欢迎体验新的 macos Catalina。

之前一篇文章也提到：[iOS 13 和 macOS Catalina 初体验](https://mp.weixin.qq.com/s/cejnbYyV0AXWknG8oL0YAw)，新版本的 macOS 有很多很棒的地方，但是同样存在很多坑，虽然有些我并不认为是系统本身的问题。

其中最重要的是，macOS 10.15 中根目录变成了只读，原来很多喜欢往根目录 / 下面写东西的软件都会失效，对我来说，可能问题更严重一些。

背景故事：

![image-20191008090206601](https://tva1.sinaimg.cn/large/006y8mN6gy1g7qikkt2qnj310q0u047v.jpg)

我遇到了同样的问题......

![](https://tva1.sinaimg.cn/large/006y8mN6gy1g7oiqupu7fj31080eoq4g.jpg)

一开始我是认可这种改动的，而且认为毕竟大家都是最终要升级的，总归要改的对吧？抱着这种念头用 Windows 开发了一周，最后顶不住了开始找解救方案。

解决方案：

1.关闭SIP

2.执行 `sudo mount -uw /` 

3.根目录下新建文件夹并赋权 sudo `mkdir /xxx`，`sudo chmod 777 /xxx`



所以这种东西为什么要写死在代码呢？感谢 v 站。

# 参考链接

- [升级 macOS 10.15 之后根目录只读，公司项目打不开了，求助 555](https://www.v2ex.com/t/606592#reply4)
- [mac os 升级 catalina 之后，没有办法在根目录新建文件，导致依赖 Cat 的 Java 项目无法启动](https://v2ex.com/t/606592#reply8)
- [Mac开启关闭SIP 系统完整性保护](https://www.jianshu.com/p/fe78d2036192)