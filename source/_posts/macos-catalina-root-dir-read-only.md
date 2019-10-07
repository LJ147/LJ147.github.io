---
title: 解决 macOS 10.15 根目录只读问题
tags:
  - macOS
date: 2019-10-07 11:16:19
updated: 2019-10-07 11:16:19
categories: 工作
description: 很开心的
---

<!-- more -->

写在最前面，本人以切身体会告诉你，工作机不要乱升级，尤其是 10.15 这种级别的大更新。

如果是自己的日用机并且你喜欢折腾，欢迎体验新的 macos Catalina。

之前一篇文章也提到，[iOS 13 和 macOS Catalina 初体验](https://mp.weixin.qq.com/s/cejnbYyV0AXWknG8oL0YAw)，新版本的 macOS 有很多很棒的地方，但是同样存在很多坑，虽然有些我并不认为是系统本身的问题。

其中最重要的是，macOS 10.15 中根目录变成了只读，原来很多喜欢往根目录 / 下面写东西的软件都会失效，对我来说，可能问题更严重一些。

我司的一个 log 日志组件，默认在根目录下创建目录写 log，例如 /app/log，最关键的时候写日志的路径还写死在了代码里，直接导致我在本地无法启动项目。

我自己很认可这种改动，保护根目录，也是保护系统安全，方便恢复。





# 参考链接

- https://www.v2ex.com/t/606592#reply4
- https://v2ex.com/t/606592#reply8