---
title: "加速镜像（2022/06/07更新）"
date: 2020-09-17 17:20:48
lastmod: 2022-06-07T10:16:26+08:00
draft: false
description: "由于众所周知的原因，很多软件默认的都是国外的镜像，导致在国内访问速度缓慢，所以有必要切换到国内的镜像以达到加速的目的，特记录下日常所用到的加速镜像。"
tags: ["Composer", "Yarn", "npm", "ubuntu"]
categories: ["PHP", "Nodejs"]
series: ["codding"]
toc: true
resources:
- name: featured-image
  src: composer.jpg
- name: featured-image-preview
  src: composer.jpg
---

# 加速镜像

由于众所周知的原因，很多软件默认的都是国外的镜像，导致在国内访问速度缓慢，所以有必要切换到国内的镜像以达到加速的目的，特记录下日常所用到的加速镜像。

## composer 加速
```composer
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
```

## npm 加速

http://npm.taobao.org 和 http://registry.npm.taobao.org 将在 2022.06.30 号正式下线和停止 DNS 解析。
新域名为 npmmirror.com, 相关服务域名切换规则请参考：
```
http://npm.taobao.org => http://npmmirror.com
http://registry.npm.taobao.org => http://registry.npmmirror.com
```

```npm
npm config set registry http://registry.npmmirror.com
```

## yarn 加速
```yarn
yarn config set registryhttp://registry.npmmirror.com
```

## cnpm 加速
```cnpm
npm install -g cnpm --registry=http://registry.npmmirror.com
```

## golang 加速镜像
可用镜像：
```
https://goproxy.cn
https://goproxy.io
https://mirrors.aliyun.com/goproxy/
```
设置

```
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct
```

## 阿里云 Ubuntu 镜像
首先，编辑我们的 /etc/apt/sources.list 文件（此处使用 Vim ，你也可以选用其他编辑器）：
```
$ vim /etc/apt/sources.list
```
替换默认的 `http://archive.ubuntu.com/` 为 `mirrors.aliyun.com`

Vim 替换指令为：
```
:%s/archive.ubuntu.com/mirrors.aliyun.com/g
:%s/security.ubuntu.com/mirrors.aliyun.com/g
```
然后使用 :wq 保存并退出。

接下来，我们需要刷新软件源：
```
$ apt update
$ apt upgrade
```
### Ubuntu 14.04.5 LTS 配置如下
```
deb https://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
deb https://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse

## Not recommended
# deb https://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
# deb-src https://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
```

### ubuntu 16.04 配置如下
```
deb http://mirrors.aliyun.com/ubuntu/ xenial main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main

deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main

deb http://mirrors.aliyun.com/ubuntu/ xenial universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates universe

deb http://mirrors.aliyun.com/ubuntu/ xenial-security main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main
deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security universe

```
### ubuntu 18.04(bionic) 配置如下
```
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse

```
### ubuntu 20.04(focal) 配置如下
```
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse

```

## 相关链接
1. [阿里云 镜像](https://developer.aliyun.com/mirror/?spm=a2c6h.265751.J_5404914170.29.728e759bS5Tzwy)
2. [Ubuntu 镜像](https://developer.aliyun.com/mirror/ubuntu)
3. [阿里云 Composer 全量镜像](https://developer.aliyun.com/composer)


