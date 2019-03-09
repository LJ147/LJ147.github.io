---
title: 计算机基础知识回顾-01
tags:
  - 计算机网络
  - 基础
  - 大学
categories: 学科笔记
date: 2018-01-24 03:32:18
updated: 2018-01-24 03:32:18
description: 计算机基础知识回顾
keyword: 
---

个人的一些【计算机网络基础】复习摘要，内容来自网络，文末标注了大部分来源，并非原创。


<!-- more -->

# 计算机网络协议
## OSI（Open System Interconnection）七层协议

制定统一的通信协议。
![](https://ws4.sinaimg.cn/large/006tKfTcly1fs3uzg27kxj30k00aumym.jpg)

## TCP/IP协议

OSI的一个简化版本

![](https://ws3.sinaimg.cn/large/006tKfTcly1fs3uzih4a0j3095049glo.jpg)

### IP地址分类

![](https://ws2.sinaimg.cn/large/006tKfTcly1fs3uzjc3z3j318y0f00xx.jpg)
### 面向连接的可靠的TCP协议

- 建立连接三次握手
- 断开连接四次握手
- URL（Uniform Resource Locator）统一资源定位符

URL的格式由三部分组成：
①第一部分是协议(或称为服务方式)。
②第二部分是存有该资源的主机IP地址(有时也包括端口号)。
③第三部分是主机资源的具体地址，如目录和文件名等。

- POST和GET请求

请求报文不同，请求方式不同，安全级别不同

1. **幂等**是指同一个请求方法执行多次和仅执行一次的效果完全相同。
2. 根据http的设计，大家在看到get的时候，都期望这个请求对服务器没有修改，看到post的时候，都认为这对服务器产生了修改。
3. 安全性： 对于POST来说，请求的报文却不会被记录，这些对于敏感数据来说，POST更安全一些。



![](https://ws4.sinaimg.cn/large/006tKfTcly1fs3uzkqjbpj31bq0sg46n.jpg)
![](https://ws4.sinaimg.cn/large/006tKfTcly1fs3uzlokxmj31a60dy40q.jpg)


- 常见的状态响应码

![](https://ws4.sinaimg.cn/large/006tKfTcly1fs3uznkr1bj31j80zkn98.jpg)

- RESTful API设计

    - 协议
    - 域名
    - 版本
    - 路径
    - HTTP动词
    - 过滤信息
    - 状态码
    - 错误处理
    - 返回结果
    - Hypermedia API （即返回结果中提供链接，连向其他API方法，使得用户不查文档，也知道下一步应该做什么。）

- Cookie、session和token   

    - 存在位置
    - Cookie一般有时效性，存在跨域问题
    - token不存在跨域问题

Cookie： 名称(key)、值(value)、有效域(domain)、路径(域的路径，一般设置为全局:"\")、失效时间、安全标志(指定后，cookie只有在使用SSL连接时才发送到服务器(https))
    
一个网站的网址组成包括协议名，子域名，主域名，端口号。比如 https://github.com/ ，其中https是协议名，www是子域名，github是主域名，端口号是80，当在在页面中从一个url请求数据时，如果这个url的协议名、子域名、主域名、端口号任意一个有一个不同，就会产生跨域问题。
即使是在 http://localhost:80/ 页面请求 http://127.0.0.1:80/ 也会有跨域问题
    
    
# 参考

- https://raw.githubusercontent.com/zqjflash/tcp-ip-protocal/master/tcp-ip-protocal.png
- https://www.zhihu.com/question/24002080/answer/150830722
- https://cuiqingcai.com
- https://zhuanlan.zhihu.com/p/22536382
- http://www.w3school.com.cn/tags/html_ref_httpmethods.asp
- https://www.zhihu.com/question/28586791
- http://www.ruanyifeng.com/blog/2014/05/restful_api.html

