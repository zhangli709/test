
## git 分布式版本控制系统，分布式版本控制系统也还有svn
* 集中式版本控制SVN,有一个中央处理器，每个人都只能看自己的那一部分，且需要联网
* 分布式控制Git，每个人都能看见全部的代码，且不需要联网，只是最后需要整合在一起上线，之前* 都是在自己的分支上修改。 分支，测试，开发。

1. 删除分支 
* git branch -d 分支名

2. 克隆代码 git clone url
3. 查看分支 git branch
4. 创建分支 git checkout -b username
5. 查看状态git status
6. 切换分支 git checkout username
7. 添加修改的数据到缓存区 
* git add .
* git add 修改的文件名
8. 提交修改到本地分支
* git commit -m ''
9. 提交本地分支到远程分支上
* git push origin 分支名
10. 设置全局变量
git config --global user.name "Mr.Zhang"
git config --global user.email "zhangli9479@163.com"
11. 合并add commit 操作
git commit -am ''
12. ssh-keygen -t rsa -C  账号zhangli9479@163.com  创建密钥
* 找到公钥所在的文件，将其添加到git网站的 setting里。
13. git diff a b  比较a和b的差别
14. 在master分支下使用语句， git merge zl     意思是把zl 合并到master上。
15. 分支 
* git branch 查看所有分支
* git branch name 创建
* git checkout name  更换
* git checkout -b name 创建并更换分支
* git merge name 合并
* git branch -D name  删除分支
16. git tag -a 版本号 -m  '注解'   打tag标签
17. git push origin 版本号  推送此到远程。
18. git push origin --delete 分支名  删除远程分支。
19. git tag -d 版本号  删除版本号
20. 缓存   只能缓存修改的东西，不能缓存新建的东西
* git stash  缓存修改的代码
* git stash list  查看缓存
* git stash apply stash@{0}  还原缓存    

# 步骤
1. git init  初始化一个仓库
2. git add .
3. git commit -m '说明'       
4. git remote add origin url  连接远程仓库
5. git push -u origin master / branch分支名

# 版本回退
1. git log 显示最近到最远的提交日志。  --pretty=oneline单行输出
2. git reset --hard HEAD^ 返回上一个版本
3. git reset --hard 未来版本号     回到未来版本，前提是你记得到版本号。
* git reflog 查看记录的命令
4. git reset --hard 版本号   去到指定的版本。

# 工作区和暂存区
* 你能在电脑里看到的目录，就是工作区
* 工作区有一个隐藏目录 .git ，叫做git的版本库，版本库里有个很重要的stage/ index 暂存区，还有git为我们自动创建的第一个分支master,以及指向master的一个叫HEAD的东西
* 添加东西的步骤
	1. 用git add 添加文件到暂存区
	2. 用git commit提交更改，把暂存区的所有内容提交到当前分支，然后暂存区就空了。

# 管理修改
1. git 跟踪管理的是修改，而非文件。
2. git diff HEAD --readme.txt / 文件名    查看工作区和版本库里面最新版本的区别。

# 撤销修改
1. git status 查看状态
2. git checkout --readme.txt  把readme.txt文件在工作区的修改全部撤销。
* 回到最近一次的git commit 或 git add 时的状态
3. git reset HEAD file 可以把暂存区的修改撤销掉，重新放回工作区。
* git reset 既可以退回版本，也可以把暂存区的修改回退到工作区
4.四大应用场景
 * 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
* 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。
* 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

# 删除文件
1. rm

# 分支管理，步骤
1. git checkout -b dev
2. git branch
3. git add .  添加到缓存
4. git commit -m '' 提交到本地
5. git checkout master 切换到master分支
6. git merge dev 合并分支
7. git branch -D dev
8. git branch

# 解决冲突
1.git log --graph --pretty=oneline --abbrev-commit 查看分支合并的情况。
2. 当Git无法自动合并分支时，先解决冲突，再提交。

# 分支管理策略
1. git merge --no-ff 表示本次合并要创建一个新的commit，这个是一个历史。
2. git log 查看分支历史

# Bug分支
1. git stash 保存现场
2. 干其他的事
3. git stash list 查看保存的现场记录
4. git stash apply ... 恢复内容，
5. git stash drop ... 删除现场保存的记录。
* git stash pop ... 先恢复现场，再删除记录

# Feature分支
1. git branch -d name 普通删除
2. git branch -D name 强制删除

# 多人协作
* git remote -v 查看远程库的信息
* origin 远程仓库的默认名称
# 推送分支
* git push origin name
# 抓取分支
* git clone url 下载网上项目
# 多人协作的工作模式
1. git push origin branch-name推送自己的修改
2. 如果推送失败，是因为远程的分支比你的本地更新，需要先用git pull 合并。
3. 如果合并失败，则解决冲突，并在本地提交
4. 解决冲突后，再次git push origin branch-name.
* 报no tracking information错误
* git checkout -b branch-name origin/branch-name  在本地创建和远程分支对应的分支
*  git branch -- set upstream branch-name origin/branch-name 建立本地分支和远程分支的联系。

## 标签管理 即版本，快照。
# 创建标签
1. git tag v1.0  在需要打标签的分支上敲这句话。
* git log 
* git tag 
2. git tag -a v1.0 commit_id对特定的打标签 
* 标签不是按照时间顺序，而是字母顺序排列的。
* git show tagname  查看标签信息
#操作标签
1. git tag -d v1.0  删除标签
2. git push origin tagname  推送标签到远程库。
3. git push origin --tags  一次性推送所有未推送的本地标签。
4. git push origin --delete (tag) v1.0