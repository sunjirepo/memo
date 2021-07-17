# Git 如何使用 https 替代 ssh

## 原因

公司 vpn 环境下 ssh 无法使用，需用 https 完成。

## 目标

基础目标：vpn 环境下 git 操作拉取 pull 提交 push 都要成功； 
额外目标：最好能静默输入用户名密码（https要求每次提交代码都输入）。

## 过程

实现 基础目标， 实现 额外目标

### 基础目标

```shell
$ git pull
> ssh: connect to host git.intra.xxxxcloud.cn port 22: Operation timed out
> fatal: Could not read from remote repository.

> Please make sure you have the correct access rights
> and the repository exists.
```

更换源

[github managing-remote-repositories][0]

```shell
$ git remote -v
> origin  git@git.intra.xxxxcloud.cn:insurance/medicine/xxxxcloud.git (fetch)
> origin  git@git.intra.xxxxcloud.cn:insurance/medicine/xxxxcloud.git (push)

$ git remote set-url origin https://git.intra.xxxxcloud.cn/insurance/medicine/xxxxcloud.git
$ git remote -v
> origin  https://git.intra.xxxxcloud.cn/insurance/medicine/xxxxcloud.git (fetch)
> origin  https://git.intra.xxxxcloud.cn/insurance/medicine/xxxxcloud.git (push)

```

试一下拉取命令

```shell
$ git pull
> Username for 'https://git.intra.xxxxcloud.cn': myusername
> Password for 'https://myusername@git.intra.xxxxcloud.cn': {mypassword}
> remote: Counting objects: 78, done.
```

成功了！

### 额外目标

[把你的github操作从ssh转成https][1]

```shell
$ git config --global credential.helper osxkeychain

$ git pull
> Already up to date.
```

实现目标！


## 参考

[github managing-remote-repositories][0]

[把你的github操作从ssh转成https][1]

[0]: https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories
[1]: https://molunerfinn.com/git-ssh2https/#%E9%85%8D%E7%BD%AEhttps%E5%85%8D%E8%BE%93%E5%85%A5%E5%AF%86%E7%A0%81
