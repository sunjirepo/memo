# Git 命令基本操作.md


## 删除分支

查看远程分支
```shell
$ git branch -a
```

删除远程分支
```shell
$ git push origin --delete <branchName>
```

删除本地分支
```shell
$ git branch -d <branchName>
```