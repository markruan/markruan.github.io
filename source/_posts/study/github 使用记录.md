---
title: github 使用记录
tag:
  - 采坑
categories:
  - study
---

使用github不是很久，把一些遇到的问题记录下来。

**很简单的几个命令；**
1：找到你要上传的文件夹，右键点击->选择git-bash-here;
2：在弹出的命令窗口输入以下命令
**git add .**
我们知道git add命令是用来添加文件到缓存区的，这里使用 . 表示所有。所有这样就把所有的内容添加进去了
**git commit -m “注释”**
这表示提交到分支
**git push origin master**
把当前分支推送到远程仓库
这样就可以了。
下面再附上git的相关命令：
**Git基本常用命令如下：**

mkdir： XX (创建一个空目录 XX指目录名)

pwd： 显示当前目录的路径。

git init 把当前的目录变成可以管理的git仓库，生成隐藏.git文件。

git add XX 把xx文件添加到暂存区去。

git commit –m “XX” 提交文件 –m 后面的是注释。

git status 查看仓库状态

git diff XX 查看XX文件修改了那些内容

git log 查看历史记录

git reset –hard HEAD^ 或者 git reset –hard HEAD~ 回退到上一个版本

```
                    (如果想回退到100个版本，使用git reset –hard HEAD~100 )
1
```

cat XX 查看XX文件内容

git reflog 查看历史记录的版本号id

git checkout — XX 把XX文件在工作区的修改全部撤销。

git rm XX 删除XX文件

git remote add origin https://github.com/zongyunqingfeng/testgit 关联一个远程库

git push –u(第一次要用-u 以后不需要) origin master 把当前master分支推送到远程库

git clone https://github.com/zongyunqingfeng/testgit 从远程库中克隆

git checkout –b dev 创建dev分支 并切换到dev分支上

git branch 查看当前所有的分支

git checkout master 切换回master分支

git merge dev 在当前的分支上合并dev分支

git branch –d dev 删除dev分支

git branch name 创建分支

git stash 把当前的工作隐藏起来 等以后恢复现场后继续工作

git stash list 查看所有被隐藏的文件列表

git stash apply 恢复被隐藏的文件，但是内容不删除

git stash drop 删除文件

git stash pop 恢复文件的同时 也删除文件

git remote 查看远程库的信息

git remote –v 查看远程库的详细信息

git push origin master Git会把master分支推送到远程库对应的远程分支上



在github上只能删除仓库,却无法删除文件夹或文件, 所以只能通过命令来解决：

首先进入你的master文件夹下, Git Bash Here ,打开命令窗口，以此输入以下命令：

1. $ git --help 帮助命令
2. $ git pull origin master 将远程仓库里面的项目拉下来
3. $ dir 查看有哪些文件夹
4. $ git rm -r --cached target 删除target文件
5. $ git commit -m ‘删除了target’ 提交,添加操作说明