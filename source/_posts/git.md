---
title: Git
author: zwbiwf
cover: true
---

#1. Linux的命令

- mkdir xxx 新建文件夹


- vi x.txt 新建文件（Visual editor）


	- 输入 i 进入编辑模式


	- ESC + ：+ wq 保存并退出


- cd xxx 进入xxx目录


- cd .. 返回上一级目录


- ls 列出当前文件夹中所有文件

- pwd 显示当前目录


- cat x.txt 显示文件内容


- clear 清屏

- ！q 强制退出
#2.Git指令#
##1.基本指令#

- git config --global user.name "Your Name"     （写用户名）

-  git config --global user.email "email@example.com"     （写邮箱）
 
- git config user.name    （查看配置的姓名）

- git config user.email    （查看配置的邮箱）

- 因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。
 
##2.创建版本库
- git init初始化版本库


-	创建成功会提示 Initialized empty Git repository in c:/Users/熊键/Desktop/0725git/.git/


-	没有初始化执行git命令，会提示fatal: Not a git repository (or any of the parent directories): .git


-	你还会发现目录上多出一个.git的文件夹,这个文件夹是Git来跟踪管理版本库的，不要去修改这个文件里的内容。


-	git add x.txt添加指定文件到仓库中


-	不会有任何提示，但是提交成功了


-	失败会提示fatal: pathspec 'x.txt' did not match any files


-	可能会出现警告，由于linux和window的换行符不一致导致的。


-	警告内容：warning: LF will be replaced by CRLF in a.txt. 


-	解决方式：git config --global core.autocrlf false 


-	怎么查看有没有添加成功呢？


-	git status 红色表示在工作区，绿色表示在暂存区


-	git commit -m 'xxx'提交所有文件


-	提交成功会提示：												[master (root-commit) 88bbb64] first commit
 	1 file changed, 2 insertions(+)
 	create mode 100644 x.txt


-   如果只输入git commit会出问题，ESC + ：+ wq 退出就好

-   **在文件在暂存区用Vi修改文件时，此时如果使用git status检查，会红色绿色都有，也就意味着，此时文件在工作区和版权区都存在**

##3.理解工作区+版本区+暂存区

- 工作区（working Directory）**[在当前目录下，除了.git 的其他区域]**：简单的理解你在电脑里能看到的目录。


- 版本库（Repository）**[.git文件]**：工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。


- 暂存区（stage）**[.git文件下的index文件]**：Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。


- **第一步是用git add把文件添加进去，实际上就是将工作区文件添加到暂存区**


- **第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支（版本库）**

##4.差异对比

- git diff : 比较工作区与暂存区
 
- git diff --cached : 比较暂存区与版本区
 
- git diff master : 比较工作区与版本区


##5.日志与版本号

- git log 显示从最近到最远的所有提交日志

- git reflog 显示每次提交（commit）的commit id

        

##6.版本回退+版本穿梭+版本撤销
- git reset --hard HEAD^ 版本回退（回退一次提交）

- git reset --hard Obfafd 回退到指定Obfafd的commit id版本


- git reset HEAD 将暂存区的目录树重写为HEAD指向的版本库中的目录树


- git checkout -- x.txt 将暂存区指定的文件替换工作区的文件（危险）


- git checkout HEAD x.txt 将HEAD指向的版本库中的文件替换暂存区和工作区的文件（危险）


- git rm --cached x.txt 从暂存区删除文件
- **git reset --hard HEAD^  回退到上一个版本**
- **git reset --hard xxx（commitid） 回退到指定版本**

##7.删除文件
- git rm x.txt 删除文件


- git rm -r x.txt 删除文件夹

##8.分支
- git checkout -b dev 创建dev分支，并切换到dev分支


- git checkout master 切换分支


- git merge dev 合并指定dev分支到当前分支


- git branch -d dev 删除指定分支


- git branch 查看当前分支


- git diff branch1 branch2 显示出两个分支之间所有有差异的文件的详细差异**（两个分支必须都添加到版本库）**


- git diff branch1 branch2 --stat （统计大概）显示出两个分支之间所有有差异的文件列表


- git diff branch1 branch2 文件名(带路径) 显示指定文件的详细差异

##9.版本冲突（手动解决）
##10.版本控制工具的区别
* 集中式和分布式的区别
	* 集中式代码集中存放在中央服务器，其他开发者只有其中的某一个版本。分布式每个开发者都有完整的版本库
	* 集中式必须联网才能进行版本控制，分布式可以离线开发
#3.github
* 是什么？
	* 基于git一个网址，用来托管git项目网址
* 本地有项目，远程空仓库
	* 本地先进行版本控制
		* git init
		* git add .
		* git commit -m 'xxx'
	* 本地和远程进行关联
		* git remote add origin xxxxx
	* 将本地项目推送到远程仓库中
		* git push -u origin master 首次
		* git push origin master 之后
* 本地没东西，远程有项目
	* 将远程仓库中的项目克隆到本地来
		* git clone xxxxx  将远程仓库克隆到本地（将远程和本地关联） 
* 本地有修改
	* 本地先进行版本控制
		* git init
		* git add .
		* git commit -m 'xxx'
	* 将本地项目推送到远程仓库中
		* git push origin master
* 远程有修改
	* git pull origin master 将远程仓库中的内容更新到本地来（直接合并文件,可能导致冲突）
	* git fetch origin dev:test 将远程仓库中指定分支dev的内容更新到本地并新建一个分支test保存（不会导致冲突）




