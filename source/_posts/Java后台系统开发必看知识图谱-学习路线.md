---
title: Java后台系统开发必看知识图谱-学习路线
date: 2017-04-05 04:21:16
tags:
- 原创
- Java
- 后台
- 图谱
category: 开发笔记
thumbnail: http://orkqx44nq.bkt.clouddn.com/24823_963e_12.jpg
---
 java后台开发知识图谱 & 高频技术汇总
 
# 1.引言：
学习一个新的技术时，其实不在于跟着某个教程敲出了几行、几百行代码，这样你最多只能知其然而不知其所以然，进步缓慢且深度有限，最重要的是一开始就对整个学习路线有宏观、简洁的认识，确定大的学习方向，这样才能事半功倍。

我们经常会遇到这样的情况：
 一开始学习一门新技术的时候，面对着很多很多陌生的名词，无从下手，一度想要放弃。
本文首先会给出关于**java后台开发**和**前端适配**的一些建议学习路线，接着简单解释一些应用到的高频技术，帮助大家理解和学习，算是一个入门篇。

# 2.Java后台开发知识一览

## 1、后端
* WEB服务器：Weblogic、Tomcat、WebSphere、JBoss、Jetty 
* 核心框架：Spring Framework  
* 分布式服务框架	Dubbo（感谢@[浅浅浅丿忧伤](http://www.jianshu.com/u/03773555eb45)指正）
* 安全框架：Apache Shiro 
* 视图框架：Spring MVC
* 服务端验证：Hibernate + Validator 
* 布局框架：SiteMesh 
* 工作流引擎：Activiti 
* 任务调度：Spring Task + Quartz
* 持久层框架： MyBatis  + MyBatis-Plus 
* 数据库连接池：Alibaba Druid 
* 缓存框架：Ehcache 、Redis
* 日志管理：SLF4J 、Log4j
* 会话管理：Spring-Session
* 工具类：Apache Commons、Jackson 、Xstream、Dozer 、POI 
* 消息队列：	ActiveMQ
* 云存储：阿里云 OSS 腾讯云 COS 七牛云
* 版本管理： git（推荐）  svn

## 2、前端

* JS框架：jQuery 1.9。
* 前端框架：Angular JS + Bootstrap + Jquery
* CSS框架：Twitter Bootstrap 2.3.1
* 客户端验证：JQuery Validation Plugin 1.11。
* 富文本在线编辑：CKEditor
* 在线文件管理：CKFinder
* 动态页签：Jerichotab
* 手机端框架：Jingle
* 数据表格：jqGrid
* 对话框：jQuery jBox
* 下拉选择框：jQuery Select2
* 树结构控件：jQuery zTree
* 日期控件： My97DatePicker


# 3.高频技术（可大致浏览，作为目录查看）
* **Spring** 

![spring_framework.gif](https://ws3.sinaimg.cn/large/006tKfTcly1fs3uy4ag4yg30ff080aa4.gif)

  * 每个模块的功能如下：
* 核心容器：核心容器提供 Spring 框架的基本功能。核心容器的主要组件是 BeanFactory，它是工厂模式的实现。
  * Spring 上下文：Spring 上下文是一个配置文件，向 Spring 框架提供上下文信息。
  * Spring AOP：通过配置管理特性，Spring AOP 模块直接将面向方面的编程功能集成到了 Spring 框架中。
  * Spring DAO：JDBC DAO 抽象层提供了有意义的异常层次结构，可用该结构来管理异常处理和不同数据库供应商抛出的错误消息。异常层次结构简化了错误处理。
  * Spring ORM：Spring 框架插入了若干个 ORM 框架，从而提供了 ORM 的对象关系工具，其中包括 JDO、Hibernate 和 iBatis SQL Map。所有这些都遵从 Spring 的通用事务和 DAO 异常层次结构。
  * Spring Web 模块：Web 上下文模块建立在应用程序上下文模块之上，为基于 Web 的应用程序提供了上下文。所以，Spring 框架支持与 Jakarta Struts 的集成。
  * Spring MVC 框架：MVC 框架是一个全功能的构建 Web 应用程序的 MVC 实现。MVC 容纳了大量视图技术，其中包括 JSP、Velocity、Tiles、iText 和 POI。
参考链接：https://www.ibm.com/developerworks/cn/java/wa-spring1/

* ** RESTful风格**


![QQ20170405-214053@2x.png](https://ws1.sinaimg.cn/large/006tKfTcly1fs3uy58r56j30yg07v763.jpg)
* ** Mybatis**
 MyBatis 是支持定制化 SQL、存储过程以及高级映射的优秀的持久层框架。MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。MyBatis 可以对配置和原生Map使用简单的 XML 或注解，将接口和 Java 的 POJOs(Plain Old Java Objects,普通的 Java对象)映射成数据库中的记录。

* ** Hibernate**

![Hibernate.png](https://ws3.sinaimg.cn/large/006tKfTcly1fs3uy5pvn2j30yg0m7n4c.jpg)
参考链接：
[Hibernate官网](http://hibernate.org)

* ** Redis**
Redis 是完全开源免费的，遵守BSD协议，是一个高性能的key-value数据库。
特点：
 * 1.Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
  * 2.Redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。
  * 3.Redis支持数据的备份，即master-slave模式的数据备份。
参考链接：
[Redis官网](http://redisinaction.com/preview/chapter1.html)

* ** Zookeeper**
　Zookeeper 分布式服务框架是 Apache Hadoop 的一个子项目，它主要是用来解决分布式应用中经常遇到的一些数据管理问题，如：统一命名服务、状态同步服务、集群管理、分布式应用配置项的管理等等。

![ZooKeeper.png](https://ws4.sinaimg.cn/large/006tKfTcly1fs3uy6l26qj30yg0u0jx6.jpg)
* ** DUBBO**
DUBBO是一个分布式服务框架，致力于提供高性能和透明化的RPC远程服务调用方案，是阿里巴巴SOA服务化治理方案的核心框架，每天为2,000+个服务提供3,000,000,000+次访问量支持，并被广泛应用于阿里巴巴集团的各成员站点。
参考链接：
[DUBBO官网](http://dubbo.io)
[教程](https://dangdangdotcom.github.io/dubbox/rest.html)

# 4.写在最后：
欢迎指正批评与交流，本博客将长期更新维护：

 [个人主页](http://www.hellogod.cn)
 ![文末福利](https://ws2.sinaimg.cn/large/006tKfTcly1fs3uy747gcj30yg0lj435.jpg)

