---
title: "Git 常用命令速查"
date: 2022-07-29T10:16:26+08:00
lastmod: 2022-07-29T10:16:26+08:00
draft: false
description: "Git 常用命令，备忘速查"
tags: ["Git"]
categories: ["工具"]
series: ["codding"]
resources:
- name: featured-image
  src: git-command.png
- name: featured-image-preview
  src: git-command.png
---
Git 常用命令，备忘速查
git version 2.37.1

> 转载：[晓飞](https://learnku.com/blog/Longfei-Yan) 的 [Git速查表](https://learnku.com/articles/68324)

## 文档说明
1. `<>` 表示【需替换的项】

2. `[]` 表示【非必填项】

3. `|` 表示【或】

`工作树`（工作区），`索引`（暂存区），`Git` 目录（HEAD） 三词含义参照 Git 官网

## 初始配置
```shell
git config --global user.name [<username>] 配置用户名

git config --global user.email [<email>] 配置邮箱

git config --global core.editor [<vim>] 配置编辑器
```


## 创建项目
```shell
git clone <options> 克隆远程仓库

git init [project] 初始化本地项目
```


## 添加
```shell
git add <file> 添加文件到暂存区

git commit -m <commit notes> 将暂存区的内容提交到 HEAD， 例子：git commit -m "备注"

git commit -am <commit notes> 将 add 和 commit 合并操作

git commit --amend -m <commit notes> 将 add 和 commit 合并操作且合并到上次 commit

git add -A 提交更改到暂存区
```


## 显示
```shell
git status 显示状态

git diff [HEAD] 显示差异

git log 显示日志

git show <commit> 显示某个 commit 的详细内容

git blame <file> 显示文件每行的 commit 信息
```


## 撤回
```shell
git restore <file> 撤回工作区的修改

git restore --staged <file> 将已提交到暂存区的修改撤回工作区

git reset [--mixed] <commit> 将当前版本撤回到某个 commit，保留工作区的修改

git reset --soft <commit> 将当前版本撤回到某个 commit, 保留工作区和暂存区的修改

git reset --hard <commit> 将当前版本撤回到某一个 commit，不保留工作区的修改

git reset --merge 取消合并

git rm <file> 将文件从工作区和暂存区删除

git mv <file> 将文件从工作区和暂存区移动或改名

git clean -df 从工作区删除未跟踪的文件
```


## 分支
```shell
git branch [--list] 显示所有分支

git branch -a 显示远程分支

git branch <branch> 创建分支

git branch -d|-D <branch> 删除分支

git branch -m <newbranch> 重命名当前分支

git switch <branch> 切换到已有分支

git switch -c <branch> 创建并切换分支

git merge <branch> 将某个分支合并到当前分支

git tag <tagname> 给当前分支打标签

git stash 将工作区的更改存储到脏工作目录中

git stash apply 将脏工作目录中的数据恢复到工作区（不会删除脏工作目录保存的数据）

git stash drop 将脏工作目录中的数据删除

git stash pop 将脏工作目录中的数据恢复工作区并删除脏数据
```


## 远程
```shell
git remote [-v] 显示远程库

git remote show <origin> 显示某个远程库的信息

git remote add <origin> <url> 添加远程库链接

git remote rm <origin> 删除远程库链接

git remote rename <oldname> <newname> 重命名远程库

git pull [<origin><branch>] 拉取远程库到本地库

git push [-u <origin> <master>] 将本地库推送到远程库

git push origin --delete <branch>|git push origin :crazy-experiment 删除远程分支

git fetch 从远程库获取到本地库
```


## 帮助
```shell
git help <command> 显示某个命令的详细使用文档

git <command> -h 显示某个命令的使用说明
```


## checkout
该命令职责不明确，不建议使用；
```shell
git checkout <file> 丢弃工作区的修改

git checkout -f 强制丢弃工作区和暂存区的修改

git checkout <branch> 切换分支， 例子：git checkout master

git checkout -b <branch> 创建并切换分支
```

## 实际操作例子

### 切换到主分支，合并其它分支
```shell
git checkout master

git merge new_branches
```

### clone 指定分支的命令
```shell
git clone -b this_branch 地址
```


### 从远程获取代码并合并本地的版本
```shell
git pull
```
git pull 出错

协同开发时，我从远程服务器上 pull 代码的时候，出现以下提示信息：

Automatic merge failed; fix conflicts and then commit the result.

分析：git pull 事实上有两步；

第一步：从远程 pull 指定分支；

第二步：将远程分支与本地分支合并。

错误，出现在第二步。

解决方法：

方法一：如果确定远程分支是我所需要的，本地分支的修改可以舍弃，那就运行以下命令，丢弃本地记录
```shell
git reset --hard origin/master
```

方法二：不能丢弃本地修改，因为其中的某些内容是我们需要的，此时需要对 unmerged 的文件进行手动修改，然后运行以下命令
```shell
git add -A
git commit -m "message"
```

方法三：如果想放弃本次合并，回到合并之前的状态，可以运行以下命令：
```shell
git reset --merge
```

### 测试代码并且回滚

首先，版本标记
```shell
git add -A
git commit -m "版本标记"
```

因为之后，我们会回滚到这个地方。

放弃所有文件的修改：
```shell
git checkout .  
```

检查状态：
```shell
git status
```

发现还有一些新建的文件，那么：
```shell
git clean -f -d
```

（强制清理文件，甚至连文件夹一起清除）
然后再次查看：
```shell
git status
```

发现一切都干干净净。

### 初始化设置

把文件夹内容加入版本管理

```shell
git init
```

设置邮箱

```shell
git config --global user.email "you@example.com"
```

设置用户名

```shell
git config --global user.name "Your Name"
```

### 生成 SSH 公钥
许多 Git 服务器都使用 SSH 公钥进行认证。

如果你想给 Git 服务器提供 SSH 公钥，你自己必须先生成一份。

那如果你不确定自己是否有拥有 SSH 公钥，可以在 Git Bash 中输入
```shell
cd ~/.ssh && ls
```

来查看。

如果你看到 id_rsa 和 id_rsa.pub 这一对文件，证明你的电脑拥有密钥。

.pub 是你的公钥，另一个则是与之对应的私钥。

如果找不到这样的文件或者 .ssh 目录根本不存在，那你需要在 Git Bash 中输入
```shell
ssh-keygen
```

命令来创建它们。

如果你不想使用密码来保护你的密钥，在创建的询问时，留空即可（按下回车直接执行）。

之后，你就可以用万能的记事本，打开 id_rsa.pub ，复制其中的内容，添加到 Git 服务器或者网站中。