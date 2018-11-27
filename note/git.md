### 学历代表你的过去，能力代表你的现在，学习代表你的将来！

---
![git](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015120901.png "git")
# 常用命令
* git config --global user.name “your_username”
* git config --global user.email “your_registered_github_Email”
* git clone git@github.com:XXX/yyyy.git //XXX为github的用户名，yyy为仓库名
* git status
* git add mmm.sss
* git commit -m "hhh"
* git log
* git push
* git init
* git log --pretty=short
* git log ggg //ggg是指指定的文件或目录，用于查看指定的目录、文件的日志
* git log -p //查看提交所带来的改动
* git log -p ggg //查看指定文件的改动
* git diff
* git diff HEAD //查看工作树与最新提交的差别
* git branch //显示分支一览表，同时确认当前所在的分支
* git checkout -b aaa //创建名为aaa的分支，并且切换到aaa分支
* git branch aaa //创建名为aaa的分支
* git checkout aaa // 切换到aaa分支
* git checkout - //切换到上一分支
* git checkout master //切换到master分支
git marge --no--ff aaa // 加--no--ff 参数可以在历史记录中明确地记录本次分支的合并
git log --graph //以图表形式查看分支
* git reset //回溯历史版本
* git reset --hrad //回溯到指定状态，只要提供目标时间点的哈希值
* git reflog //查看仓库的操作日志，找到要推历史的哈希值
git reset --hrad ddd //ddd为要推进历史的哈希值
* git remote add eee git@github.com: 用户名/仓库名.git //添加远程仓库，并将git@github.com: 用户名/仓库名.git远程仓库的名称改为eee
* git push -u eee master //推送至远程仓库 master分支下 -u 参数可以在推送的同时，将eee仓库的master分支设置为本地仓库的当前分支的的upstream（上游）；添加这个参数，将来运行git pull命令从远程仓库获取内容时，本地仓库的这个分支就可以直接从eee的master
* git checkout -b feature d eee/feature d //获取远程的feature d分支到本地仓库，-b参数后面是本地仓库中新建的仓库的名称
* git pull eee feature d //将本地的feature d分支更新为最新状态
* 在GitHub上面查看两个分支之间的差别，只需要在地址栏中输入http://github.com/用户名/仓库名/分支1...分支2
查看master分支在最近七天内的差别：http://github.com/用户名/仓库名/master@{7.day.ago}...master （同样，day，week，month，year都是可以哒）
查看与指定日期之间的差别：http://github.com/用户名/仓库名/master@{xxxx-xx-xx}...master （xxxx-xx-xx代表年月日）
* git config --list
* git rm [file1] [file2] 删除工作区文件，并且将这次删除放入暂存区
* git rm --cached [file] 停止追踪指定文件，但该文件会保留在工作区
* git mv [file-original] [file-renamed] 改名文件，并且将这个改名放入暂存区
* git commit -v 提交时显示所有diff信息
* git commit --amend -m [message] 使用一次新的commit，替代上一次提交;;如果代码没有任何新变化，则用来改写上一次commit的提交信息
* git commit --amend [file1] [file2] 重做上一次commit，并包括指定文件的新变化
* git branch 列出所有本地分支
git branch -r 列出所有远程分支
git branch -a 列出所有本地分支和远程分支
* git branch [branch] [commit] 新建一个分支，指向指定commit
* git branch --track [branch] [remote-branch] 新建一个分支，与指定的远程分支建立追踪关系
* git branch --set-upstream [branch] [remote-branch] 建立追踪关系，在现有分支与指定的远程分支之间
* git merge [branch] 合并指定分支到当前分支
* git cherry-pick [commit] 选择一个commit，合并进当前分支
* git branch -d [branch-name] 删除分支
* git push origin --delete [branch-name] 删除远程分支
git branch -dr [remote/branch] 删除远程分支
* git tag 列出所有tag
* git tag [tag] 新建一个tag在当前commit
* git tag [tag] [commit] 新建一个tag在指定commit
* git tag -d [tag] 删除本地tag
* git push origin :refs/tags/[tagName] 删除远程tag
* git show [tag] 查看tag信息
* git push [remote] [tag] 提交指定tag
* git push [remote] --tags 提交所有tag
* git checkout -b [branch] [tag] 新建一个分支，指向某个tag
* git log --stat 显示commit历史，以及每次commit发生变更的文件
* git log -S [keyword] 搜索提交历史，根据关键词
* git log [tag] HEAD --pretty=format:%s 显示某个commit之后的所有变动，每个commit占据一行
* git log [tag] HEAD --grep feature 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
* git log --follow [file] 显示某个文件的版本历史，包括文件改名
git whatchanged [file]
* git log -p [file] 显示指定文件相关的每一次diff
* git log -5 --pretty --oneline 显示过去5次提交
* git shortlog -sn 显示所有提交过的用户，按提交次数排序
* git blame [file] 显示指定文件是什么人在什么时间修改过
* git diff 显示暂存区和上一个commit的差异
* git diff HEAD 显示工作区与当前分支最新commit之间的差异
* git diff [first-branch]...[second-branch] 显示两次提交之间的差异
* git diff --shortstat "@{0 day ago}" 显示今天你写了多少行代码
* git show [commit] 显示某次提交的元数据和内容变化
* git show --name-only [commit] 显示某次提交发生变化的文件
* git show [commit]:[filename] 显示某次提交时，某个文件的内容
* git rebase [branch] 从本地master拉取代码更新当前分支：branch 一般为master
* git remote update 更新远程仓储
* git fetch [remote] 下载远程仓库的所有变动
* git remote show [remote] 显示某个远程仓库的信息
* git remote add [shortname] [url] 增加一个新的远程仓库
* git pull [remote] [branch] 取回远程仓库的变化，并与本地分支合并
* git push [remote] [branch] 上传本地指定分支到远程仓库
* git push [remote] --force 强行推送当前分支到远程仓库，即使有冲突
* git push [remote] --all 推送所有分支到远程仓库
* git checkout [file] 恢复暂存区的指定文件到工作区
* git checkout [commit] [file] 恢复某个commit的指定文件到暂存区和工作区
* git checkout . 恢复暂存区的所有文件到工作区
* git reset [file] 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
*  git reset --hard 重置暂存区与工作区，与上一次commit保持一致
* git reset [commit] 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
* git reset --hard [commit] 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
* git reset --keep [commit] 重置当前HEAD为指定commit，但保持暂存区和工作区不变
* git revert [commit] 新建一个commit，用来撤销指定commit 后者的所有变化都将被前者抵消，并且应用到当前分支
* git stash 暂时将未提交的变化移除，稍后再移入
git stash pop
* git archive 生成一个可供发布的压缩包
* remote->repository
