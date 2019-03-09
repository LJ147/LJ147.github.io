---
title: 一时打卡小玩意
tags:
  - 日常
  - leetcode
  - 后端
categories: 日常
date: 2019-03-03 18:51:45
updated: 2019-03-03 18:51:45
description: 瞎折腾系列
keyword:
---


# 一、LeetCode小组打卡：一时打卡


## 1.1 项目背景

和朋友相约在LeetCode上打卡，就组成了小组的形式，既然要打卡，自然就有查卡，一开始是大家刷完题把截图
发到群里，然后肉眼查卡，后来为了偷懒就写了这个小玩意（为了偷懒搞出更多事情系列）。

## 1.2 项目预览

> 部署地址：[group.hellogod.cn](http://group.hellogod.cn/#/check)

![PC端](https://ws2.sinaimg.cn/large/006tKfTcly1g0phjoxnfqj31h00u0n8d.jpg)
<!-- more -->

![移动端](https://ws4.sinaimg.cn/large/006tKfTcly1g0pjcdvopkj30ku11242o.jpg)

## 1.3 功能

定时查询小组内同学的打卡情况，你可以通过 [腾讯问卷：LeetCode主页搜集](https://docs.qq.com/form/fill/DUEhBb0ZGTFFwUVpz)，加入小组排行榜。


## 1.4 实现逻辑
爬虫根据用户主页地址，每小时定期爬取基础信息，存储在MySQL数据库，后端为前端提供对应接口。

# 三、技术栈

## 3.1 前端
UI基于 [startbootstrap-sb-admin-2](https://github.com/BlackrockDigital/startbootstrap-sb-admin-2) ，数据绑定基于AngularJS，页面跳转基于`ui-router`。

核心 js 文件为

-  `resources/js/app/app.js`  
-  `resources/js/app/controllers.js`

## 3.2 后端
Spring Boot 2.1.2


 - `bean` 实体类
 - `repository` 数据库操作
 - `service` 服务层
 - `controller` 对外发布接口

## 3.3 爬虫
Scrapy 1.5.0

爬虫部分代码：[spider_leetcode](https://github.com/LJ147/spider_leetcode)






