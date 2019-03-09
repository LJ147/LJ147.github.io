---
title: leetcode-Course-Schedule
tags:
  - LeetCode
  - 图
categories: LeetCode
date: 2019-01-21 22:43:43
updated: 2019-01-21 22:43:43
description:
keyword:
---




<!-- more -->

# 第一题

# 第二题

- 链接： [207. Course Schedule](https://leetcode.com/problems/course-schedule/)
- 考点：有向图中环的检测
- 算法：BFS、DFS
- 时间复杂度 
- 空间复杂度
- 速度：99.57% 

```java 
import java.util.*;

class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<Integer>[] from = new ArrayList[numCourses];
        for (int i = 0; i < numCourses; i++) from[i] = new ArrayList();
        int[] to = new int[numCourses];
        boolean[] cur = new boolean[numCourses];
        boolean[] isV = new boolean[numCourses];
        for (int[] pre : prerequisites) {
            from[pre[1]].add(pre[0]);
            to[pre[0]]++;
        }
        // check if circle exists
        for (int i = 0; i < numCourses; i++) {
            if (to[i] == 0 && !isV[i]) {
                if (findCircle(i, from, cur, isV)) {
                    return false;
                }
            }
        }
        // check if all courses are reachable
        for (int i = 0; i < numCourses; i++) {
            if (to[i] != 0 && !isV[i]) return false;
        }
        return true;
    }
    private boolean findCircle(int idx, List<Integer>[] from, boolean[] cur, boolean[] isV) {
        if (isV[idx]) return false;
        if (cur[idx]) return true;
        cur[idx] = true;
        for (int i : from[idx]) {
            if (findCircle(i, from, cur, isV)) {
                return true;
            }
        }
        cur[idx] = false;
        isV[idx] = true;
        return false;
    }
}
```

运行结果：

![](https://ws3.sinaimg.cn/large/006tNc79gy1fzel9qiv4lj312e0cagnh.jpg)

