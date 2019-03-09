---
title: 今日头条大数据研发实习生
tags:
  - 面试
  - 今日头条
  - 数据平台
categories: 面试
date: 2018-02-13 23:35:17
updated: 2018-02-23 21:56:34
description: 大概就是好事多磨吧
keyword: 
---

先说明下情况，之前确定的入职部门因为re-org去掉了现在的职位，所以把我转到了另外一个部门：数据研发，但是那个部门表示需要重新面试（两轮），所以就有了这一篇文章。


好在有惊无险，顺利通过。



2018-02-23: 正式offer


![](https://ws1.sinaimg.cn/large/006tNbRwly1fv8d05qbz2j30f0054wf2.jpg)

<!-- more -->

# 一面

## 项目经历
依然是针对项目聊了一些相关的技术细节。此处不表。

## 算法
- 实现32进制的加法（要求尽量不采用10进制中转的方法）
- 实现空间复杂度O(1)的单链表反转


``` java

//第一种方法是：非递归方法
/*
struct ListNode {
    int val;
    struct ListNode *next;
    ListNode(int x) :
            val(x), next(NULL) {
    }
};*/
class Solution {
public:
    ListNode* ReverseList(ListNode* pHead) {
         
        if(pHead==NULL) return NULL;//注意程序鲁棒性
         
        ListNode* pNode=pHead;//当前指针
        ListNode* pReverseHead=NULL;//新链表的头指针
        ListNode* pPrev=NULL;//当前指针的前一个结点
         
        while(pNode!=NULL){//当前结点不为空时才执行
            ListNode* pNext=pNode->next;//链断开之前一定要保存断开位置后边的结点
             
            if(pNext==NULL)//当pNext为空时，说明当前结点为尾节点
                pReverseHead=pNode;
  
            pNode->next=pPrev;//指针反转
            pPrev=pNode;
            pNode=pNext;
        }
        return pReverseHead;
    }
}
 
//第二种方法是：递归方法 /*
struct ListNode {
    int val;
    struct ListNode *next;
    ListNode(int x) :
            val(x), next(NULL) {
    }
};*/
class Solution {
public:
    ListNode* ReverseList(ListNode* pHead) {
        //如果链表为空或者链表中只有一个元素
        if(pHead==NULL||pHead->next==NULL) return pHead;
         
        //先反转后面的链表，走到链表的末端结点
        ListNode* pReverseNode=ReverseList(pHead->next);
         
        //再将当前节点设置为后面节点的后续节点
        pHead->next->next=pHead;
        pHead->next=NULL;
         
        return pReverseNode;
         
    }
};
```

# 二面

面完之后大概几分钟，二面面试官出现，leader面，主要是一些宏观层面。

- 为什么不选择读研（来自之前的面试官记录），如何应对因为没有读研带来的知识深度不够的问题？
- 对于Hadoop、Spark等大数据框架是否有了解？
- 自己的学习轨迹是什么样的？（也就是技术栈的变更，这里其实聊了比较多）
- 如何接触到机器学习这个领域的？
- 最近在读什么书？读的时候在关注什么？ 
- 武汉的学校一般管的比较紧，是否有足够的时间实习？


前两面结束，天已经黑透了（差不多17：开始），我也饿了将近两个多小时肚子，加上我在的房间没开空调，到了最后说话的时候甚至都在微微发抖，但是一时也管不了那么多，只想着快点结束。

# 后记

其实这次的重心应该不是面试，而是面试前的一些心态变化。

自己被告知因为更换入职部门并且需要重新面试（也就是之前的offer失效，面试不通过即自动失去机会）的时候，一度很烦。也是这时候才发现自己是个很喜欢走提前量的人，有计划的感觉总是很舒服，加上拿到offer之后确实浪了有几天，一时有些找不回状态。讲道理写到这里其实就是发牢骚了，因为一开始的打算就是在武汉解决好offer的事情，然后回家好好浪，在家安心养生的时候，突然接到面试通知的时候还是有点错愕。

好在一贯的性格就是，什么坏事情，只要睡一觉就好了~

总的来说，很感谢这个过程中的一些小伙伴，包括面试官、`leader`和`HR`，也感谢自己赶紧摆正了心态。

那么接下来，就期待新的旅程吧！


# 参考

- [牛客网](https://www.nowcoder.com/questionTerminal/75e878df47f24fdc9dc3e400ec6058ca)

