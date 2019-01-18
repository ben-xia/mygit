https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
1.初始化一个Git仓库:cd到某个目录,之后使用 git init命令。
2.用命令git add file 告诉Git，把文件添加到仓库,注意，可反复多次使用，添加多个文件；git add -A：将文件的修改，文件的删除，文件的新建，添加到暂存区。
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

21.分支管理: 一开始的时候，master分支是一条线，Git用master指向最新的提交，再用HEAD指向master，就能确定当前分支，以及当前分支的提交点
	查看分支,当前分支前面会标一个*号。：git branch
	创建分支：git branch <name>
	切换分支：git checkout <name>
	创建+切换分支：git checkout -b <name>
	合并某分支到当前分支：git merge <name>
						git merge --no-ff -m "merge with no-ff" dev: ,
						[Fast forward模式合并分支,会在删除分之后,丢掉分支的信息;--no-ff表示禁用Fast forward模式,此时Git就会在merge后生成一个新的commit，这样，从分支历史上就可以看出分支信息]
	删除分支：git branch -d <name>

	当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

	git log --graph --pretty=oneline --abbrev-commit: 查看分支合并图

	Bug分支: Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作;
		     git stash list:罗列出所以的stash;
	         恢复现场: 一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；
	                  另一种方式是用git stash pop，恢复的同时把stash内容也删了：

	Feature分支:开发一个新feature,最好新建一个分支;如果要丢弃一个没有被合并过的分支;可以通过git branch -D <name>强行删除。

	当你从远程仓库克隆时,实际上Git自动把本地的master分支和远程的master分支对应起来了,并且远程仓库的默认名称是origin
	git remote -v:查看远程库的信息,它会显示可以抓取和推送的origin的地址。如果没有推送权限，就看不到push的地址。

	多人协作的工作模式：
		首先，可以试图用git push origin <branch-name>推送自己的修改；
		如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
		如果合并有冲突，则解决冲突，并在本地提交；
		没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
		如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。

22.标签管理
	Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像对不对？但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的。

	本地创建标签:    git tag [-a]<name> [-m '说明文字'] [commit id] (默认标签是打在最新提交的commit上的,也可以选择打在指定的提交上)
	查看标签列表: git tag (标签不是按时间顺序列出，而是按字母排序的。可以用git show <tagname>查看标签信息)

	命令git push origin <tagname>可以推送一个本地标签到远程仓库；
	命令git push origin --tags可以推送全部未推送过的本地标签到远程仓库；
	命令git tag -d <tagname>可以删除一个本地标签；
	命令git push origin :refs/tags/<tagname>可以删除一个远程标签。



