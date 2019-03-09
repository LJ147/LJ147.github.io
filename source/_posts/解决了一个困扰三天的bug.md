---
title: 解决了一个困扰三天的bug
date: 2017-08-02 02:25:23
tags: 
- 开发笔记
- Spring Boot
- Java
categories: 开发笔记
description: Spring Boot中 hibernate 延迟加载 | 懒加载（lazy loading）造成序列化失败

---

描述：Spring Boot中 hibernate 延迟加载 | 懒加载（lazy loading）造成序列化失败


明日填坑

过了好几天才来填，很难过，因为当时解决的时候没有立即记录，现在我对着电脑发呆，想了十分钟记不起这个bug到底是什么。

可啪。


于是决定记录新遇到的一个问题。 

# 一、Spring hibernate 懒实例化
Spring Boot中 `hibernate` 延迟加载 | 懒加载（lazy loading）造成序列化失败


## 问题描述

背景很简单，一个家长（Guardian）对应多个孩子（Student）

首先在家长bean里定义 `List<Student> students` ，接着通过guardian对象的`guardian.getStudents()`获取对应的学生对象，按理说没有任何问题

Guardian.java 家长bean

``` java
@Entity
@Table(name = "Guardian")
public class Guardian {

    @OneToMany
    private List<Student> students; //学生列表

}

```

 GuardianController.java  

``` java
@ApiOperation(value = "孩子列表")
    @GetMapping(value = "/children")
    public  List<Student> children(HttpServletRequest request) throws ServletException {

        Guardian guardian = userService.currentGuardian(request);
        return guardian.getStudents();
    }
```

 * 在IDEA本地运行的时候接口正常:

 ![7FE3731E-DE7B-49BB-A644-941D10D14212](https://ws1.sinaimg.cn/large/006tKfTcly1fs3uyitqclj30un0j5goh.jpg)

 
 * 但是奇怪的是部署到服务器Tomcat上之后接口报错：
 * 
 ![](https://ws4.sinaimg.cn/large/006tKfTcly1fs3uyj9o1mj30ui0dxtae.jpg)
 
输出如下：

``` 
{
    "timestamp": 1501826190599,
    "status": 500,
    "error": "Internal Server Error",
    "exception": "org.springframework.http.converter.HttpMessageNotWritableException",
    "message": "Could not write content: could not extract ResultSet (through reference chain: org.sklse.lab.bean.ResultModel[\"content\"]->org.hibernate.collection.internal.PersistentBag[0]->org.sklse.lab.bean.Student[\"submittedHomeworks\"]); nested exception is com.fasterxml.jackson.databind.JsonMappingException: could not extract ResultSet (through reference chain: org.sklse.lab.bean.ResultModel[\"content\"]->org.hibernate.collection.internal.PersistentBag[0]->org.sklse.lab.bean.Student[\"submittedHomeworks\"])",
    "path": "/edu/guardian/children"
}
```
## 解决方案
一番debug之后很是头疼，后来请教了一位长者，指出可能是`懒实例化`的问题，于是查找到[解决方案](http://www.jianshu.com/p/c676fd86a219)，在Spring Boot的`application.properties`配置项添加：


```
spring.jpa.properties.hibernate.enable_lazy_load_no_trans=true
```
于是问题顺利解决

## 思考
 
> 这个例子当中的`guardian.getStudents()`是延迟加载的，最开始的studentList其实放的是 Hibernate 的 [PersistentBag](https://docs.jboss.org/hibernate/orm/3.2/api/org/hibernate/collection/PersistentBag.html) ，这个对象是不可以序列化的。

 待补充细节


# 二、Tomcat缓存问题


本文链接：http://hellogod.cn/2017-08-02/解决了一个困扰三天的bug/


