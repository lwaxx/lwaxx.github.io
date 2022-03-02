---
title: 工作中常用到的github命令
date: 2022-03-02 16:05:06
tags: [git, github]
---
工作中常用到的github命令
<!--more-->

## 从master新建分支
> 1.git checkout master                       切换到master分支    
> 2.git pull                                  更新到最新代码    
> 3.git checkout -b dev                       创建新分支并切换到该分支    
> 4.git push origin dev                       推送新分支到远程仓库    
> 5.git branch --set-upstream-to=origin/dev   关联远程仓库    
> 6.git pull                                  尝试拉取验证

## dev分支合并代码到master
> 1.git checkout maste;
> 2.git pull origin master;
> 3.git merge --squash dev;
> 4.git status;
> 5.git stash;  (暂存起来，查看解决的冲突有没有问题)
> 6.git stash pop;
> 7.git diff;   (确认没问题，直接添加)
> 8.git add .;
> 9.git commit -m "feat: xxxx";
> 10.git log;
> 11.git push origin master;

## git rebase（dev--自己， master--想要比对的）
> 1.dev和master分支先更新到最新，然后切换到dev分支；   
> 2.git log;    
> 3.git rebase master;    
> 4.git status;    
> 5.解决冲突;    
> 6.git add [冲突文件]；    
> 7.git rebase --continue;    
> 8.:wq（保存）    
> 9.继续git status;        (重复知道所有冲突解决完)    
> 10.git rebase -i [commit名称（dev分支第一次commit之前的名称，非自己的）];    
> 11.将前面的pick改为f（除了第一次commit的);