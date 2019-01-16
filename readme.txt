1.初始化一个Git仓库:cd到某个目录,之后使用 git init命令。
2.用命令git add file 告诉Git，把文件添加到仓库,注意，可反复多次使用，添加多个文件；
3.用命令git commit -m '本次提交的说明'告诉Git，把文件提交到仓库;
4.要随时掌握工作区的状态，使用git status命令
5.如果git status告诉你有文件被修改过，用git diff file 可以查看修改内容。
6.git log命令显示从最近到最远的提交日志;
7.用HEAD表示当前版本，也就是最新的提交1094adb...（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
8.git回退版本: git reset --hard HEAD^[或者版本号];
9.git reflog用来记录你的每一次命令[提交,回滚];
10.工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
11.前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：
第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。
你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。
12.用git diff HEAD -- readme.txt命令可以查看工作区和版本库里面最新版本的区别：
13.命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
总之，就是让这个文件回到最近一次git commit或git add时的状态。
git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到git checkout命令。
14.用命令git reset HEAD <file>可以把暂存区的修改撤销掉（unstage），重新放回工作区：
15.rm file 删除工作区的文件,现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令git rm file删掉，并且git commit：
命令gitrm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容
16.git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
17.并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交。
18.要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
	关联后，使用命令git push -u origin master第一次推送master分支的所有内容；由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
	此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；
19.git clone克隆一个本地库: git clone git@github.com:ben-xia/gitskills.git
20.github中的Fork:将别人的项目clone一份到自己的github仓库,自己在将此项目clone到自己本地开发;

21.分支管理 + 标签管理









