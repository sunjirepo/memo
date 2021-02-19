### Git 使用代理提速 github （更换代理遇到的问题）

#### 更换代理端口遇到的问题

从 SSR 更换到 ClashX，代理端口有变化。

shell && gitconfig 代理已更换，但项目和远程通信还是有问题，执行
```shell
$ git fetch # 或者 git pull
```
有以下报错
> nc: connect to 127.0.0.1 port 1086 (tcp) failed: Connection refused
kex_exchange_identification: Connection closed by remote host
fatal: Could not read from remote repository.
> Please make sure you have the correct access rights
and the repository exists.

原来：ssh 也有代理需要配置

```shell
$ less ~/.ssh/config

# --- Sourcetree Generated ---
Host xxxx
        HostName github.com
        User xxxx
        PreferredAuthentications publickey
        IdentityFile /Users/xxxx/.ssh/xxxx
        UseKeychain yes
        AddKeysToAgent yes

Host github.com
        HostName github.com
        User git
        ProxyCommand nc -v -x 127.0.0.1:1086 %h %p
# ----------------------------
```

将 ProxyCommand nc -v -x 127.0.0.1:1086 %h %p 端口改为新端口即可。

原因大约是 git clone 项目用的 ssh 协议。

一开始花时间在 gitconfig 和 zsh 本身的代理，误入歧途。

> 关注点1 报错信息开头有 'nc' 表示 netcat 和一般的 gitconfig 代理错误不一样
> 关注点2 报错信息 kex_exchange_identification 和权限相关，联想 ssh
> 关注点3 
```shell
$ git config -l | grep remote
remote.origin.url=git@github.com:xxxx/xxxx.git
```
> git remote 使用的 ssh 协议头。

