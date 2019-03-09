---
title: 开发常用工具备忘录
tags:
  - 工具
  - 笔记
  - 开发
categories: 开发笔记
date: 2018-06-13 10:36:02
updated: 2018-06-13 10:36:02
description: 好记性不如烂笔头
keyword: 
---


经常遇到新开一个开发环境的情况，每换一个开发环境就要重新搜一次环境配置，这里整理到一起，一劳永逸。

<!-- more -->

# 本机ssh免密登录远程linux服务器

如果本地之前未生成过密钥，执行 `ssh-keygen -t rsa` ，如果已经生成，则不无需执行该步骤。


`scp /root/.ssh/id_rsa.pub root@10.*.*.**:~/`   #将公钥拷到服务器中

`cat ~/id_rsa.pub >> ~/.ssh/authorized_keys`  #追加公钥到授权key中


`service sshd restart`  #服务器端重启ssh服务




# IntelliJ IDEA快捷键


- 创建main函数（首字母缩写）：  psvm 
![](https://ws2.sinaimg.cn/large/006tNbRwgy1fu3zyuz3lgj30w203cglv.jpg)

> public static void main(String[] args) {
    }

- 输出语句： System.out.println()



![](https://ws4.sinaimg.cn/large/006tNbRwgy1fu400qhcsqj30qq070dh0.jpg)
> sout 

# 国外源换国内源
 
因为网络环境的问题，很多国外的开发资源拉取很慢，所以需要换到国内加快速度。

## pip更换国内源

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



## conda更换国内源

TUNA 还提供了 Anaconda 仓库的镜像，运行以下命令:

```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes
```
即可添加 Anaconda Python 免费仓库。

运行 conda install numpy 测试一下吧。


## homebrew更换国内源

替换现有上游

shell中执行：

```
cd "$(brew --repo)"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git

cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git

brew update
```

# 参考链接

- [清华大学开源软件镜像站](https://mirror.tuna.tsinghua.edu.cn/help/anaconda/)
- [更改pip源至国内镜像，显著提升下载速度](https://blog.csdn.net/lambert310/article/details/52412059)
- [Homebrew 镜像使用帮助](https://mirror.tuna.tsinghua.edu.cn/help/homebrew/)

