## git 命令
* init ： 进入任一一个普通文件夹，执行 “git init” 操作，将会使得当前文件夹成为仓库。
* add : 用于将文件添加到仓库中
* commit : 用于将文件提交到仓库，执行完这一步之后，会显示当前的操作的细节，例如增加、减少、修改那些行。与add的区别在于，每次只能添加一个文件，但是可以提交多个文件。而且在提交时应该利用 “-m” 参数附上信息，即：“git commit -m "message" ”。
* status ： 显示当前仓库的状态。<br>
当对一个文件进行了修改之后，在添加（add）之前，使用**git diff**命令，会显示当前文件和前一个版本文件的区别，使用**git status**会显示*Changes not staged for commit*，表示修改未提交；在执行**git add**之后，在使用**git diff**命令，此时则没有输出，使用**git status**会显示*Changes to be committed*，即修改马上就要提交；在执行**git commit -m message**之后，再执行**git status**会显示*nothing to commit, working tree clean*;如果新建一个文件，还没有add，执行**git status**会显示*Untracked file*.
* 如果在工作区对一个文件进行了修改但是并没有提交到暂存区的话，执行**git checkout -- file name**就可以撤销对该文件的修改，其本质其实就是用仓库里面的文件代替工作区中的文件；如果已经提交到了暂存区，那么就执行**git reset HEAD file name**，将修改退回到工作区，然后再撤销工作区的修改即可。
* rm : **git rm filename**,用于删除文件
## git 存储分区
git 主要分为三个区域，如下图所示：<br>
![分区图片](https://github.com/HappyCodingJoe/GitSkills/blob/master/GitPartition.png)

其中，工作区就是我们所能看到的文件目录，而执行**git add**之后则会将文件提交到暂存区（**stage**），然后再执行**git commit -m message**将暂存区中的所有文件一次性提交到当前分支。
