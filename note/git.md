### 学历代表你的过去，能力代表你的现在，学习代表你的将来！
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
