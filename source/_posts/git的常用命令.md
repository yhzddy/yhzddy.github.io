---
title: Git的常用命令
date: 2019-09-15 14:28:16
tags: Git
categories: git
thumbnail: /assets/gg.jpg
---


**git上传常用命令的基本流程**

        git init //初始化git仓库
        git add . //将文件提交到暂存区
        git commit -m '说明'
        git remote add [本地自定义远程仓库名] [远程仓库url]  //建立远程仓库
        git push <远程主机名> <本地分支名>:<远程分支名>


**拉取并合并**

        git pull <远程主机名> <远程分支名>:<本地分支名> 
        git pull=git fetch +git merge 

**推送**

        git push -u origin master //第一次将本地仓库推送到远程仓库
        git push  <远程主机名> <本地分支名>:<远程分支名>

**总结**

        git pull/push <远程主机名> <源地址>:<目的地址>

**常用吗命令**

        git ls-files //查看暂存区文件

        git diff //查看暂存区前后不同

        git branch 分支名 //创建新的分支

        git branch //查看分支

        git branch -r //查看远程的分支名

        git branch --set-upstream-to=<远程主机名>/<远程分支名> <本地分支名> //给该分支设置上游远程节点

        git checkout -b 分支名  //创建新的分支并切换过去

        git checkout 分支名 //切换到该分支

        git init //初始化git仓库

        git add 文件名  //提交该文件

        git add . //提交仓库所有文件

        git commit -m "注释" //提交暂存区的文件到版本库 

        git remote add [本地自定义远程仓库名] [远程仓库url]  //建立远程仓库

        git clone <远程仓库地址>    //克隆该仓库的默认分支

        git clone -b 分支名 <远程仓库地址>   //克隆指定的分支
