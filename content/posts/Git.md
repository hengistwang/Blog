+++
title = "Git"
author = ["hengist"]
date = 2022-04-11T00:00:00+08:00
lastmod = 2022-04-12T00:17:47+08:00
tags = ["emacs", "orgmode"]
draft = false
+++

## Local {#local}

```nil
git add <file_name>
git commit -m "<message>"
```


### Branch {#branch}

```nil
git branch <branch_name>     #新建branch
git checkout <branch_name>   #切换分支
git merge <branch_name>      #将branch_name 合并到当前分支
```


### Rebase {#rebase}

**rebase合并的方向和merge是相反的**

```nil
git rebase <branch_name>     #将当前分支rebase到branch_name分支
git branch -f branch_name C0 #将branch强行指向C0提交记录
```


### Undo {#undo}

分离出HEAD分支，直接checkout就行了


#### 撤销本地提交 {#撤销本地提交}

让HEAD指向要撤销的提交

```nil
git reset HEAD^ 撤销一次本地提交
```


#### 撤销远程提交 {#撤销远程提交}

先checkout到该分支
然后直接git revert

```nil
git revert <pushed>
```


### 整理提交记录 {#整理提交记录}

```nil
git cherry-pick c3 c4 c7 将这三个节点加到当前分支后面
git rebase -i HEAD~4
```


## Remote {#remote}
