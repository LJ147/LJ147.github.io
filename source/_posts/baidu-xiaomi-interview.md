---
title: 百度小米2018实习生面试面经
tags:
  - 百度
  - 小米
  - 面经
  - 算法
categories: 面试
date: 2018-01-23 14:06:53
updated: 2018-01-23 14:06:53
description: 失败*2 失败*3
keyword: 面试
---




![](https://ws1.sinaimg.cn/large/006tKfTcly1fs3uzozaa0j310c0psn5h.jpg)

<center>封面</center>



<!-- more -->

说起来真的是很凄惨呢，百度的挂在了二面，小米还在等通知，但是表现不好，很大概率也会被拒。

> 1.25 update 已收到拒信

怎么说呢，选择了这条路，就要走下去吧。不得不说，这几次下来，对自己还是有一定打击。

> 有位学长说的其实蛮好：真正重要的不是面试技巧，是你真正做出来的东西，共勉。

# 百度

推荐的部门是搜索推荐相关

## 一面

本来要求去北京面试，和hr沟通之后面试官同意电话面，好感plus。

流程：
**1.自我介绍**
一五一十
**2.聊项目经历**

面试官对我的主要项目（物体检测）不是很了解，另外两个做的并不深入，所以聊起来比较尬。

**3.算法题**

问题描述： 
无序数组array, 找到数组中两个数的最大差值, 且大数出现在小数之后，如：arr[i]-arr[j], 且 i<j 
比如： array 是 [2, 3, 10, 6, 4, 8, 1]，最大差值是8（10-2）

[这里](http://blog.csdn.net/light_lj/article/details/49490261) 是一个时间复杂度O(n),空间复杂度O(1)的解法。

> 1) 记录当前访问过的数组中的最小值 min_val;
2) 当前元素值arr[i] - min_val 和 max_diff作比较
   若大于 max_diff , 则更新它的值

C++代码如下

```cpp
#include <iostream>
using namespace std;

int maxDiff(int *arr, int n)
{
        int min_val = arr[0];
        int max_diff = arr[1]-arr[0];
        for(int i=1; i<n; ++i)
        {
                if(max_diff <(arr[i]-min_val))
                        max_diff = arr[i] - min_val;
                min_val = arr[i]<min_val?arr[i]:min_val;
        }
        return max_diff;
}


int main()
{
        int arr[] = {2, 3, 10, 6, 4,8,1};
        cout<<maxDiff(arr, 7)<<endl;
}

```


**4.机器学习基础**

- CNN中过拟合是如何产生的？
- 训练过程中的梯度消失和梯度爆炸是如何产生的？应该如何解决？ 


## 二面

二面是一个女面试官，没有算法题，主要在聊OCR的项目，比较关注具体的实现和效果的提示，最后问了一些没有接触的知识。


- 详细介绍一个常见的传统学习算法

介绍了K-means的基本算法流程，提问部分问了如何选取k值和初始的k个点，什么时候结束训练过程

- 介绍一下常见的推荐算法？
- 如何计算两段文本之间的相似度？



 
应该是挂在了这里，面试官给我介绍了下他们的部分，主要是做搜索推荐，问到这里的时候比较尴尬，面试官问我是不是了解LR，但是当时听得不是很清楚，加上脑子短路，竟然一时没有想起来LR就是逻辑回归(Logistic Regression, LR)，之后又问了协同推荐的一些东西，之前了解的不多，有些尬。

> update： 2018-08-13  

再回头看是真的头铁，记得当时文本相似度的计算答的也是烂的一批。

# 小米

## 项目相关
- 数据库的大量数据（百万级别）如何做存储优化？

## 算法题

三道算法题，现场手写。  




- 顺序打印螺旋数组

最简单明了的方法，但是写起来相对比较复杂：

``` java
public List<Inter> printList(int[][] arr){

	List<Inter> result = new ArrayList<>();

	if((arr == null) || (arr.length == 0) || arr[0].length == 0){
		return result;
	}
	int left = 0;
	int right = arr[0].length - 1;
	int top = 0;
	int bottom = arr.length - 1;

	while(true){
		// 向右遍历
		for(int j = left; j <= right; j++){
			result.add(arr[top][j]);
		}
		top++;
		if(top > bottom){
			break;
		}

		// 向下 
		for(int i = top; i <= bottom; i++){
			result.add(arr[i][right]);
		}
		right--;
		if(left > right){
			break;
		}

		// 向左遍历
		for(int j = right; j >= left; j--){
			result.add(arr[bottom][j]);
		}
		bottom--;
		if(top > bottm){
			break;
		}

		// 向上遍历
		for(int i = bootm; j>= top; i--){
			result.add(arr[i][left]);
		}
		left++;
		if(left > right){
			break;
		} 


		return result;
	}

}

```

更简洁的Python代码：

``` python

class Solution:
 
    def printMatrix(self, matrix):
        res = []
        while matrix:
            res += matrix.pop(0)
            if matrix and matrix[0]:
                for row in matrix:
                    res.append(row.pop())
            if matrix:
                res += matrix.pop()[::-1]
            if matrix and matrix[0]:
                for row in matrix[::-1]:
                    res.append(row.pop(0))
        return res

```

明白说了考察 [代码实现](http://blog.csdn.net/xiaowei_cqu/article/details/8258071)

- `O(1)`空间复杂度反转链表

很常规的一道 [题目](https://www.nowcoder.com/practice/75e878df47f24fdc9dc3e400ec6058ca?tpId=13&tqId=11168&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)。

- 如何求解单向链表是否存在环、求取环的长度、求取环的入口、求取总链表的长度

是否存在环：可以用两个快慢指针，快指针每步走两格，慢指针每步走一格；
环的长度：先用快慢指针找到交点，同时记录慢指针走的步数，让一个
## 基础

- 进程锁的种类

这里莫名其妙蒙圈了，只答出一个读写锁。 回来之后查了一些资料，似乎也有些不清楚，按照表现形式，常见的锁：读写锁（rwlock）、自旋锁(spinlock)、互斥锁(mutex)、顺序锁(seqlock)。

这里又要感慨一番，真的复习起来，要重新捡起来的东西实在是太多了，想要雨露均沾几乎是不可能的，只有在某一个方面表现得尤为突出才能做到瑕不掩瑜！
- 讲讲`C++`和`Java`的多态（polymorphism）

**多态** 是面向对象编程语言的重要特性，它允许基类的指针或引用指向派生类的对象，而在具体访问时实现方法的动态绑定


C++主要基于虚函数和虚函数表实现（动态绑定），由此引申一系列诸如重载、重写、隐藏的比较绕口实际差别很大的东西——但总是有人会绕这些没有意义的概念，什么指针函数、函数指针，常量指针、指针常量。

说到这里，涉及到继承关系的时候，最好是把析构函数设置为虚函数，然后在子类中利用多态特性进行覆盖，这样在delete子类对象的时候可以调用每个子类对应的析构函数进行释放空间等工作。

![](https://ws1.sinaimg.cn/large/006tKfTcly1fs3uzs7usyj30ck04y0sy.jpg)

![](https://ws3.sinaimg.cn/large/006tKfTcly1fs3uzt6cwgj30ih08574z.jpg)
上述两幅图均来自 [博客](http://blog.jobbole.com/107432/)

```cpp

#include<iostream>
using namespace std;
//基类对象
class Base
{
public:
    //有virtual关键字，运行时多态
    virtual void f(float x)
    {
        cout<<"Base::f(float)"<< x <<endl;
    }
    //无viratul关键字，不会发生运行时多态
    void g(float x)
    {
        cout<<"Base::g(float)"<< x <<endl;
    }
    void h(float x)
    {
        cout<<"Base::h(float)"<< x <<endl;
    }
};
class Derived : public Base
{
public:
    virtual void f(float x)
    {
        cout<<"Derived::f(float)"<< x <<endl;   //多态、覆盖
    }
    //子类与父类的函数同名，无virtual关键字，则为隐藏
    void g(int x)
    {
        cout<<"Derived::g(int)"<< x <<endl;     //隐藏
    }
    void h(float x)
    {
        cout<<"Derived::h(float)"<< x <<endl;   //隐藏
    }
};
int main(void)
{
    Derived d;    //子类
    Base *pb = &d;    //基类指针指向子类
    Derived *pd = &d;    //子类指针指向自己
    // Good : behavior depends solely on type of the object
    pb->f(3.14f);   // Derived::f(float) 3.14    调用子类，多态
    pd->f(3.14f);   // Derived::f(float) 3.14    调用子类
    // Bad : behavior depends on type of the pointer
    pb->g(3.14f);   // Base::g(float)  3.14    无多态，调用自己的
    pd->g(3.14f);   // Derived::g(int) 3     无多态，调用自己的
    // Bad : behavior depends on type of the pointer
    pb->h(3.14f);   // Base::h(float) 3.14    无多态，调用自己的
    pd->h(3.14f);   // Derived::h(float) 3.14    无多态，调用自己的
    return 0;
}
```
代码引自 [这里](http://huqunxing.site/2016/09/08/C++%20%E4%B8%89%E5%A4%A7%E7%89%B9%E6%80%A7%E4%B9%8B%E5%A4%9A%E6%80%81/)

- 讲讲对于python底层的了解
- C++如何释放二维数组空间


```cpp
 //申请、释放二维数组   
 int **p = new int*[5];
    for(int i=0; i<5; ++i)
        delete [] p[i];
    delete []p;
    return 0;
```

# 结语

自己有个习惯，喜欢看别人的博客，平时查资料看到好的博客，都会进到主页参观一番，有时候一路翻下来，花很多时间，但总是乐此不疲。

一篇一篇，多数是技术博文，就像在和一个人面对对交流，看到一个人的成长。

当然，多数情况下，博主们都是和我一样，喜欢立一些 `flag`，鲜有能坚持下去的。

又刚好在微博看到一些关于碎片阅读的观点：

![](https://ws1.sinaimg.cn/large/006tKfTcly1fs3uzviyacj30x40ougq4.jpg)

厚着脸皮说一句不谋而合，近期对这个越来越有感触，很多时候看博客都图 **省事**，但是没有系统的学习，琐碎的看一下碎片知识，其实很难形成一个整体，之后也要多加注意。

或者说，博客只能用于临时 `备忘`，不能希翼更多。博客上写的一些东西，多数是拾人牙慧（说的自然是我这样一类），不能过分依赖。

至于近期的面试，其实也是属于不得已。自己独立学习的时候总感觉方向不是那么明显，所以希望有面试来不断督促自己，有压力也许会好一点？

offer倒是其次，学习为主吧。


最后，似乎更完一篇文章最近的愧疚感有所减轻呢。长久的摸鱼，什么时候能有所改观呢......

一个高度自律的人。

# 参考

- http://blog.csdn.net/light_lj/article/details/49490261
- [封面](https://www.bilibili.com/video/av2753899/)
- [例图](http://blog.jobbole.com/107432/)
- [多态在 Java 和 C++ 编程语言中的实现比较
](https://www.ibm.com/developerworks/cn/java/j-lo-polymorph/)

