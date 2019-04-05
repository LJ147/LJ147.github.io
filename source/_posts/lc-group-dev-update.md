---
title: 一时打卡网站公告区
tags:
  - LeetCode
  - 打卡
keyword:
  - LeetCode
date: 2019-04-03 12:23:20
updated: 2019-04-03 12:23:20
categories: 日常
description: https://group.hellogod.cn 更新日志，常见 FQA
---

# 1.更新日志

- 添加小组统计数据，新增 datatable 表格(排序、搜索、分页)

时间： 2019-04-05 12:21:28

<center>打卡数据</center>



![image-20190405122124911](https://ws3.sinaimg.cn/large/006tNc79gy1g1rn2nk16hj31r50u0gpa.jpg)



<center>表格支持排序、分页、搜索</center>

![img](https://ws2.sinaimg.cn/large/006tNc79gy1g1rn58bdk6j31gk0u04ea.jpg)



<!-- more -->

- 不再收录长时间未打卡的用户 

时间：2019-04-03 12:27:49

除名规则： 加入排行榜十天以上，且十天内打卡次数为零。SQL 如下：

```
UPDATE Member m
JOIN (
  SELECT
    address,
    checkdays,
    cnt 
  FROM
    (
    SELECT
      address,
      ( cnt - uncheck ) AS checkdays,
      cnt 
    FROM
      ( SELECT address, count( * ) AS cnt, sum( checked ) AS uncheck FROM CheckDayInfo GROUP BY address ORDER BY cnt DESC ) a 
    WHERE
      cnt > 10 
    ) b 
  WHERE
    checkdays = 0 
  ) c 
  SET m.STATUS = 1 
WHERE
  url = c.address
```

![image-20190405122353852](https://ws2.sinaimg.cn/large/006tNc79gy1g1rn58bdk6j31gk0u04ea.jpg)



<!-- more -->

- 将长期未打卡的用户除名 

时间：2019-04-03 12:27:49

除名规则： 加入排行榜十天以上，且十天内打卡次数为零。SQL 如下：

```mysql
UPDATE Member m
JOIN (
	SELECT
		address,
		checkdays,
		cnt 
	FROM
		(
		SELECT
			address,
			( cnt - uncheck ) AS checkdays,
			cnt 
		FROM
			( SELECT address, count( * ) AS cnt, sum( checked ) AS uncheck FROM CheckDayInfo GROUP BY address ORDER BY cnt DESC ) a 
		WHERE
			cnt > 10 
		) b 
	WHERE
		checkdays = 0 
	) c 
	SET m.STATUS = 1 
WHERE
	url = c.address
```



# 2.常见问题

## 2.1 排行榜规则是什么？

三个指标：是否打卡、今日刷题数量、总刷题数量

其中今日刷题，只计入之前未刷过的题。新用户加入的时候，由于前一天的刷题总数无从获取，故今日刷题 = 总刷题。



## 2.2 这个项目如何产生的？



参见之前的文章：  [一时打卡小玩意](https://hellogod.cn/2019-03-03/leetcode-group-website/)



##  2.3 这个项目是如何开发的？



你可以在我们的 [trello](https://trello.com/b/us9CBVcv/%E4%B8%80%E6%97%B6%E6%89%93%E5%8D%A1) 看板了解更多。




