### Git 命令如何撤销 git pull origin develop


#### 场景

误操作 git pull origin develop


#### 恢复手段 git reset --hard

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