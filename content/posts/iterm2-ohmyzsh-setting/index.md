---
title: "打造 iTerm2 + Oh My Zsh 终端环境"
date: 2020-11-30 16:50:01
lastmod: 2022-06-07T10:16:26+08:00
draft: false
description: "记录下如何一步一步的打造属于自己的 Terminal，你如果想和我一样，直接 cv 大法 就可以搞一套一样的。"
tags: [iTerm2, zsh]
featured_image: "ohmyzsh.jpg"
categories: [工具]
comment : true
disableToC: false
---

记录下如何一步一步的打造属于自己的 Terminal，你如果想和我一样，直接 cv 大法 就可以搞一套一样的。

# 安装 zsh
```
mac: brew install zsh
ubuntu: apt install zsh
```

# 安装 oh my zsh
```
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

# 切换主题 
```
vim ./zshrc
# 在文件里找到 plugins 添加
ZSH_THEME="ys"

# 去掉 @ 主机名 
cd ~/.oh-my-zsh/themes
cp ys.zsh-theme ou.zsh-theme
vim ou.zsh-theme

# 在文件里找到 PROMPT , 去掉以下两行：
%{$fg[white]%}@ \
%{$fg[green]%}%m \

```
# 安装 zsh 插件

## Zsh 命令自动补全插件 zsh-autosuggestions
```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

vim ./zshrc
# 在文件里找到 plugins 添加
plugins=(zsh-autosuggestions)
```

## 语法高亮 zsh-syntax-highlighting
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

vim ./zshrc
# 在文件里找到 plugins 添加
plugins=( zsh-syntax-highlighting)
```
## autojump
```
# ------ mac -----
brew install autojump
vim ~/.zshrc
# 在文件里找到 plugins 添加
plugins=(autojump)

# 在文件末尾添加
[[ -s $(brew --prefix)/etc/profile.d/autojump.sh ]] && . $(brew --prefix)/etc/profile.d/autojump.sh

source $ZSH/oh-my-zsh.sh
# 最后
source ~/.zshrc

# ------ linux -----
git clone git://github.com/joelthelion/autojump.git
cd autojump
./install.py
vim ~/.zshrc
# 在文件里找到plugins，添加
plugins=(autojump)
# 在文件末尾添加
[[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && . ~/.autojump/etc/profile.d/autojump.sh
source ~/.zshrc

```
# 安装字体
```
# git clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
```
# 更新
```
omz update
```
# 卸载
```
uninstall_oh_my_zsh
```
# 参考链接

1. https://juejin.cn/post/6844904178075058189

2. https://juejin.cn/post/6844903939121348616