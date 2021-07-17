### Git 命令如何撤销 git pull origin develop


#### 场景

误操作 git pull origin develop


#### 恢复手段 git reset --hard {commit}

法一：

```shell
git reset --hard {commitId}
``` 

如何获取 {commitId}

```shell
git reflog

> fdb70fe HEAD@{0}: {message1}
> 40a9a83 HEAD@{1}: {message2}
``` 

commitId=fdb70fe / commitId=HEAD@{0}

法二（更常见）：

回到某个分支，当前分支会滚到 {branch}，当前分支在此之后的变更统统舍弃

```shell
git reset --hard {branch}
```

eg：

```shell
git checkout preivew
 Switched to branch 'preview'
 Your branch and 'origin/preview' have diverged,
 and have 2 and 50 different commits each, respectively.
   (use "git pull" to merge the remote branch into yours)

# 可以看到当前 preview 分支和远程分支有不一样，且出现冲突
# 我的目标是获取一个干净的原创 preview 分支，而不在乎本地 preview 分支上的代码。于是我执行一下命令
git reset --hard origin/preview
 HEAD is now at eca40ca9 合并分支 'feature_210715' 到 'preview'

git status
On branch preview
Your branch is up to date with 'origin/preview'.

nothing to commit, working tree clean

```

