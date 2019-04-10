---
title: LeetCode 题解 - 0
tags:
  - LeetCode
keyword:
  - 题解
date: 2019-04-10 04:02:43
updated: 2019-04-10 04:02:43
categories: LeetCode
description: 记录题解，加深印象。

---

近期断断续续在刷题，个人习惯问题，感觉到大致思路之后就先去看答案了， 也不知时好时坏，还是有几分心虚，加上之前一直说要写刷题笔记，所以这里记录一下自己对于答案的理解，以及遇到的一些问题，方便日后回顾。



<!-- more -->

[636. Exclusive Time of Functions](https://leetcode.com/problems/exclusive-time-of-functions/)



On a single threaded CPU, we execute some functions.  Each function has a unique id between `0` and `N-1`.

We store logs in timestamp order that describe when a function is entered or exited.

Each log is a string with this format: `"{function_id}:{"start" | "end"}:{timestamp}"`.  For example, `"0:start:3"` means the function with id `0` started at the beginning of timestamp `3`.  `"1:end:2"` means the function with id `1` ended at the end of timestamp `2`.

A function's *exclusive time* is the number of units of time spent in this function.  Note that this does not include any recursive calls to child functions.

Return the exclusive time of each function, sorted by their function id.

 

**Example 1:**

**![img](https://assets.leetcode.com/uploads/2019/04/05/diag1b.png)**

```
Input:
n = 2
logs = ["0:start:0","1:start:2","1:end:5","0:end:6"]
Output: [3, 4]
Explanation:
Function 0 starts at the beginning of time 0, then it executes 2 units of time and reaches the end of time 1.
Now function 1 starts at the beginning of time 2, executes 4 units of time and ends at time 5.
Function 0 is running again at the beginning of time 6, and also ends at the end of time 6, thus executing for 1 unit of time. 
So function 0 spends 2 + 1 = 3 units of total time executing, and function 1 spends 4 units of total time executing.
```



题意：求解单 CPU 机器函数运行时间

解题思路：这种问题很自然想到要用栈，然后就是优化空间复杂度，这里是使用一个 prev 存储。



```java
public class Solution {
    public int[] exclusiveTime(int n, List < String > logs) {
        Stack <Integer> stack = new Stack <> ();
        int[] res = new int[n];
        String[] s = logs.get(0).split(":");
        stack.push(Integer.parseInt(s[0]));
        int i = 1, prev = Integer.parseInt(s[2]);
        while (i < logs.size()) {
            s = logs.get(i).split(":");
            if (s[1].equals("start")) {
                if (!stack.isEmpty())
                    res[stack.peek()] += Integer.parseInt(s[2]) - prev;
                stack.push(Integer.parseInt(s[0]));
                prev = Integer.parseInt(s[2]);
            } else {
                res[stack.peek()] += Integer.parseInt(s[2]) - prev + 1;
                stack.pop();
                prev = Integer.parseInt(s[2]) + 1;
            }
            i++;
        }
        return res;
    }
}
```

