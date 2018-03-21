## 索引
1. **创建**
1. **本地修改**
1. **提交历史**
1. **分支与标签**
1. **更新与发布**
1. **合并与重置**
1. **撤销**
1. **工作区，版本库(暂存区-stage，分支-master)图**
1. **创建与合并分支图**
1. **branches图**
1. **git folw图**
---
### 创建

复制一个已创建的仓库
```sh
$ git clone ssh://user@domain.com/repo.git
```
创建一个新的本地仓库
```sh
$ git init
```
---
### 本地修改

显示工作路径下已修改的文件：
```sh
$ git status
```
显示与上次提交版本文件的不同：
```sh
$ git diff
```
把当前所有修改添加到下次提交中：
```sh
$ git add .
```
把对某个文件的修改添加到下次提交中：
```sh
$ git add -p <file>
```
提交本地的所有修改：
```sh
$ git commit -a
```
提交之前已标记的修改：
```sh
$ git commit
```
附加消息提交：
```sh
$ git commit -m 'message here'
```
修改上次提交

*请勿修改已发布的提交记录!*
```sh
$ git commit --amend
```
---
### 提交历史

从最新提交开始，显示所有的提交记录（显示hash， 作者信息，提交的标题和时间）：
```sh
$ git log
```
显示所有提交（仅显示提交的hash和message）：
```sh
$ git log --oneline
```
显示某个用户的所有提交：
```sh
$ git log --author="username"
```
显示某个文件的所有修改：
```sh
$ git log -p <file>
```
谁，在什么时间，修改了文件的什么内容：
```sh
$ git blame <file>
```
---
### 分支与标签

列出所有的分支：
```sh
$ git branch
```
切换分支：
```sh
$ git checkout <branch>
```
基于当前分支创建新分支：
```sh
$ git branch <new-branch>
```
基于远程分支创建新的可追溯的分支：
```sh
$ git branch --track <new-branch> <remote-branch>
```
删除本地分支:
```sh
$ git branch -d <branch>
```
给当前版本打标签：
```sh
$ git tag <tag-name>
```
---
### 更新与发布

列出对当前远程端的操作：
```sh
$ git remote -v
```
显示远程端的信息：
```sh
$ git remote show <remote>
```
添加新的远程端：
```sh
$ git remote add <remote> <url>
```
下载远程端版本，但不合并到HEAD中：
```sh
$ git fetch <remote>
```
下载远程端版本，并自动与HEAD版本合并：
```sh
$ git remote pull <remote> <url>
```
将远程端版本合并到本地版本中：
```sh
$ git pull origin master
```
将本地版本发布到远程端：
```sh
$ git push remote <remote> <branch>
```
删除远程端分支：
```sh
$ git push <remote> :<branch> (since Git v1.5.0)
or
git push <remote> --delete <branch> (since Git v1.7.0)
```
发布标签:
```sh
$ git push --tags
```
---
### 合并与重置

将分支合并到当前HEAD中：
```sh
$ git merge <branch>
```
将当前HEAD版本重置到分支中:

*请勿重置已发布的提交!*
```sh
$ git rebase <branch>
```
退出重置:
```sh
$ git rebase --abort
```
解决冲突后继续重置：
```sh
$ git rebase --continue
```
使用配置好的merge tool 解决冲突：
```sh
$ git mergetool
```
在编辑器中手动解决冲突后，标记文件为已解决冲突
```sh
$ git add <resolved-file>
$ git rm <resolved-file>
```
---
### 撤销

放弃工作目录下的所有修改：
```sh
$ git reset --hard HEAD
```
移除缓存区的所有文件（i.e. 撤销上次git add）:
```sh
$ git reset HEAD
```
放弃某个文件的所有本地修改：
```sh
$ git checkout HEAD <file>
```
重置一个提交（通过创建一个截然不同的新提交）
```sh
$ git revert <commit>
```
将HEAD重置到上一次提交的版本，并放弃之后的所有修改：
```sh
$ git reset --hard <commit>
```
将HEAD重置到上一次提交的版本，并将之后的修改标记为未添加到缓存区的修改：
```sh
$ git reset <commit>
```
将HEAD重置到上一次提交的版本，并保留未提交的本地修改：
```sh
$ git reset --keep <commit>
```
-----
### 工作区，版本库(暂存区-stage，分支-master)
![工作区，版本库(暂存区-stage，分支-master)](https://i.loli.net/2018/03/22/5ab290177394c.png)
### 创建与合并分支
[![创建与合并分支](https://i.loli.net/2018/03/22/5ab2920304401.png)](https://i.loli.net/2018/03/22/5ab2920304401.png)
[![创建与合并分支2](https://i.loli.net/2018/03/22/5ab29203e613a.png)](https://i.loli.net/2018/03/22/5ab29203e613a.png)
###  分支
[![branches](https://i.loli.net/2018/03/22/5ab292e70a55b.png)](https://i.loli.net/2018/03/22/5ab292e70a55b.png)
### git folw
[![flow.png](https://i.loli.net/2018/03/22/5ab2938813a88.png)](https://i.loli.net/2018/03/22/5ab2938813a88.png)


#### 参考

[Git Cheat Sheet 中文版](https://github.com/flyhigher139/Git-Cheat-Sheet)

[Git教程 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)  
