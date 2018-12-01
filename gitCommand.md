## git 命令
* init ： 进入任一一个普通文件夹，执行 “git init” 操作，将会使得当前文件夹成为仓库。
* add : 用于将文件添加到仓库中
* commit : 用于将文件提交到仓库，执行完这一步之后，会显示当前的操作的细节，例如增加、减少、修改那些行。与add的区别在于，每次只能添加一个文件，但是可以提交多个文件。而且在提交时应该利用 “-m” 参数附上信息，即：“git commit -m "message" ”。
* status ： 显示当前仓库的状态。<br>
当对一个文件进行了修改之后，在添加（add）之前，使用**git diff**命令，会显示当前文件和前一个版本文件的区别，使用**git status**会显示*Changes not staged for commit*，表示修改未提交；在执行**git add**之后，在使用**git diff**命令，此时则没有输出，使用**git status**会显示*Changes to be committed*，即修改马上就要提交；在执行**git commit -m message**之后，再执行**git status**会显示*nothing to commit, working tree clean*;如果新建一个文件，还没有add，执行**git status**会显示*Untracked file*.
## git 存储分区
git 主要分为三个区域
