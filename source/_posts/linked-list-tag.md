---
title: 链表高频算法题及其解法
tags:
  - 链表
  - 面试
categories: 算法
date: 2018-12-09 03:24:18
updated: 2018-12-09 03:24:18
description: 链表常见题目，代码语言统一为Python，整理在一起方便回顾。
keyword:
---


整理之后想起来LeetCode自己家出过一个类似的汇总Orz，大概是最近真的太闲了，想整理下刷过的题目，老实讲之前刷的题并不多。 LeetCode领扣的公众号做得很好，有时间回去翻翻看。

- [面试专题 | 链表操作](https://mp.weixin.qq.com/s/rx4fD0fHtG8oIiZ-b05u9A)
- [专题 | 链表类算法精析（下）](https://mp.weixin.qq.com/s/mXqz7DqgbnLNMGoexGdgyQ)

<!-- more -->


# 单链表反转

## 题目描述

输入一个链表，反转链表后，输出新链表的表头。

解法：

``` python
# -*- coding:utf-8 -*-
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
class Solution:
    # 返回ListNode
    def ReverseList(self, pHead):
        if pHead == None:
            return pHead
        pre = next = None
        while pHead != None:
            next = pHead.next
            pHead.next = pre
            pre = pHead
            pHead = next
        return pre
```

# 链表中环的检测

## 题目描述

[141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/)
Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.

## 题解

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        # Given an empty list
        if not head:
            return False
        
        # Initialize two pointers
        slow = head
        fast = head.next
        while fast and slow:
            # Two pointers would finally come to the same node 
            # when there is a cycle
            if fast == slow:
                return True
            if fast.next:
                fast = fast.next.next
                slow = slow.next
            # fast.next is None means that there is no cycle
            else:
                break
            
        return False
```
# 有序链表合并

## 题目描述

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4

## 题解


``` python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        returnNode = ListNode(-1)
        headNode = returnNode
        
        while l1 != None and l2 != None:
            if l1.val <= l2.val:
                returnNode.next = l1
                l1 = l1.next
            else:
                returnNode.next = l2
                l2 = l2.next
            returnNode = returnNode.next
        
        if l1 == None:
            returnNode.next = l2
        elif l2 == None:
            returnNode.next = l1
            
        return headNode.next
```
# 删除链表中倒数第n个节点
## 题目描述

[19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

Given a linked list, remove the n-th node from the end of list and return its head.

Example:

Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
## 题解


```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        dummy = ListNode(0)
        dummy.next = head
        
        l = r = dummy

        for _ in range(n+1):
            r = r.next
        
        while r != None:
            r = r.next
            l = l.next
            
  
        l.next = l.next.next
        
        return dummy.next
        
        
```

# 求链表的中间节点

## 题目描述

[876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/description/)


Given a non-empty, singly linked list with head node head, return a middle node of linked list.

If there are two middle nodes, return the second middle node.


## 题解


``` python 
class Solution(object):
    def middleNode(self, head):
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        return slow
```


