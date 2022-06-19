Git

一，什么是git? 

	分布式版本控制系统，可以有效，快速的进行项目版本管理
二，为什么需要git

	因为手动进行版本管理太复杂，尤其是多个人的时候,设想：多人在一起开发代码，在别人增加功能后，需要把代码同步给你，由你手动添加新增的代码，何其复杂？
三，git的优点：

	适合分布式开发，强调个体；

	公共服务器压力和数据量都不会太大；

	速度快、灵活；

	任意两个开发者之间可以很容易的解决冲突；

	离线工作。
四，git的工作流程
	一般工作流程如下：

	从远程仓库中克隆资源作为本地仓库；

	在本地仓库中进行代码修改；

	在提交本地仓库前先将代码提交到暂存区；

	提交修改，提交到本地仓库。本地仓库中保存修改的所有历史版本；

	在需要和团队成员共享代码时，可以将修改的代码push到远程仓库。

	// todo, 需要放上流程解析图片



五，git常用命令操作

	查看所有本地分支	git branch

	列出所有远程分支	git branch -r

	新建一个分支，但依然停留在当前分支	git branch [branch-name]

	新建一个分支，并切换到该分支	git checkout -b [branch]

	合并指定分支到当前分支	git merge [branch]

	删除分支	git branch -d [branch-name]

	删除远程分支
		git push origin --delete [branch-name]
		git branch -dr [remote/branch]


六，git实际操作

- 功能开发到一半，需要修复线上问题

  1. 在当前分支上，git bash = git stash save（保存未提交的内容, 想要添加保存信息则执行：git stash save -a “message”（git stash save命令将来会被git stash push代替））	
  2. 切换分支
  3. 修复完后回到原开发分支，并执行git stash pop (git stash pop = git stash apply stash@{0} + git stash drop stash@{0})

- 将代码提交到错误分支

  1. 切换到在目标分支dev下执行->git cherry-pick commitId1 commitId2..
  2. git rebase：git rebase --onto dev<开始的commitId><结束的commitId>
  3. 切换到目标分支git checkout dev

  	执行上述操作后，实际上git会将dev作为基底分支，将<开始的commitId><结束的commitId>做的相应改变重做一遍，重做的commitId可能跟旧的commitId不一样（若是能ff，则commitId一样），重做后，HEAD指针指向最新的commitId上（游离状态，没有指向任何分支上）

- 需要将其他分支的文件复用过来：

  ​git checkout source_path(其他分支) filename1 filename2...(其他分支
  的文件)

- 需要删除中途某次提交：
  git revert commitID 
  使用一次新的commit来回滚之前的commit

- 本地仓库需要回退到某个版本

   1. git reset --hard commitId ： 将 commitId 和 commitId 之后的所有提交记录均删除；但是如果 merge 其他老的分支到该分支，commitId后面被回滚的commit应该还会被引入（一般在提交点push到公共分支之前操作）
   2. git reset --soft commitId：此次提交之后的修改会被退回到暂存区。(回退版本commitId后的修改还保留在本地工作空间)
   3. git reset commitId 默认使用选项 --mixed，此次提交之后的修改会被退回到工作区


- ​迭代发布时，需要确认分支是否合并
  git branch --merge
  git branch --no-merged 

  
