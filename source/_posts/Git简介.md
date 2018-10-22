---
title: Git简介
date: 2018-10-15 14:30:53
tags: Git
---
### git是什么
 Git是目前世界上最先进的分布式版本控制系统
### 安装Git
在Mac 上安装Git 可以从AppStore安装Xcode，Xcode集成Git，不过默认没有安装，需要运行Xcode
选择Xcode->preference,在弹框窗口中找到“Downloads”选择“Command Line Tools”点击install
就可以完成安装
 在Windows上安装使用Git，可以从Git官网直接去下载[安装程序](https://git-scm.com/downloads)，然后按照默认选项安装就可以了
 安装完成后，在开始菜单里找到Git->Git Bash，出现一个类似于命令行的东西就说明Git安装成功了
 ![](Git_Bash.png)
### 创建版本库
版本库其实就是仓库，英文名就是repository,其实就是一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改，删除，Git都能
跟踪，
所以创建一个版本库非常简单，首先就是要选择一个合适的地方，创建一个空目录
> mkdir learngit
> cd learngit
> pwd    pwd命令用于显示当前目录

然后通过
> git init 

把这个目录变成Git可以管理的仓库
![输入相应的命令对应的输出](learnGit.png)
这个时候就把仓库建好了，而且这个是一个空的仓库，在输入 git init 会发现当前目录多了一个.git目录，这个目录就是Git来管理跟踪管理版本库的
一般尽量不要改动这个目录里面的文件，不然容易破坏了Git仓库
### 把文件添加到版本库
现在我们在learngit目录下编写一个readme.txt文件，
内容可以随便写比如
.Git is a version control system.
.Git is free software
接下来要做的就是把这个文件放到Git仓库中
第一步：
 用命令git add告诉Git，把文件添加到仓库：
 > git add readme.txt
 
 执行上面的命令，没有啥显示，这就说明添加成功了。
 第二步：
 用命令 git commit告诉Git，把文件提交到仓库：
 > git commit -m "wrote a readme file"  -m后面的就是本次提交说明，可以输入任何内容
 ![](s.png)
### 版本回退
在工作中一个文件我们可能会有很多次的改动，但是每次改动的记录我们可以使用git log命令去查看
比如我修改内容为
.Git is a version control system.
.Git is free software distributed under the GPL.
![每次修改的记录](X.png)
现在我想把readme.txt回退到上一个版本，首先必须要知道当前版本是哪个版本，用HEAD表示当前版本，
上一个版本就是HEAD^,上上个版本就是HEAD^^, 往上100个版本就写成HEAD~100，然后就可以使用
> git reset --hard HEAD^

再用
> cat readme.txt

就可以查看readme.txt的内容了
![内容就成为之前的内容了](E.png)
当然要是我回退版本后后悔了，想要恢复新的版本就可以使用
> git reflog

找到新版本的commit id
然后在使用

> git reset --hard commit_id  就可以了

![查看内容有成为最新版本的内容了](N.png)
### 工作区和暂存区
Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念
#### 工作区
就是你在电脑里看到的目录，比如我之前创建的learngit就是一个工作区
#### 版本库
工作区有一个隐藏目录.git,这个并不是工作区，而是Git的版本库。
Git的版本库里面存在很多东西，其中最重要的就是称为stage的暂存区，还有Git为我们自懂创建的第一个分支master,
以及指向master的一个指针叫HEAD.
### 关于修改
Git管理的是修改，当使用git add命令后，在工作区的第一次修改就被放入暂存区，git commit 只负责把暂存区的修改给提交了，
提交后可以用
> git diff HEAD --readme.txt

命令可以查看工作区和版本库里面的最新版的区别
如果每次修改后不用git add到暂存区，就不会加入到commit中的
.当你改乱了工作区的某个文件的内容，想要丢弃工作区的修改时，用命令
> git checkout -- file

.当你不但改动了工作区某个文件的内容，还添加到了暂存区时，想放弃修改的时候，使用
> git reset HEAD <file>  可以把暂存区的修改撤销掉（unstage），重新放回工作区
> git checkout -- file

命令git checkout --file把文件在工作区的修改全部撤销，有俩种情况：
1. 文件自修改后还没有被放到暂存区，现在撤销修改就回到和版本库一抹一样的状态
2. 文件已经添加到暂存区后，又做了修改，现在，撤销修改就回到暂存区的状态
. 如果提交了不合适的修改到版本库时候，想要撤销本次提交的时候，可以使用
> git reset --hard commit_id

进行版本回退，前提是没有提交到远程仓库
文件当前的状态可以用
> git status  查看
### 删除文件
删除文件分为俩种情况
1.如果你有一个新建的文件并且已经提交到版本库需要从版本库中删除可以使用
> git rm file
> git commit -m  "xxxx" -m后内容本次提交的说明

进行删除，使用$ git commit 文件也就从版本库中被删除了
2. 如果发现自己删除错误，但是并没有从版本库中删除，可以使用
>  git checkout -- file
进行一键还原

如果从版本库删除了就需要使用 git reset --hard commit_id进行版本还原恢复了
### 远程仓库
 在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这俩个仓库进行远程同步
 创建一个远程仓库首先登陆你的GitHub
 点击右上角的“+”号，点击“New repository”
 ![](add.png)
 然后在repository name填入learngit(仓库名称)其他的可以保持默认
![](new.png)
最后将已有的本地仓库与远程仓库关联
.要关联一个远程仓库，使用命令git remote add origin git@server-name: path/repo-name.git;
.关联后，使用命令git push -u origin master第一次推送master分支上的所有内容；
.此后，每次本地提交后，只有有必要就可以使用git push origin master推送最新修改
### 从远程库克隆项目
克隆一个仓库，首先要知道仓库的地址，然后使用
> git clone 项目地址
### 创建并合并分支
创建一个dev分支，然后切换到dev分支
> git branch dev
> git checkout dev

查看当前分支
> git branch

![](dev.png)

绿色并带有星号表示当前分支

完成dev上的工作后，要合并俩个分支用
> git merge dev 

就可以将dev分支合并到master上去
合并完成后，就可以用 
> git branch -d dev

删除dev分支了
### 解决冲突
在我们在一个新的分支上完成工作，并进行提交的时候。master分支也有了新的提交
这种合并可能会产生冲突，这时候就需要我们手动去解决冲突，然后再次提交，进行合并。

### 修改bug
当有bug要修改的时候，这时候需要创建一个分支issue-101来修复它，但是，正在dev上进行的工作并没有提交，
这时候就可以使用
> git stash

将当前工作现场储存起来，然后再用
> git status

查看工作区，就是干净的，然后就可以创建分支来修复bug了，需要在那个分支上修复bug,就在那个分支上创建临时分支
假若，需要在master分支上修复，就在master创建临时分支
> git checkout master
> git checkout -b bug1

然后将修复的文件提交(假若修改了readme.txt)
> git add readme.txt
> git commit -m "fix bug 1"

修复后切换到master分支，完成合并，
> git checkout master
> git merge --no-ff -m "fix bug 1" bug1

然后用
> git stash pop

将刚才存起来的工作恢复，并继续进行工作.
如果需要丢弃一个没有合并过得分支，可以使用 
> git branch -D name

进行删除
### 多人协作开发
一般多人协作工作模式一般是
1. 首先可以试图用git push origin <branch-name>推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图去合并
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 如果解决到冲突，再用git push origin <branch-name>推送就能成功
如果使用git pull 提示no tracking information，则说明本地分支和远程分支的连接关系没有创建，用命令
git branch --set-upstream-to <branch-name> origin/<branch-name>




