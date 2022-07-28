---
title: "CentOs 7 编译安装最新版 Git"
date: 2022-07-28T10:16:26+08:00
lastmod: 2022-07-28T10:16:26+08:00
draft: false
description: "记录下在 CentOs 7 下编译安装最新版 Git 的过程"
tags: ["Git"]
categories: ["工具"]
series: ["codding"]
resources:
- name: featured-image
  src: git.jpg
- name: featured-image-preview
  src: git.jpg
---

记录下在 CentOs 7 下编译安装最新版 Git 的过程， 其他系统可以 Linux 系统通用。

## 查看 Git 版本
```
root@iZbp18tsw8ozfwv9w47ablZ:~# git version
git version 2.25.1
```

## 下载源码，进行编译

到github上下载源码，[下载地址](https://github.com/git/git/tags)

尽量不要选择rc版本

尽量选择最新版本低 3-4 个版本的

我这里选择 `2.37.1` 这个版本，复制右下角 `tar.gz` 的链接地址

{{< image src="git-version.png" caption="Lighthouse (`git-version`)" >}}

或者使用命令行方式进行下载 ，我使用的命令行方式下载的。

下载到本地服务器后，就可以进行源码安装了。

依次执行如下几条指令：

```shell
wget https://github.com/git/git/archive/refs/tags/v2.37.1.tar.gz

tar -xvf v2.37.1.tar.gz # 解压安装包

cd v2.37.1 # 切换到源码目录

./configure --prefix=/usr/local/git #生成配置文件

make # 编译

make install # 安装

echo "export PATH=$PATH:/usr/local/git/bin" >> /etc/bashrc  # 配置环境变量

source /etc/bashrc # 更新环境变量
```


如很顺利没有报错，那恭喜你最新的 Git-2.37.1 的版本基本就算安装成功了。 如果出错那一般肯定都是依赖包缺失才导致安装失败，那就 谷歌 或者 度娘 解决报错问题吧。

现在可以查看安装的最新版本了，执行如下：

```
root@iZbp18tsw8ozfwv9w47ablZ:~# git version
git version 2.37.1
```
