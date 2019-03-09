---
title: Objective-C基础知识点总结（一）
date: 2017-06-23 04:26:45
tags: 
- iOS 
- Objective-C
category: 开发笔记
---
 
长文，建议跳跃选择性阅读，大约10min可以读完全文。
 <!-- more -->

![iOS开发](https://ws1.sinaimg.cn/large/006tKfTcly1fs3uz7mln0j304v04vjrl.jpg)

# 1.目录

* 1.个人学习建议
* 2.知识点整理
* 3.下集预告


 iOS这一行，都过了这么多年，还是水分很足，没有几个愿意安安心心查资料写东西的。虽说博客都是互相抄，但是起码其他行业抄的最开始的人是对的，但是这一行因为中文资料少（是的，到现在中文资料也不完善），所以出现很多粗制滥造的，这里经过笔者校验之后分享一些相关知识。


个人建议：

* 入门视频首选是[斯坦福CS193P课程 iOS10, Xcode8 ,Swift 3 - Youtube](https://www.youtube.com/playlist?list=PLPA-ayBrweUz32NSgNZdl0_QISw-f12Ai)，白胡子老爷爷在这一行可以称得上是元老，之前还想出一个针对这个视频教程的学习笔记，后来给鸽了；这里链接放了YouTube上的最新视频，墙内的朋友也可以自行百度其他资源，我这里也存了一份百度云(16年的版本iOS9)，需要的可以在评论留下邮箱（某资源论坛既视感？？？）。

* 入门教材[Programming in Objective-C 6th edition（英文版）](https://github.com/frankfenghua/ios/blob/master/Programming%20in%20Objective-C%206th%20Edition/Programming%20in%20Objective-C%20-%206th%20Edition.pdf)，这里附上教材PDF下载链接，没有具体考证链接合法性，经济允许建议支持正版。

* 项目实战，大学生的话去实验室找一个项目做一做，大概几个月也就熟了（最初级的那种），这里还要感谢当初带我的学长@子豪学长——是一个很让人佩服的学长。社会人士自学的话可以在在github、码云上面多找找完整的客户端试试看。

下面是学习OC时对于一些知识点的总结，资料来源互联网，权当学习笔记，参考的资料尽量附上原文链接。

# 2.重要知识点总结 

其实下面的每一个点都可以单独行文，这里摘录其中较为重要的部分，同时添加链接供读者深度查看。之后可能单独领出深究，这里先埋坑。

#### 2.1 继承关系

OC中的继承属于单继承，这一点和Java类似。        
* 在Objective-C中super是指向直接父类的指针 
* 而self是指向本身的指针，self就相当于java中的this指针。

在Objectiv-C中几乎所有的类都是继承自NSObject类，NSObject类中存在大量功能强大的方法。这里不再赘述，详情可查看
* [Objective-C中的继承和多态](http://www.cnblogs.com/ludashi/p/3877735.html)



#### 2.2 MVC设计模式
![MVC](https://ws1.sinaimg.cn/large/006tKfTcly1fs3uz8myn8j30yg0jeagu.jpg)
[iOS开发——MVC详解&Swift＋OC](http://www.cnblogs.com/iCocos/p/4641787.html)
#### 2.3 block

这里搬运一下

block定义
``` objectivec
struct Block_descriptor {
    unsigned long int reserved;
    unsigned long int size;
    void (*copy)(void *dst, void *src);
    void (*dispose)(void *);
};


struct Block_layout {
    void *isa;
    int flags;
    int reserved; 
    void (*invoke)(void *, ...);
    struct Block_descriptor *descriptor;
    /* Imported variables. */
};

```
有人认为OC中block 本质应该是一个函数指针加上一个对应捕获上下文变量的内存块（结构体或者类）。
建议参考：
[知乎：OC中， block（块）的本质是什么？](https://www.zhihu.com/question/30779258)
 

#### 2.4   静态变量、静态常量、全局变量

##### static

static修饰的变量必须放在@implementation外面或方法中，它只在程序启动初始化一次。

``` objectivec
 static int num; 
```

##### const

const修饰的变量是不可变的，如果需要定义一个时间间隔的静态常量，就可以使用const修饰。

``` objectivec
static const NSTimeInterval LMJTimeDuration = 0.5;
```

如果试图修改TimeDuration编译器则会报错。

如果我们定义一个字符串类型的静态常量就要注意了，这两种写法是一样的，而且是可以修改的。
``` objectivec
static NSString const * LMJName = @"iOS开发者公会";
static const NSString * LMJName = @"iOS开发者公会";
```
这两种写法cons修饰的是* LMJName,*是指针指向符，也就是说此时指向内存地址是不可变的，而内存保存的内容时可变的。
所以我们应该这样写：

``` objectivec
static NSString * const LMJName = @"iOS开发者公会";
```
当我们定义一个对象类型常量的时候，要将const修饰符放到*指针指向符后面。

##### extern
extern修饰的变量，是一个全局变量。

extern NSString * LMJName = @"iOS开发者公会;
extern修饰的变量也可以添加const进行修饰：

extern NSString * const LMJName = @"iOS开发者公会;
此时全局变量只能被初始化一次
extern定义的全局常量的用法和宏定义类似，但是还是有本质上的不同的。 extern定义的全局常量更不容易在程序中被无意窜改。
*  [OC中的全局变量 与 static](http://blog.csdn.net/codeaswater/article/details/41648011)

* [iOS定义静态变量、静态常量、全局变量](http://www.jianshu.com/p/aec2e85b9e84)

* [浅析Objective-C中的堆与栈（PDF版）](http://www.jianshu.com/p/e83f983ded01)





#### 2.5 NSObject ,Id, instancetype

* NSObject 

NSObject确定对象类型是继承于NSObject。很常用。

* id

可以指向任意类型的objcetive-c的对象，声明的对象具有运行时的特性。并不一定是NSObject对象。对于一些不能进行类型检查或者不想检查的地方，可以使用id，经常会声明delegate为id类型，在运行的时候载使用respondToSelector:检查。

* instancetype

  stack overflow上面所说：“Use instancetype whenever it's appropriate, which is whenever aclass returns an instance of that same class.”
在instancetype有效的情况下，应该尽量去使用instancetype。


id数据类型，是一种通用的对象类型。也就是说，它可以用来存储属于任何类的对象。当以这种方式在一个变量中存储不同类型的对象时，在程序执行的期间，这种数据类型的真正优势就出现了。

instancetype和id的区别如下（ARC和MRC的讲解部分放在后面的2.7中）:

区别1:

在ARC(Auto Reference Count)环境下:

instancetype用来在编译期确定实例的类型,而使用id的话,编译器不检查类型, 运行时检查类型.

在MRC(Manual Reference Count)环境下:

instancetype和id一样,不做具体类型检查

区别2:

id可以作为方法的参数,但instancetype不可以

instancetype只适用于初始化方法和便利构造器的返回值类型

#### 2.6 Copy, strong, retain

> 先说copy和strong的区别，这里摘录一个例子。



在定义一个类的property时候，为property选择strong还是copy特别注意和研究明白的，如果property是NSString或者NSArray及其子类的时候，最好选择使用copy属性修饰。

为什么呢？这是为了防止赋值给它的是可变的数据，如果可变的数据发生了变化，那么该property也会发生变化。


代码示例

还是结合代码来说明这个情况
``` objectivec
@interface Person : NSObject
@property (strong, nonatomic) NSArray *bookArray1;
@property (copy, nonatomic) NSArray *bookArray2;
@end

@implementation Person
//省略setter方法
@end

//Person调用
main(){
    NSMutableArray *books = [@[@"book1"] mutableCopy];
    Person *person = [[Person alloc] init];
    person.bookArray1 = books;
    person.bookArray2 = books;
    [books addObject:@"book2"];
    NSLog(@"bookArray1:%@",person.bookArray1);
    NSLog(@"bookArray2:%@",person.bookArray2);
}
```
我们看到，使用strong修饰的person.bookArray1输出是[book1,book2]，而使用copy修饰的person.bookArray2输出是[book1]。这下可以看出来区别了吧。

> 备注：使用strong，则person.bookArray1与可变数组books **指向同一块内存区域** ，books内容改变，导致person.bookArray1的内容改变，因为两者是同一个东西；而使用copy，person.bookArray2在赋值之前，将books内容复制，创建一个 **新的内存区域**，所以两者不是一回事，books的改变不会导致person.bookArray2的改变。

总结起来，其实@property的参数还有很多，主要分为四类：

* 1、内存管理
 
> retain ： release旧值，retain新值
assign ：直接复制（缺省值，适用于非OC对象类型）
copy ： release旧值，copy新值


![retain assign copy具体实现](https://ws3.sinaimg.cn/large/006tKfTcly1fs3uz91q7tj30te0l6dil.jpg)
* 2、读写属性，是否要生成set方法

>  readaonly ：只读，只生成getter的声明和实现
readwrite ：可读可写，生成setter和getter的生命和实现（缺省值）

* 3、多线程管理

> nonatomic ：性能高，不加锁，线程不安全（建议使用，开发常写）
atomic：性能低，加锁，线程安全（缺省值）

* 4、setter和getter方法的名称

> @property (setter = setXxx: ,getter = xxx) int weight;
一般使用在BOOL类型的成员变量 getter = isXxx

* [Objective-C属性修饰符strong和copy的区别](https://segmentfault.com/a/1190000002520583)

#### 2.7 Manually reference Counting和Automatic Reference Counting




** 1.MRC 手动管理内存(Manual Reference Counting)**

先看一个例子：

NSNumber对象myInt被设置为整数100，并且程序输出显示它的初始计数为1。然后，使用addObject：方法将该对象添加到数据myArr中。引用计数变成2.将对象添加到任何类型的集合都会使该对象的引用次数增加。这意味着，如果随后释放了添加的对象，那么数组中仍然保存这该对象的有效引用，对象不会释放。

接下来，将myInt赋值给变量myInt2.要注意这个操作并没有使myInt对象的引用次数增加，这会给以后造成潜在的麻烦。例如，如果对myInt的引用次数减少到0，并且它占用的空间被释放，那么myInt2将拥有无效的引用对象（将myInt赋值给myInt2的操作并没有复制实际的对象，只是指向myInt在内存中位置的指针）。

然后通过代码再来直观的感受一下。
``` objectivec
int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // 只要创建一个对象默认引用计数器的值就是1
        Person *p = [[Person alloc] init];
        NSLog(@"retainCount = %lu", [p retainCount]); // 1

        // 只要给对象发送一个retain消息, 对象的引用计数器就会+1
        [p retain];

        NSLog(@"retainCount = %lu", [p retainCount]); // 2
        // 通过指针变量p,给p指向的对象发送一条release消息
        // 只要对象接收到release消息, 引用计数器就会-1
        // 只要一个对象的引用计数器为0, 系统就会释放对象

        [p release];
        // 需要注意的是: release并不代表销毁\回收对象, 仅仅是计数器-1
        NSLog(@"retainCount = %lu", [p retainCount]); // 1

        [p release]; // 0
        NSLog(@"--------");
    }
//    [p setAge:20];    // 此时对象已经被释放
    return 0;
}
```

**MRC内存原则**
```
1.需要引用时，+1；不需要引用了，-1；

2.谁创建，谁release；

3.谁retain，谁release；

4.只要调用了alloc，必须有release(autorelease)

5.成员变量的set方法中需要注意的：基本数据不用管，对象数据需要注意。
```
**2.自动释放池（Automatic Reference Counting）**
autorelease是一种支持引用计数的内存管理方式，只要给对象发送一条autorelease消息，会将对象放到一个自动释放池中，当自动释放池被销毁时，会对池子里面的所有对象做一次release操作


*  使用autorelease有什么好处呢

不用再关心对象释放的时间
不用再关心什么时候调用release


*  autorelease的原理实质上是什么？

autorelease实际上只是把对release的调用延迟了，对于每一个autorelease，系统只是把该对象放入了当前的autorelease pool中,当该pool被释放时,该pool中的所有对象会被调用release。

* [OC知识--彻底理解内存管理(MRC、ARC)](http://www.jianshu.com/p/48665652e4e4)

* [OC基本语法总结（四）——内存管理MRC和ARC](http://www.tuluobo.com/2016/03/11/550.html)

#### 2.8 auto、const和volatile
待补充...

#### 2.9 alloc, init, dealloc, release,new ,retain

简单地说，alloc分配内存空间，init对该对象进行初始化，这些方法若没有重写方法则默认继承自父类。
通常来讲，new =  alloc + init 
Objective-C的对象在使用完成之后不会自动销毁，需要执行dealloc来释放空间（销毁），否则内存泄露。下面是一个简单的例子。
``` objectivec
ClassA *obj1 = [[ClassA alloc] init];

[obj1 hello]; //输出hello

[obj1 dealloc];
```

Objective-C采用了引用计数(ref count或者retain count)。对象的内部保存一个数字，表示被引用的次数。例如，某个对象被两个指针所指向（引用）那么它的retain count为2。需要销毁对象的时候，不直接调用dealloc，而是调用release。release会让retain count减1，只有retain count等于0，系统才会调用dealloc真正销毁这个对象。

Objective-C指针赋值时，retain count不会自动增加，需要手动retain。

``` objectivec

ClassA *obj1 = [[ClassA alloc] init]; //retain count = 1
ClassA *obj2 = obj1; //retain count = 1
[obj2 retain]; //retain count = 2
[obj1 hello]; //输出hello
[obj1 release]; //retain count = 2 – 1 = 1
[obj2 hello]; //输出hello
[obj2 release]; //retain count = 0，对象被销毁
```


![alloc & init](https://ws4.sinaimg.cn/large/006tKfTcly1fs3uzcuz5dj30k00lztfo.jpg)

[Objective-C 内存管理——你需要知道的一切](https://segmentfault.com/a/1190000004943276)

[Objective-C内存管理教程和原理剖析（一）](http://blog.jobbole.com/66197/)

#### 2.10 文件操作
待补充...
#### 2.11 分类和协议
待补充...
#### 2.12 NSString， NSNumber，NSArray，NSDictionary， NSSet 类的主要方法
待补充...

#### 2.13 Cocoa 
Cocoa是一种支持应用程序提供丰富用户体验的框架，它实际上由两个框架组成：
* Foundation框架
* Application Kit (或AppKit)框架  :  提供与窗口、按钮、列表等相关的类。
* core Data

![Cocoa框架服务](https://ws2.sinaimg.cn/large/006tKfTcly1fs3uzf43idj30fk0fi0tz.jpg)

补充：

内核以设备驱动程序的形式提供与硬件的底层通信。它负责管理系统资源，包括调度要执行的程序、管理内存和电源，以及执行基本的I/O操作。


核心服务提供的支持比它上面层次更加底层或更加“核心”。例如，这里提供对集合、网络、 调试、文件管理、文件夹、内存管理、线程、时间和电源的管理。
应用程序服务层包含对打印和图形呈现的支持，包括Quartz、OpenGL和Quicktime。

Cocoa层直接位于应用程序层之下。正如图所示，Cocoa包括Foundation禾口AppKit框架0 Foundation框架提供的类用于处理集合、字符串、内存管理、文件系统‘存档等。AppKit框架提供的类用于管理视图、窗口、文档和让Mac OS X闻名于世的多信息用户界面。

> Cocoa框架用于Mac OS X桌面与笔记本电脑的应用程序开发，而Cocoa Touch框架用于 iPhone与ipod Touch的应用程序开发。
Cocoa和Cocoa Touch都有Foundation框架。然而在Cocoa Touch下，UIKit代替了 AppKit框架，以便为很多相同类型的对象提供支持，比如窗口、视图、按钮、文本域等。另外，Cocoa Touch还提供使用加速器（它与GPS和WiFi信号一样都能跟綜你的位置）的类和触摸式界面， 并且去掉了不需要的类，比如支持打印的类。


# 4.


前文也提到，本文提到的每一个点都可以单独行文，这里只是做一个浅显的介绍，后期会结合**示例代码**做一些更加深入探讨。

欢迎指正批评与交流，本博客将长期更新维护。


 [个人主页](http://www.hellogod.cn)


未完待续...

