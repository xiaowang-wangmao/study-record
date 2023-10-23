GitHub入门

# 简介

social code 面向社会编程，

## 集中型

## 分布式



# 前期准备

## 注册

去官网注册个账号，设置自己的一些基本信息

（取名好难好麻烦，尽量还是取得简洁且有辨识性，不过后面都是可以修改的）

## 设置SSH Key

以本地为例







# 基本指令

![image-20231022230147831](./GitHub%E5%85%A5%E9%97%A8.assets/image-20231022230147831.png)

![image-20231023091815498](./GitHub%E5%85%A5%E9%97%A8.assets/image-20231023091815498.png)

```bash
git init #初始化
git config --list #显示当前git配置
git config -e [--global] #编辑配置文件
#设置提交用户信息
git config [--global] user.name "name"
git config [--global] user.email "email"
```

ps: <>必填，[]选填

> 整个流程:

```bash
01.git init #在指定文件夹下面创建git的本地仓库
02.git remote add origin url #添加远程仓库
03.git remote -v #查看已有远程仓库
04.git pull #从远程仓库拉取代码并合并本地代码
05.git checkout <branch-name> #切换当前分支
06.git branch -r #查看远程分支
07.git branch -a #查看所有(本地和远程)分支
08.git checkout -b <branch-name> #创建并切换到指定分支
10.git clone -b <branch-name> url #拉取指定分支代码
<---- 提交代码流程 ---->
11.git add . #添加当前目录下的所有文件到暂存区
12.git status #查看文件状态
13.git commit -m"commit message" #将暂存区中的内容提交到本地仓库
14.git push #将当前分支的代码推送到远程分支上
```



## clone/fork/branch

fork可代表分叉、克隆出一个仓库的新拷贝，包含了原来的仓库（即upstream repository，上游仓库）所有内容，如分支、Tag、提交。【就是在github里面别人的仓库右上角可以直接fork到自己的主页】[可以通过发送`pull requests`给上游仓库，看别个接不接受你的更改。git上的项目的一些贡献者或许就是这么来的]

clone克隆，将文件从远程代码仓下载到本地，从而形成一个本地代码仓。默认配置下远程 `Git` 仓库中的每一个文件的每一个版本都将被拉取下来

```bash
git clone <url>
```

branch分支，开启一个新的分支

本地分支关联远程：

```bash
git branch --set-upstream-to=origin/分支名 分支名
```

```bash
git branch #显示所有本地分支
git branch -r #显示所有远程分支
git branch -a #显示所有分支
git branch <new-branch> #新建分支
git branch -d <branch> #删除本地分支
git checkout <branch> #切换分支
```



## add/commit/push

add 把文件添加到暂存区

```bash
git add <file/dir> #添加指定文件/目录
git add . #添加所有文件
git rm <> #删除工作区文件，且放入暂存区
git rm --cached <file> #停止跟踪文件但不删除
```



提交代码commit->推送到远程push

```bash
git commit -m "message" #提交所有更新过的文件
git commit --amend #修改最后一次提交

git remote -v #显示所有远程仓库
git remote add [name] [url] #增加新的远程仓库
git push [remote] [branch] #上传本地指定分支到远程仓库
git push [remote] --force #强行推送，不管冲突
git push [remote] --all #推送所有分支
```



## pull/fetch

- git fetch 命令用于从另一个存储库下载对象和引用，将远程主机的最新内容拉到本地，用户在检查了以后决定是否合并到工作本机分支中.[更安全，在合并前查看冲突并手动解决]



- git pull 命令用于从另一个存储库或本地分支获取并集成(整合),将远程主机的最新内容拉下来后直接合并，即：`git pull = git fetch + git merge`，这样可能会产生冲突，需要手动解决.



```bash
git fetch/pull <远程主机名> <远程分支名>:<本地分支名>
```



## stash

stash，译为存放，在 git 中，可以理解为保存当前工作进度，会把暂存区和工作区的改动进行保存，这些修改会保存在一个栈上，后续可以在任何时候任何分支重新将某次的修改推出来，重新应用这些更改的代码

默认情况下，`git stash`会缓存下列状态的文件：

- 添加到暂存区的修改（staged changes）
- Git跟踪的但并未添加到暂存区的修改（unstaged changes）

但以下状态的文件不会缓存：

- 在工作目录中新的文件（untracked files）
- 被忽略的文件（ignored files）

如果想要上述的文件都被缓存，可以使用`-u`或者`--include-untracked`可以工作目录新的文件，使用`-a`或者`--all`命令可以当前目录下的所有修改

**指令概览**

```bash
git stash #保存当前工作进度，会把暂存区和工作区的改动保存起来

git stash save

git stash list #显示保存进度的列表，git stash命令可以多次执行。小白就不要多次存了

git stash pop #从栈中读取最近一次保存的内容，也就是栈顶的stash会恢复到工作区
git stash pop stashname

git stash apply #将堆栈中的内容应用到当前目录,但不会将内容从堆栈中删除

git stash show #查看堆栈中最新保存的stash和当前目录的差异

git stash drop [name]#移除stash

git stash clear #删除所有存储的进度
```

**应用场景**

1.当你的开发进行到一半,但是代码还不想进行提交 ,然后需要同步去关联远端代码时.如果你本地的代码和远端代码没有冲突时,可以直接通过`git pull`解决

但是如果可能发生冲突怎么办.直接`git pull`会拒绝覆盖当前的修改，这时候就可以依次使用下述的命令：

- git stash
- git pull
- git stash pop

2.当你开发到一半，现在要修改别的分支问题的时候，你也可以使用`git stash`缓存当前区域的代码

- git stash：保存开发到一半的代码
- git commit -m '修改问题'
- git stash pop：将代码追加到最新的提交之后



## rebase/merge

二者都是将一个分支的提交合并到另一分支上。

```bash
git merge xxx #将当前分支合并到指定分支

git rebase -i <commit> #将当前分支移植到指定分支或指定commit之上
git rebase --continue #用于解决冲突之后，继续执行rebase
```

**merge**

通过`merge`合并分支会新增一个`merge commit`，然后将两个分支的历史联系起来

其实是一种非破坏性的操作，对现有分支不会以任何方式被更改，但是会导致历史记录相对复杂

- 如果`bugfix`分支是从`master`分支分叉出来的，如下所示：

![img](GitHub%E5%85%A5%E9%97%A8.assets/88410a30-fdd4-11eb-991d-334fd31f0201.png)

合并`bugfix`分支到`master`分支时，如果`master`分支的状态没有被更改过，即 `bugfix`分支的历史记录包含`master`分支所有的历史记录，所以通过把`master`分支的位置移动到`bugfix`的最新分支上，就完成合并。

- 如果`master`分支的历史记录在创建`bugfix`分支后又有新的提交，如下情况：

![img](GitHub%E5%85%A5%E9%97%A8.assets/929eb220-fdd4-11eb-991d-334fd31f0201.png)

这时候使用`git merge`的时候，会生成一个新的提交，并且`master`分支的`HEAD`会移动到新的分支上，如下图所示，会把两个分支的最新快照以及二者最近的共同祖先进行三方合并，合并的结果是生成一个新的快照。

![img](GitHub%E5%85%A5%E9%97%A8.assets/9fdfa3e0-fdd4-11eb-991d-334fd31f0201.png)



**rebase**

`rebase`会将整个分支移动到另一个分支上，有效地整合了所有分支上的提交

主要的好处是历史记录更加清晰，是在原有提交的基础上将差异内容反映进去，消除了 `git merge`所需的不必要的合并提交。

如果`master`分支的历史记录在创建`bugfix`分支后又有新的提交，如下情况：

![img](GitHub%E5%85%A5%E9%97%A8.assets/ab2d5120-fdd4-11eb-bc6f-3f06e1491664.png)

通过`git rebase`，会变成如下情况：

![img](GitHub%E5%85%A5%E9%97%A8.assets/b72aed70-fdd4-11eb-991d-334fd31f0201.png)

在移交过程中，如果发生冲突，需要修改各自的冲突，`rebase`之后，`master`的`HEAD`位置不变。

![img](GitHub%E5%85%A5%E9%97%A8.assets/c9ba0e80-fdd4-11eb-bc6f-3f06e1491664.png)

因此，要合并`master`分支和`bugfix`分支

![img](GitHub%E5%85%A5%E9%97%A8.assets/dc660660-fdd4-11eb-991d-334fd31f0201.png)

`rebase`会找到不同的分支的最近共同祖先，如上图的`B`节点，然后对比当前分支相对于该祖先的历次提交，提取相应的修改并存为临时文件（老的提交`X`和`Y`也没有被销毁，只是简单地不能再被访问或者使用），然后将当前分支指向目标最新位置`D`, 然后将之前另存为临时文件的修改依序应用。



## reset/revert

**reset**

用于回退版本，可以遗弃不再使用的提交，执行遗弃时，需要根据影响的范围而指定不同的参数，可以指定是否复原索引或工作树内容。

<img src="GitHub%E5%85%A5%E9%97%A8.assets/ab4d0c00-ff72-11eb-bc6f-3f06e1491664.png" alt="img" style="zoom:50%;" />

```bash
#没有指定ID, 暂存区的内容会被当前ID版本号的内容覆盖，工作区不变
git reset
#指定ID，暂存区的内容会被指定ID版本号的内容覆盖，工作区不变
git reset <ID> 

git log #查询日志ID
```

**revert**

在当前提交后面，新增一次提交，抵消掉上一次提交导致的所有变化，不会改变过去的历史，主要是用于安全地取消过去发布的提交

<img src="GitHub%E5%85%A5%E9%97%A8.assets/bd12c290-ff72-11eb-991d-334fd31f0201.png" alt="img" style="zoom:50%;" />

```bash
git revert <commit_id>
git revert HEAD #撤销前一个版本
get revert HEAD^ #撤销前前版本
```

重设完全地移除了一堆更改，而撤销保留了原来的更改，用一个新的提交来实现撤销

**主要区别**

- git revert是用一次新的commit来回滚之前的commit，git reset是直接删除指定的commit
- git reset 是把HEAD向后移动了一下，而git revert是HEAD继续前进，只是新的commit的内容和要revert的内容正好相反，能够抵消要被revert的内容
- 在回滚这一操作上看，效果差不多。但是在日后继续 merge 以前的老版本时有区别

> git revert是用一次逆向的commit“中和”之前的提交，因此日后合并老的branch时，之前提交合并的代码仍然存在，导致不能够重新合并
>
> 但是git reset是之间把某些commit在某个branch上删除，因而和老的branch再次merge时，这些被回滚的commit应该还会被引入

- 如果回退分支的代码以后还需要的情况则使用`git revert`， 如果分支是提错了没用的并且不想让别人发现这些错误代码，则使用`git reset`



## 冲突

多个分支修改了同一个文件（任何地方）或者多个分支修改了同一个文件的名称 就会产生冲突

当`Git`无法自动合并分支时，就必须首先解决冲突，解决冲突后，再提交，合并完成。

解决冲突就是把`Git`合并失败的文件手动编辑为我们希望的内容，再提交









