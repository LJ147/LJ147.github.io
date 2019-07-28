---
title: 开发常用工具备忘录（持续更新）
tags:
  - 工具
  - 笔记
  - 开发
categories: 开发笔记
date: 2018-06-13 10:36:02
updated: 2019-07-28 22:02:42
description: 好记性不如烂笔头
keyword: 
---


经常遇到新开一个开发环境的情况，每换一个开发环境就要重新搜一次环境配置，这里整理到一起，一劳永逸。

<!-- more -->

# 1.本机ssh免密登录远程linux服务器

如果本地之前未生成过密钥，执行 `ssh-keygen -t rsa` ，如果已经生成，则不无需执行该步骤。


`scp /root/.ssh/id_rsa.pub root@10.*.*.**:~/`   #将公钥拷到服务器中

`cat ~/id_rsa.pub >> ~/.ssh/authorized_keys`  #追加公钥到授权key中


`service sshd restart`  #服务器端重启ssh服务




# 2.IntelliJ IDEA快捷键


- 创建main函数（首字母缩写）：  psvm 
![](https://ws2.sinaimg.cn/large/006tNbRwgy1fu3zyuz3lgj30w203cglv.jpg)

> public static void main(String[] args) {
    }

- 输出语句： System.out.println()



![](https://ws4.sinaimg.cn/large/006tNbRwgy1fu400qhcsqj30qq070dh0.jpg)
> sout 

| 快捷键      | 说明             |
| ----------- | ---------------- |
| Command+B   | 跳转到实现       |
| Command + U | 跳转到上层方法   |
| Command + [ | 回到刚刚的位置   |
| Ctrl + H    | 查看接口的实现类 |

# 3.国外源换国内源

因为网络环境的问题，很多国外的开发资源拉取很慢，所以需要换到国内加快速度。

## 4.pip更换国内源

永久修改，一劳永逸：

linux/Mac下，修改 ~/.pip/pip.conf (没有就创建一个：)

```
mkdir ~/.pip
vi ~/.pip/pip.conf
```
修改 index-url至tuna，内容如下：

```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

windows下，直接在user目录中创建一个pip目录，如：C:\Users\xx\pip，新建文件pip.ini，内容如下

```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```


## 5.homebrew更换国内源

替换现有上游

shell中执行：

```
cd "$(brew --repo)"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git

cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git

brew update
```

# 6.vscode-json



vscode-json插件，应用市场可搜，美化、校验，方便又安全。



# 参考链接

- [清华大学开源软件镜像站](https://mirror.tuna.tsinghua.edu.cn/help/anaconda/)
- [更改pip源至国内镜像，显著提升下载速度](https://blog.csdn.net/lambert310/article/details/52412059)
- [Homebrew 镜像使用帮助](https://mirror.tuna.tsinghua.edu.cn/help/homebrew/)

