---
title: 重学Java（1）
tags:
  - Java
  - 未完待续
date: 2019-07-11 13:55:58
updated: 2019-07-11 13:55:58
categories: 学科笔记
description: 我司大量使用 Java，所以重新学习一下。
---

希望 flag 不会那么快倒下hhh

<!-- more -->

# 1.Java 8 语言特性

## 1.1 Steam()

函数编程的思想

> In functional programming, a monad is a structure that represents computations defined as sequences of steps. A type with a monad structure defines what it means to chain operations, or nest functions of that type together.

```java
List<String> myList =
    Arrays.asList("a1", "a2", "b1", "c2", "c1");

myList
    .stream()
    .filter(s -> s.startsWith("c"))
    .map(String::toUpperCase)
    .sorted()
    .forEach(System.out::println);
// C1
// C2
```

几种常见构建流的方式：

```java
 // 1. Individual values 单独值
        Stream stream = Stream.of("a1", "b1", "c1");
        stream.forEach(System.out::print);//打印 a1b1c1

        // 2. Arrays 数组
        String[] strArray = new String[] {"a2", "b2", "c2"};
        stream = Stream.of(strArray);
        stream = Arrays.stream(strArray);
        System.out.println(stream.collect(Collectors.joining(",")).toString());//打印 a2,b2,c2

        // 3. Collections 集合
        List<String> list = Arrays.asList(strArray);
        stream = list.stream();
```

理解就好，需要具体 API 的时候查一查也无妨。

# 2.Gradle 和 Maven

两者同为构建工具，大同小异，各有各的优势缺点。多了解即可。

# 3.Spring Boot

出去团建和同事聊到之前试用过 Spring Boot，有人随口问了句，Spring Boot 到底是什么，一时头绪很多，不知从何讲起，只说了一句是一个集成了很多 web 开发工具的脚手架。

这个框架，自己之前使用过很长时间，但是更多时候是知道如何使用，而没有深入了解其原理，现在尝试从更加 high level 的角度重新理解一下。

其实如果一步一步的使用各种框架，例如早期的 SSM 框架，可能对于其作用理解更深，但是技术更新快，过时的技术，很快就被抛到后面。

## 3.1 Spring Boot 是什么

下面是官网对于框架的描述：

> Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".

所以其作用就是帮助开发人员更加快速的开发出 Spring 项目，很多时候都是这样，一个框架好不好用，决定了其用户规模。

优势：

- Create stand-alone Spring applications
- Embed Tomcat, Jetty or Undertow directly (no need to deploy WAR files)
- Provide opinionated 'starter' dependencies to simplify your build configuration
- Automatically configure Spring and 3rd party libraries whenever possible
- Provide production-ready features such as metrics, health checks and externalized configuration
- Absolutely no code generation and no requirement for XML configuration

## 3.2 如何做到以上几点？



## 3.3 Spring 简单介绍



# 参考

- [Java构建工具:Maven与Gradle的对比](https://zhuanlan.zhihu.com/p/21394120)
- https://gradle.org/maven-vs-gradle/
- https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html
- [阿里巴巴Java 开发手册](http://techforum-img.cn-hangzhou.oss-pub.aliyun-inc.com/阿里巴巴Java开发手册(终极版).pdf)
- [理解 Spring boot](https://juejin.im/post/5a50b189518825732334f713) 
- [Spring boot 官网](https://spring.io/projects/spring-boot)
- [Spring Boot深入理解](https://www.5210blog.com/SpringBoot02/) 
- https://winterbe.com/posts/2014/07/31/java8-stream-tutorial-examples/
- https://www.jianshu.com/p/d69a5d9ad5ec

