---
title: git总结
date: 2023-11-28 09:35:39
tags: Git
categories: 学习
---

![](/images/git.png)

> - Workspace：工作区
> - Index / Stage：暂存区
> - Repository：仓库区（或本地仓库）
> - Remote：远程仓库

# 1. git 配置命令

## 查询配置信息

1. 列出当前配置：`git config --list`;
2. 列出 repository 配置：`git config --local --list`;
3. 列出全局配置：`git config --global --list`;
4. 列出系统配置：`git config --system --list`;

## 第一次使用 git，配置用户信息

1. 配置用户名：`git config --global user.name "your name"`;
2. 配置用户邮箱：`git config --global user.email "youremail@github.com"`;

# 2. 工作区上的操作命令

## 新建仓库

1. 将工作区中的项目文件使用 git 进行管理，即创建一个新的本地仓库：`git init`；
2. 从远程 git 仓库复制项目：`git clone <url>`，如：`git clone git://github.com/wasd/example.git`;克隆项目时如果想定义新的项目名，可以在 clone 命令后指定新的项目名：`git clone git://github.com/wasd/example.git mygit`；

## 提交

1. 提交工作区所有文件到暂存区：`git add .`
2. 提交工作区中指定文件到暂存区：`git add <file1> <file2> ...`;
3. 提交工作区中某个文件夹中所有文件到暂存区：`git add [dir]`;

## 查询信息

1. 查询当前工作区所有文件的状态：`git status`;

# 3.暂存区上的操作命令

## 提交文件到版本库

1. 将暂存区中的文件提交到本地仓库中，即打上新版本：`git commit -m "commit_info"`;
2. 将所有已经使用 git 管理过的文件暂存后一并提交，跳过 add 到暂存区的过程：`git commit -a -m "commit_info"`;
3. 提交文件时，发现漏掉几个文件，或者注释写错了，可以撤销上一次提交：`git commit --amend`;

## 查看信息

1. 比较暂存区与上一版本的差异：`git diff --cached`;
2. 指定文件在暂存区和本地仓库的不同：`git diff <file-name> --cached`;
3. 查看提交历史：`git log`；参数`-p`展开每次提交的内容差异，用`-2`显示最近的两次更新，如`git log -p -2`;

## 分支管理

1. 创建分支：`git branch <branch-name>`，如`git branch testing`；
2. 从当前所处的分支切换到其他分支：`git checkout <branch-name>`，如`git checkout testing`；
3. 新建并切换到新建分支上：`git checkout -b <branch-name>`;
4. 删除分支：`git branch -d <branch-name>`；
5. 将当前分支与指定分支进行合并：`git merge <branch-name>`;
6. 显示本地仓库的所有分支：`git branch`;
7. 查看各个分支最后一个提交对象的信息：`git branch -v`;
8. 查看哪些分支已经合并到当前分支：`git branch --merged`;
9. 查看当前哪些分支还没有合并到当前分支：`git branch --no-merged`;
10. 把远程分支合并到当前分支：`git merge <remote-name>/<branch-name>`，如`git merge origin/serverfix`；如果是单线的历史分支不存在任何需要解决的分歧，只是简单的将 HEAD 指针前移，所以这种合并过程可以称为快进（Fast forward），而如果是历史分支是分叉的，会以当前分叉的两个分支作为两个祖先，创建新的提交对象；如果在合并分支时，遇到合并冲突需要人工解决后，再才能提交；
11. 在远程分支的基础上创建新的本地分支`：git checkout -b <branch-name> <remote-name>/<branch-name>`，如`git checkout -b serverfix origin/serverfix`;
12. 从远程分支 checkout 出来的本地分支，称之为跟踪分支。在跟踪分支上向远程分支上推送内容：`git push`。该命令会自动判断应该向远程仓库中的哪个分支推送数据；在跟踪分支上合并远程分支：`git pull`；
13. 将一个分支里提交的改变移到基底分支上重放一遍：`git rebase <rebase-branch> <branch-name>`，如`git rebase master server`，将特性分支 server 提交的改变在基底分支 master 上重演一遍；使用 rebase 操作最大的好处是像在单个分支上操作的，提交的修改历史也是一根线；如果想把基于一个特性分支上的另一个特性分支变基到其他分支上，可以使用`--onto`操作：`git rebase --onto <rebase-branch> <feature branch> <sub-feature-branch>`，如`git rebase --onto master server client`；使用 rebase 操作应该遵循的原则是：**一旦分支中的提交对象发布到公共仓库，就千万不要对该分支进行 rebase 操作**；

# 5.本地仓库上的操作

1. 查看本地仓库关联的远程仓库：`git remote`；在克隆完每个远程仓库后，远程仓库默认为`origin`;加上`-v`的参数后，会显示远程仓库的`url`地址；
2. 添加远程仓库，一般会取一个简短的别名：`git remote add [remote-name] [url]`，比如：`git remote add example git://github.com/example/example.git`;
3. 从远程仓库中抓取本地仓库中没有的更新：`git fetch [remote-name]`，如`git fetch origin`;使用 fetch 只是将远端数据拉到本地仓库，并不自动合并到当前工作分支，只能人工合并。如果设置了某个分支关联到远程仓库的某个分支的话，可以使用`git pull`来拉去远程分支的数据，然后将远端分支自动合并到本地仓库中的当前分支；
4. 将本地仓库某分支推送到远程仓库上：`git push [remote-name] [branch-name]`，如`git push origin master`；如果想将本地分支推送到远程仓库的不同名分支：`git push <remote-name> <local-branch>:<remote-branch>`，如`git push origin serverfix:awesomebranch`;如果想删除远程分支：`git push [romote-name] :<remote-branch>`，如`git push origin :serverfix`。这里省略了本地分支，也就相当于将空白内容推送给远程分支，就等于删掉了远程分支。
5. 查看远程仓库的详细信息：`git remote show origin`；
6. 修改某个远程仓库在本地的简称：`git remote rename [old-name] [new-name]`，如`git remote rename origin org`；
7. 移除远程仓库：`git remote rm [remote-name]`；

# 常用命令

新建仓库`git init`

克隆`git clone <url>`

提交到暂存区`git add .`

提交到本地仓库`git commit -m '描述信息'`

添加远程仓库`git remote add [remote-name] [url]`

拉取`git pull`

推送`git push origin master`

---

参考：https://juejin.cn/post/6844903598522908686
