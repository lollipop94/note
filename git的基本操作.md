### git的基本操作

选择一个合适的位置，创建一个空目录，比如`git_exercise`，并进入到该目录下，用`pwd`显示当前目录。

```
mkdir git_exercise
cd git_exercise
pwd
```

将该目录变成Git可以管理的仓库。

```
git init
```

执行上述命令后，会在当前目录下看见一个名为.git的文件夹，注意该文件夹是隐藏的。

在目录下，创建一个README.md文件，然后将该文件添加到Git仓库。

```
git add README.md
```

如果执行的是`git add ./`，则意味着是将该目录下的所有文件都添加。
执行`git add`命令是将要提交的所有修改放到暂存区。

然后告诉Git，把文件提交到仓库。

```
git commit -m "first commit"
```

其中，`-m`后面输入的是本次提交的说明。
执行`git commit`是将暂存区的所有修改提交到分支。
如果`commit`时，注释写错了，执行`git commit --amend`命令，进入vim操作命令的模式，键盘输入字母“i”或按下`Insert`键，进入插入编辑模式，然后在你需要修改的地方进行修改，按下`ESC`键，退出编辑模式，切换到命令模式，然后在命令模式下输入`:wq`，就保存修改并退出了。
查看当前文件状态。

```
git status
```

如果没有文件被修改过，则显示如下内容：

```
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean
```

如果存在文件被修改了，则显示如下内容：

```
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

如果想显示README.md文件的内容，则可以执行如下命令：

```
cat README.md
```

查看工作区和版本库里最新版本的区别。

```
git diff HEAD -- README.md
```

查看历史提交记录。

```
git log
```

回退到上一个版本。

```
git reset --hard HEAD
```

查看命令历史。

```
git reflog
```

在`add`之前，执行如下命令可以撤销文件在工作区的修改。

```
git checkout -- README.md
```

如果在`add`之后，`commit`之前，该修改被丢在了暂存区，还没有被提交到仓库。
先将暂存区的修改撤销，重新放回工作区，再撤销在工作区的修改。

```
git reset HEAD README.md
```

`git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区。其中，`HEAD`表示最新的版本。

在当前目录下创建一个新文件test.txt，然后添加并提交到仓库中去。

```
vi test.txt
git add test.txt
git commit -m "test"
```

删除文件。

```
rm test.txt
```

执行`git status`命令，会看到如下内容（我这里README.md里的内容也在修改）：

```
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   README.md
        deleted:    test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

如果确定要从版本库中删除该文件，则执行如下命令：

```
git rm test.txt
git commit -m "remove test.txt"
```

执行后会看到如下内容：

```
On branch master
Changes not staged for commit:
        deleted:    test.txt

no changes added to commit
```

如果是删错了，则把误删的文件恢复到最新版本：

```
git checkout -- test.txt
```

添加远程库。

```
git remote add origin https://github.com/lollipop94/git_exercise.git
```

查看远程库。

```
git remote -v
```

将本地库的所有内容推送到远程库上。

```
git push -u origin master
```

其中，在第一次推送时，远程库还是空的，此时加上`-u`参数，Git不但会把本地的`master`分支的内容推送到远程新的`master`分支，还会把本地的master分支和远程的`master`分支关联起来，在之后的推送或拉取时就可以不带参数了。

```
git push origin master
```

使用`git clone`命令实现克隆。

```
λ git clone https://github.com/lollipop94/Tab_switch.git
Cloning into 'Tab_switch'...
remote: Counting objects: 19, done.
remote: Total 19 (delta 0), reused 0 (delta 0), pack-reused 19
Unpacking objects: 100% (19/19), done.
```

创建一个分支，分支名为`dev`，并切换到该分支上。

```
git checkout -b dev
```

上述命令相当于如下两条命令：

```
git branch dev
git checkout dev
```

查看当前分支。

```
git branch
```

该命令会列出所有分支，当前分支前会标有一个`*`号。

```
* dev
  master
```

切换回`master`分支。

```
git checkout master
```

把`dev`分支上的内容合并到`master`分支上。

```
git merge dev
```

删除分支。

```
git branch -d dev
```

新创建一个分支dev1，并转到该分支下，然后修改branch.txt中的内容，在dev1分支上提交。

```
λ git checkout -b dev1
Switched to a new branch 'dev1'

λ git add branch.txt

λ git commit -m "dev1"
[dev1 71364e5] dev1
 1 file changed, 1 insertion(+), 1 deletion(-)
```

切换到master上，在master分支上将刚才修改的地方进行二次修改，然后提交。

```
λ git checkout master
Your branch is ahead of 'origin/master' by 1 commits.
  (use "git push" to publish your local commits)
Switched to branch 'master'

λ git add branch.txt

λ git commit -m "master"
[dev1 8c5d810] master
 1 file changed, 1 insertion(+), 1 deletion(-)
```

然后把各自的修改进行合并，此时会出现冲突。

```
λ git merge dev1
Auto-merging branch.txt
CONFLICT (content): Merge conflict in branch.txt
Automatic merge failed; fix conflicts and then commit the result.
```

branch.txt文件存在冲突，需要我们手动解决。执行`git status`命令可以查看到冲突的文件。

```
λ git status
On branch master
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified:   branch.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

查看branch.txt的内容：

```
λ cat branch.txt
创建一个新的分支。

<<<<<<< HEAD
在master上进行修改。
=======
在dev1上进行修改。
>>>>>>> dev1
```

Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容。
你需要删除`<<<<<<< HEAD`，`=======`，`>>>>>>> dev1`这些东西，然后修改你的内容，保存，再提交。

执行`git log --graph`命令可以看见分支合并图。

当你写了一段代码，代码还没写完但是你还不想提交，可是又需要切换到另一个分支时，可以进行暂存修改。

```
git stash
```

如果想要暂存所有修改，则执行`git stash -a`或者`git stash -all`，如果在此基础上还想添加信息，则执行`git stash -a "comment"`。


执行该命令后，Git将stash内容存在了某个地方。

查看stash内容。

```
git stash list
```

想要恢复stash内容，有如下两种方法：

第一种：

```
git stash apply
git stash drop
```

其中，执行`git stash apply`，只是恢复了，但stash内容不会删除，需要用`git stash drop`来删除。

第二种（恢复的同时stash内容也被删了）：

```
git stash pop
```

清除所有stash内容。

```
git stash clean
```

修改作者和邮箱。

```
git config --global user.name "Author Name"
git config --global user.email "Author Email"
```

git的Matching（Git 1.x的默认行为）;
执行`git push`但没有指定分支时，它将push所有你本地的分支到远程仓库中对应匹配的分支。
修改默认设置的命令如下：

```
git config --global push.default matching
```

git的simple模式（Git 2.x的默认行为）：
执行`git push`但没有指定分支时，只有当前分支会被push到你使用`git pull`获取的代码。
修改默认设置的命令如下：

```
git config --global push.default simple
```

其中，`--global`表示全局设置，如果不带该参数，则为本地项目库配置。

上述命令执行完后，执行`git commit --amend --reset-author`。

如果想`git add`所有文件，并且想忽略部分文件的话，可以执行如下操作：
在项目文件下创建一个.gitignore文件或者在命令行中输入`touch .gitignore`来创建；然后打开.gitignore，添加你需要忽略的文件和文件夹，比如：

```
node_modules/
package-lock.json
.gitignore
.vscode/
```

如果你想忽略的文件或文件夹已经提交了，那么需要删除。
比如我要删除`node_modules`文件夹，执行如下操作：

```
git rm -r --cached node_modules
git commit -m "delete node_modules"
git push origin master
```

如果只存在缓存区或本地版本库内，则执行`git reset Head file.name`。

#### 多人协作

本地新建的分支如果不推送到远程，对其他人是不可见的。
从本地推送分支，使用`git push origin branch-name`，如果推送失败，则说明远程分支比你的本地更新，需要先用`git pull`抓取远程的新提交；
如果合并有冲突，则解决冲突，并在本地提交；
在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
使用`git branch --set-upstream branch-name origin/branch-name`建立本地分支和远程分支的关联。

如果使用`git pull`，提示`There is no tracking information for the current branch.`，则说明本地分支的链接关系没有创建，那么就需要执行命令`git branch --set-upstream-to=origin/<branch-name> <branch-name>`。

如果想要git的提交历史是一条干净的直线，则执行命令`git rebase`。
