# Git 如何将本地代码合到远程分支

### 问题描述

远端新建 Git 项目（github 或者 gitlab），模版代码中只有 read.me 等文件。 本地用 SpringBoot Initialer 生成工程模版代码，如何能够将本地代码合并到远程分支上去呢？

### 解决

[两种解决思路](https://www.jianshu.com/p/c907fa80ab6b)

1 git clone 后，再手动copy。

2 利用 git 远程分支。

- 1 git clone 后，再手动copy。
```shell
$ cp -r dir1 dir2 # dir2 不存在
$ cp -r dir1/. dir2 # dir2 存在
```

- 2 利用 git 远程分支。
TODO