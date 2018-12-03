## git 命令
* init ： 进入任一一个普通文件夹，执行 “git init” 操作，将会使得当前文件夹成为仓库。
* add : 用于将文件添加到仓库中
* commit : 用于将文件提交到仓库，执行完这一步之后，会显示当前的操作的细节，例如增加、减少、修改那些行。与add的区别在于，每次只能添加一个文件，但是可以提交多个文件。而且在提交时应该利用 “-m” 参数附上信息，即：“git commit -m "message" ”。
* status ： 显示当前仓库的状态。<br>
当对一个文件进行了修改之后，在添加（add）之前，使用**git diff**命令，会显示当前文件和前一个版本文件的区别，使用**git status**会显示*Changes not staged for commit*，表示修改未提交；在执行**git add**之后，在使用**git diff**命令，此时则没有输出，使用**git status**会显示*Changes to be committed*，即修改马上就要提交；在执行**git commit -m message**之后，再执行**git status**会显示*nothing to commit, working tree clean*;如果新建一个文件，还没有add，执行**git status**会显示*Untracked file*.
* 如果在工作区对一个文件进行了修改但是并没有提交到暂存区的话，执行**git checkout -- file name**就可以撤销对该文件的修改，其本质其实就是用仓库里面的文件代替工作区中的文件；如果已经提交到了暂存区，那么就执行**git reset HEAD file name**，将修改退回到工作区，然后再撤销工作区的修改即可。
* rm : **git rm filename**,用于删除文件
* clone : **git clone git@github.com:michaelliao/gitskills.git**,克隆远程仓库到本地。
## git 存储分区
git 主要分为三个区域，如下图所示：<br>
![分区图片](https://github.com/HappyCodingJoe/GitSkills/blob/master/GitPartition.png)

其中，工作区就是我们所能看到的文件目录，而执行**git add**之后则会将文件提交到暂存区（**stage**），然后再执行**git commit -m message**将暂存区中的所有文件一次性提交到当前分支。
## 添加远程仓库
在本地仓库执行以下命令,可以将本地仓库与远程仓库相关联：
```
git remote add origin gitaddress
```
然后将本地仓库的当前分支推送到远程分支,这里的`-u`只需要在第一次推送时使用，后面就不需要：
```
git push -u origin master
```
## 分支管理
### 基本命令
git的每一个分支就是一个时间线，HEAD指向的是当前分支。新建分支**git branch branchname**就是新建一个指针并指向当前的时间点；切换分支**git checkout branchname**就是将HEAD指针指向想要的分支指针；删除分支**git branch -d branchname**其实就是删除分支指针，如果要强行删除一个分支则为**git branch -D branchname**;合并分支**git merge branchname**就是把指定分支合并到当前分支，实际就是把当前分支的指针指向目标分支。
### 解决冲突
如果在master分支上产生了一个新分支dev，又在master以及dev分支上均产生了新的修改，这时候再进行合并时可能会产生冲突，**但是这个冲突只是以特殊字符标注的方式指出，此时只能进行人工修改解决冲突，但是如果依然直接提交，会把两个分支冲突的内容以及提示符包含在其中提交上去**。可以用**git log --graph**来查看分支合并图。
### 临时分支隐藏——Stash
**git status**用于临时隐藏当前的工作状态，待修改的文件无论是出于**工作区**还是**暂存区**,经过stash之后，当前分区都会回到clean状态，这时候可以随意切换到别的分支。之后再恢复的时候，**git stash list**可以查看隐藏的列表，可以指定**git stash apply stashnumber**来恢复，并**git stash drop stashnumber**来删除，但是如果只有一个的话，直接**git stash pop**弹出一个并删除。
>从master分支，新建一个分支dev分支，然后对一个文件进行修改，此时可以在master分支与dev分支之间随意切换，而且文件保持不变（即并不会因为切换到master分支而回到master分支里面的状态），只有在commit之后，再切换到master分支，此时被修改的文件才会回到master分支里应该存在的状态。由于dev分支已经commit了一次了，因此dev和master已经不再指向一个点，这时候再在dev分支里面对某个文件进行修改，在提交之前不能进行分支切换。而此时进行**git stash**操作的意义就体现出来了，使得当前分支回到**clean**的状态
## 多人协作流程
>1.首先，试图用**git push origin branch-name**推送自己的修改<br>
2.如果推送失败，则因为远程分支比本地更新。需要先用git pull拉去并自动合并，如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令**git branch --set-upstream-to branch-name origin/branch-name**<br>
3.如果合并有冲突，则解决冲突，并在本地重新推送提交<br>
