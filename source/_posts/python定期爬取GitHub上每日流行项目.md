---
title: python定期爬取GitHub上每日流行项目
date: 2017-06-26 18:12:27
tags: 
- python 
- 爬虫 
- Github

updated: 2017-09-27 15:40:21
category: 开发笔记
---
 

介绍一个在GitHub上看到的通用的python爬虫，难度不大，是一个蛮好玩的点，顺便总结一下python爬虫的一些需要注意的点。
先上链接：[github源码](https://github.com/LJ147/github-trending)
#  项目简介

大家可以看一下这个网站 [https://github.com/trending](https://github.com/trending)
![](https://ws1.sinaimg.cn/large/006tKfTcly1fs3uxz5jgxj30yg0lbtcz.jpg)

<!-- more -->

随时关注最新的技术动向，永远是一个程序员应该做到的，但我们不能做到每天去查看，于是就诞生了这个repo（更正为原作者写了这个repo），我们将爬虫挂在Linux服务器上，定期爬取并且推送到自己的repo上，只要有时间，就可以看到之前的所有热门项目。

![](https://ws4.sinaimg.cn/large/006tKfTcly1fs3uy0539oj30yg0nddkg.jpg)

顺便说一句这样是不是还可以刷一波GitHub commit

代码po在了最后面


#  关于python的私人总结
**使用python开发爬虫的时候需要注意哪些？**

##   区分python版本
>  python 2.x 3.x 差别很大，如果遇到就编译通不过，及早意识到进行修正还好，若是语法差别不大却没有意识到，有时候会给自己惹来很大的麻烦

##  关注几种易于混淆的数据类型
* Tuples
* Lists
* Dictionary
* Json
需要格外关注这几种类型之间的转换，我们知道python是一种弱数据类型语言，但不代表着它的数据类型可以混用，反而，正因为弱化了声明，才让有些操作更加容易出错，这时候我们需要做的，就是仔细阅读文档，熟悉不同的用法。
![Tuples](https://ws4.sinaimg.cn/large/006tKfTcly1fs3uy1hwduj30yg0kjag2.jpg)

![Lists](https://ws1.sinaimg.cn/large/006tKfTcly1fs3uy2fxo0j30yg0nm11x.jpg)

![Dictionary](https://ws2.sinaimg.cn/large/006tKfTcly1fs3uy3dt4cj30yg0qptl5.jpg)

推荐文档：[Tuples, Lists, and Dictionaries](http://sthurlow.com/python/lesson06/)
##  注意合理使用第三方类库
>  python相对于java等语言，最大的优势就在于其具有很大规模的封装良好的类库，可以让我们使用短短的几行代码，实现很多功能。这里列举几个常用的库和框架：

*  virtualenv 创建独立 Python 环境的工具。
* Beautiful Soup 提供一些简单的、python式的函数用来处理导航、搜索、修改分析树等功能 简单的说就是解析网页
* Scrapy 强大的爬虫框架Scrapy
限于篇幅，放几个链接大家自己进去看
[哪些 Python 库让你相见恨晚？](https://www.zhihu.com/question/24590883)
[Python 常用的标准库以及第三方库有哪些？](https://www.zhihu.com/question/20501628)

#   代码

下面是注释版代码，python2.7 用了requests PyQuery等几个类库
代码写的比较明确了，就没有过多注释

```python
  #!/usr/local/bin/python2.7
  # coding:utf-8

import datetime
import codecs
import requests
import os
import time
from pyquery import PyQuery as pq
    #git操作 推送到远程repo
def git_add_commit_push(date, filename):
    cmd_git_add = 'git add .'
    cmd_git_commit = 'git commit -m "{date}"'.format(date=date)
    cmd_git_push = 'git push -u origin master'

    os.system(cmd_git_add)
    os.system(cmd_git_commit)
    os.system(cmd_git_push)


def createMarkdown(date, filename):
    with open(filename, 'w') as f:
        f.write("###" + date + "\n")


def scrape(language, filename):

    HEADERS = {
        'User-Agent'		: 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10.7; rv:11.0) Gecko/20100101 Firefox/11.0',
        'Accept'			: 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8',
        'Accept-Encoding'	: 'gzip,deflate,sdch',
        'Accept-Language'	: 'zh-CN,zh;q=0.8'
    }

    url = 'https://github.com/trending/{language}'.format(language=language)
    r = requests.get(url, headers=HEADERS)
    assert r.status_code == 200
    # print(r.encoding)

    d = pq(r.content)
    items = d('ol.repo-list li')

    # codecs to solve the problem utf-8 codec like chinese
    with codecs.open(filename, "a", "utf-8") as f:
        f.write('\n##{language}\n'.format(language=language))

        for item in items:
            i = pq(item)
            title = i("h3 a").text()
            owner = i("span.prefix").text()
            description = i("p.col-9").text()
            url = i("h3 a").attr("href")
            url = "https://github.com" + url
            # ownerImg = i("p.repo-list-meta a img").attr("src")
            # print(ownerImg)
            f.write(u"* [{title}]({url}):{description}\n".format(title=title, url=url, description=description))
    #定时爬取对应语言的并写入到markdown文本中
def job():
    strdate = datetime.datetime.now().strftime('%Y-%m-%d')
    filename = '{date}.md'.format(date=strdate)
    # create markdown file
    createMarkdown(strdate, filename)
    # write markdown
    scrape('python', filename)
    scrape('swift', filename)
    scrape('javascript', filename)
    scrape('go', filename)
    scrape('Objective-C', filename)
    scrape('Java', filename)
    scrape('C++', filename)
    scrape('C#', filename)

    # git add commit push
    git_add_commit_push(strdate, filename)
    #主函数
if __name__ == '__main__':
    while True:
        job()
        time.sleep(12 * 60 * 60)
```

#  扩展及埋坑 下集预告

这里分享几个python相关的重要链接，看了一定会有收获（尤其是前两者），而且很大，没效果你回来打我（匿

下面准备把oschina一个类似的东西一块爬一下，push到repo里

接下来准备写一个爬取学校教务系统验证码并训练识别的文章，敬请期待。

* 资源汇总：[python框架、类库、软件和资源汇总repo](https://github.com/vinta/awesome-python)
*  爬虫集合：[各种python爬虫集合 ](https://github.com/facert/awesome-spider)
* python爬虫教程: [静觅 崔庆才的个人博客](http://cuiqingcai.com/1052.html)
* python学习路线: [知乎：如何入门 Python 爬虫?](https://www.zhihu.com/question/20899988)
* 原repo go语言版本: [github-trending](https://github.com/josephyzhou/github-trending)
* python版本: [github-trending](https://github.com/bonfy/github-trending)


欢迎各位在评论区批评指正  若是觉得码字不易，也可以赞赏啊Orz

[个人主页](http://www.hellogod.cn)


