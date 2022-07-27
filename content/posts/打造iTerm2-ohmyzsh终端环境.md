---
title: "打造 iTerm2 + Oh My Zsh 终端环境"
date: 2020-11-30T11:47:18+08:00
lastmod: 2021-09-16T10:16:26+08:00
draft: false
tags: ["iTerm2", "zsh", "抖音"]
categories: ["开发工具"]
featuredImage: "https://cdn.jsdelivr.net/gh/ibyond/CDN/posts/20201130/ohmyzsh.jpg"
featuredImagePreview: "https://cdn.jsdelivr.net/gh/ibyond/CDN/posts/20201130/ohmyzsh.jpg"
description: 记录下如何一步一步的打造属于自己的 Terminal，你如果想和我一样，直接 cv 大法 就可以搞一套一样的。
---
<!--more-->

## 安装 zsh
### mac
```bash
$ brew install zsh
```
### ubuntu
```bash
$ apt install zsh
```

## 安装 oh my zsh

选择一种方式按照即可

```
$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
$ sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

## 切换主题
选择合适的主题

具体效果可以参考： [ohmyzsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)，里面有官方自带的主题的效果图展示。

这里我选择 `ys` 主题

{{< image src="https://cdn.jsdelivr.net/gh/ibyond/CDN/posts/20201130/theme-ys.jpg" >}}

```bash
$ vim ./zshrc
# 在文件里找到 ZSH_THEME 添加
ZSH_THEME="ys"

# 去掉 @ 主机名 
$ cd ~/.oh-my-zsh/themes
$ cp ys.zsh-theme ou.zsh-theme
$ vim ou.zsh-theme

# 在文件里找到 PROMPT , 去掉以下两行：
%{$fg[white]%}@ \
%{$fg[green]%}%m \

```

## 安装 zsh 插件

### Zsh 命令自动补全插件 zsh-autosuggestions

```bash
$ git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

$ vim ./zshrc
# 在文件里找到 plugins 添加
plugins=(zsh-autosuggestions)

# 保存执行生效
$ source ~/.zshrc
```

### 语法高亮 zsh-syntax-highlighting
```bash
$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

$ vim ./zshrc
# 在文件里找到 plugins 添加
plugins=( zsh-syntax-highlighting)

# 保存执行生效
$ source ~/.zshrc
```

### autojump
```bash
# ------ mac -----
$ brew install autojump
$ vim ~/.zshrc
# 在文件里找到 plugins 添加
plugins=(autojump)

# 在文件末尾添加
[[ -s $(brew --prefix)/etc/profile.d/autojump.sh ]] && . $(brew --prefix)/etc/profile.d/autojump.sh

$ source $ZSH/oh-my-zsh.sh
# 最后
$ source ~/.zshrc

# ------ linux -----
$ git clone git://github.com/joelthelion/autojump.git
$ cd autojump
$ ./install.py
$ vim ~/.zshrc
# 在文件里找到plugins，添加
plugins=(autojump)
# 在文件末尾添加
[[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && . ~/.autojump/etc/profile.d/autojump.sh
$ source ~/.zshrc

```

## 安装字体
```bash
# git clone
$ git clone https://github.com/powerline/fonts.git --depth=1
# install
$ cd fonts
$ ./install.sh
# clean-up a bit
$ cd ..
$ rm -rf fonts
```

## 更新

```bash
$ omz update
```

## 卸载
```bash
$ uninstall_oh_my_zsh
```

## 参考链接

1. https://juejin.cn/post/6844904178075058189

2. https://juejin.cn/post/6844903939121348616