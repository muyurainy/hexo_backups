---
title: github使用
date: 2017-03-29 17:41:53
tags: github
category: 
- 折腾
toc: true
---

# 使用 #
## 提交 ##
    git init  
    git add readme.txt  
    git commit -m "add 3 files."  
    git remote add origin https://github.com/muyurainy/note.git  
    git push -u origin master

## git add常用命令 ##
    git add -i 查看修改
    git add -A 提交所有修改

## git push ##
    $ git push ssh://git@dev.lemote.com/rt4ls.git master // 把本地仓库提交到远程仓库的master分支中

    $ git remote add origin ssh://git@dev.lemote.com/rt4ls.git
    $ git push origin master 

这两个操作是等价的，第二个操作的第一行的意思是添加一个标记，让origin指向ssh://git@dev.lemote.com/rt4ls.git，也就是说你操 作origin的时候，实际上就是在操作ssh://git@dev.lemote.com/rt4ls.git。origin在这里完全可以理解为后者的别名。
