+++
image = "img/portfolio/git.png"
showonlyimage = false
date = "2016-11-05T19:57:40+05:30"
title = "Git 使用"
writer = "子适"
draft = false
categories = [ "code" ]
weight = 7
+++

- 分布式版本控制系统

## 本地 Git

### 安装&配置
<!--more-->

- 配置全局用户名和邮箱

```bash
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

- 创建仓库

```bash
$ mkdir learngit
$ cd learngit
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```

### 工作区&暂存区&分支

 ![WX20190111-123155](/Users/cshi/Desktop/学习笔记/assets/WX20190111-123155.png)

### 将文件放入Git仓库(创建和更新)

```bash
$ git add readme.txt
$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```

- 其中， `commit -m ""` 命令说明本次提交的说明。
- 也可以 `add` 多个文件后一次 `commit`
- `add` 命令将文件添加到暂存区
- `commit`命令将暂存区所有内容提交到当前分支

### 查看状态

#### 查看仓库状态

```bash
$ git status

位于分支 master
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git checkout -- <文件>..." 丢弃工作区的改动）

	修改：     readme.txt

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
```

#### 查看文件变化部分

- `diff` 实际是比较工作区和暂存区文件区别

```bash
$ git diff readme.txt

diff --git a/readme.txt b/readme.txt
index d8036c1..013b5bc 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
\ No newline at end of file

```

#### 查看修改历史记录

```bash
$ git log
commit 0ffb5aef54a52be5ac25da0f7eb0d03af12979aa (HEAD -> master)
Author: cshi <847302434@qq.com>
Date:   Fri Jan 11 12:14:47 2019 +0800

    add GPL

commit 71b1f053c4473948862b8481f22bde39d6f5ce12
Author: cshi <847302434@qq.com>
Date:   Fri Jan 11 12:12:29 2019 +0800

    add distributed

commit 89db0a2f66395fa1079b495df2442a3588a88f6a
Author: cshi <847302434@qq.com>
Date:   Fri Jan 11 11:19:14 2019 +0800

    add a readme file

// 简洁版
$ git log --pretty=oneline
```

### 版本回溯

#### 版本表示

- 当前版本——`HEAD`
- 上一个版本——`HEAD^`
- 上100个版本——`HEAD~100`

#### 回溯命令

- `git reset --hard HEAD^`
- 回溯到未来版本——`git reset --hard 1094a`
  - 其中， 1094a 是之前显示的未来版本的 `commit id`,只需写前几位即可
  - 如何找到`commit id`? 可以用 `git reflog` 来查看每一次命令

### 撤销更改

#### 未 add 的错误修改

```bash
$ git checkout -- readme.txt
```

- 命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

  - 一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
  - 一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

  总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。

#### add 了的错误修改

```bash
$ git reset HEAD <file>
```

- 将暂存区的修改回退到工作区
- 然后可以用上面的命令取消工作区的修改

#### commit 了的错误修改

- 使用版本回溯
- 前提是未推送到远程库

### 删除文件

- 删除也是修改

#### 确实删除

1. 手工删除 或者 `rm` 命令删除
2. `git rm file` 删掉
3. `git commit`

#### 删错了

用版本库里的版本替换工作区版本

`git checkout -- text.txt`

- ⚠️： 你恢复的文件只能是最新版本的



## 远程仓库

### 配置SSH

```bash
ssh-keygen -t rsa -C "847302434@qq.com"
```

- 产生 `id_rsa` 和 `id_rsa.pub` 文件在`/Users/cshi/.ssh/`下
- 将 `id_rsa.pub`文件内容填到 GitHub 上。本机就可以向 GitHub 推送

### Push 代码

- 关联——在本地仓库下运行命令

```bash
git remote add origin https://github.com/cshi11/LeetCode.git
```

- 推送
  - 其中，`-u` 是因为第一次推送，远程库是空的，故将当前 `master`分支和远程  `master` 	分支关联

```bash
git push -u origin master
```

- 之后做了修改，本地提交后，可以通过命令将修改推送到 Github

```bash
git push origin master
```

### Clone

```bash
git clone git@github.com:cshi11/LeetCode.git
```

- SSH 比 Https 速度更快，不用每次输入口令

## 分支

### 创建、合并分支

- 创建新分支`dev`,则创建一个新指针 `dev`,指向`master`相同的提交，再把`HEAD` 指向 `dev`,表示当前分支在 `dev`上。
- ![0](/Users/cshi/Desktop/%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/assets/0.png)
- 再提交后，dev 向前走，而 master 不动![0 (/Users/cshi/Desktop/%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/assets/0%20(1).png)](/Users/cshi/Desktop/学习笔记/assets/0 (1).png)

#### 创建并切换分支

```bash
git checkout -b dev
```

等价于

```bash
git branch dev
git checkout dev
```

- 查看当前分支

```bash
git branch
```

#### 合并分支

```bash
git merge dev

```

#### 删除分支

```bash
git branch -d dev

```


