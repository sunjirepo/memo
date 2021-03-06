# Git 如何恢复删除 .git 文件后的分支

## 问题描述 

手误删除项目中 .git 文件，不想丢失进度。

## 解决

1. 换个目录 git clone 之后再将原文件 copy 一份，并提交（不推荐）
2. git init ; git remote add origin #源地址 ; git pull / add / commit / push 

[参考 segmentfault 问答最后的答案](https://segmentfault.com/q/1010000006796939)


## 后续问题

后续命令 git pull origin master; 会出现 "fatal: refusing to merge unrelated histories"

这是由于本地和远程两个分支 没有共同的commit。（提交记录都被删了.git/）

告知 git 不关心历史 commit 就好（--allow-unrelated-histories）

```shell
git pull origin master --allow-unrelated-histories;
```
