# Git 如何将{git add .}和{git commit -m "message"}合并成一个命令


1.  一般提交方式

```shell
git add .
git commit -m "some message"
git push
```

2.  合并提交方式
    1. config: 
>$ git config --global alias.add-commit '!git add -A && git commit'

    2. use: 
>	$git add-commit -m 'My commit message'




[link-stackoverflow](https://stackoverflow.com/questions/4298960/git-add-and-commit-in-one-command)
