### Git 命令如何操作分支

git-branch

[git-branch 官方命令](https://git-scm.com/docs/git-branch)

例子：

1. 列出分支 （本地/远程/全部）
> git branch  === git branch --list # 本地分支
> git branch -r # 远程分支
> git branch -a # 全部分支
> 

2. 查询分支
> git branch --list 'master' === git branch --list master
> git branch --list 'dev*'

3. 创建分支
> git branch <newbranch>
> 
> 创建完成后 转移 git switch <newbranch>
> 
> === 等于 git checkout <newbranch>
> 

4. 删除分支
> git branch -d <branchname>
> 