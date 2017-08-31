	查看当前所有分支
git branch -a
	基于当前HEAD创建分支b1
git branch b1
	在origin/master的基础上，创建一个新分支newBrach，并切换到newBrach
git checkout newBrach origin/master
	将工作区切换到主线master
git checkout master
	重命名分支
git branch -m oldbranch newbranch
git branch -m newbranch
	强制push本地分支到远端[拒绝merge到本地]，[可以使用-u选项指定一个默认主机]
	删除分支
git branch -d b1
git push -u origin RAZOR-16711:RAZOR-16711
git push -u --force origin RAZOR-16711:RAZOR-16711
	设置commit描述消息文本
git commit -m "RAZOR-16711:some commit message"
	取回origin主机的master分支
git fetch origin master
	取回origin主机的next分支，与本地的master分支合并
git pull origin next:master
	如果远程分支是与当前分支合并，则冒号后面的部分可以省略。
git pull origin next
	本地的master分支自动"追踪"origin/master分支
git branch --set-upstream master origin/next，上面命令指定master分支追踪origin/next分支。
	下面命令表示删除origin主机的master分支。
$ git push origin :master
# 等同于
$ git push origin --delete master
	在Git v1.7.0 之后，可以使用这种语法删除远程分支：
git push origin --delete <branchName>
	重命名远程分支，把 devel 分支重命名为 develop 分支
1删除远程分支：git push --delete origin devel
2重命名本地分支：git branch -m devel develop
3推送本地分支：git push origin develop
	查看本地当前分支的commit
git log --pretty=oneline
	cherry-pick其他分支的commit，并自定义提交信息
git cherry-pick -e "some commit message" <commit id>
	cherry-pick其他分支的commit，保留更改但不提交
git cherry-pick -n <commit id>
	使用 git status 來查看檔案狀態
git status 
	取消，並且回到 cherry-pick 前的狀態
git cherry-pick --abort
	查看分支提交历史信息
git log --oneline
	查看本地分支对应的远程分支
git branch -vv
	rebase本地分支 branchA onto new分支，比如master
git rebase master
git rebase --force-rebase --onto master branchA
================================================
	合并某个分支上的一系列commits
假设你需要合并feature分支的commit 76cada ~62ecb3 到master分支。
首先需要基于feature创建一个新的分支，并指明新分支的最后一个commit：
git checkout -bnewbranch 62ecb3  
然后，rebase这个新分支的commit到master（--ontomaster）。76cada^ 指明你想从哪个特定的commit开始。
git rebase --onto master 76cada^  
得到的结果就是feature分支的commit 76cada ~62ecb3 都被合并到了master分支。
================================================
	如何使用git merge 一系列的commits?
git log --pretty=oneline
看到如下结果
commit ac72a4308ba70cc42aace47509a5e
commit 77df2a40e53136c7a2d58fd847372
commit 249cf9392da197573a17c8426c282
之后执行以下命令即可合并前两条commit
git reset --mixed 249cf9392da197573a17c8426c282
git add .
git commit -m 'some commit message'
#================================================
   .gitignore 不起作用
git rm -r --cached .
git add .
git commit -m 'update .gitignore'




