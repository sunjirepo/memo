# Git 命令 git add 如何取消暂存文件

场景

    `git add .`之后有某个文件不想提交。 如何从暂存区去除？

## 做法 1
```shell
$ git add *
$ git status
...
  (use "git reset HEAD <file>..." to unstage)
...

$ git reset HEAD file1
$ git status
...
file1 do not in stage
...
```

参考:  
[git-scm 取消暂存的文件](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%92%A4%E6%B6%88%E6%93%8D%E4%BD%9C)

## 做法 2
```shell
$ git add *

$ git add -u
$ git reset -- ${file path}
```

不想 push 部分可以再 stash.

参考：  
[stackoverflow 提问&回答](https://stackoverflow.com/questions/4475457/add-all-files-to-a-commit-except-a-single-file)
