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

![image-20231022230147831](D:/PersonalSystem/study%20record/GitHub%E5%85%A5%E9%97%A8.assets/image-20231022230147831.png)

![image-20231023091815498](D:/PersonalSystem/study%20record/GitHub%E5%85%A5%E9%97%A8.assets/image-20231023091815498.png)

```bash
git init #初始化
git config --list #显示当前git配置
git config -e [--global] #编辑配置文件
#设置提交用户信息
git config [--global] user.name "name"
git config [--global] user.email "email"
```

ps: <>必填，[]选填

## clone/fork/branch

fork可代表分叉、克隆出一个仓库的新拷贝，包含了原来的仓库（即upstream repository，上游仓库）所有内容，如分支、Tag、提交。【就是在github里面别人的仓库右上角可以直接fork到自己的主页】

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



## stash



## rebase/merge



## reset revert



## 冲突









