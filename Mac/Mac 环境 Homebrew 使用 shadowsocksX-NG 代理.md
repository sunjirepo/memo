### Mac 环境 Homebrew 使用 shadowsocksX-NG 代理

#### 月经贴了= = 尝试解决一下问题。。。
[知乎尝试解决](https://zhuanlan.zhihu.com/p/88825725)

[Mac实现终端翻墙](http://locke.ink/post/Mac-Ternimal-Shadowsocks-fanqiang-kexueshangwang/)

#### homebrew

非翻墙环境下 zsh 速度感人
```shell
brew udpate
```
可以执行一辈子


#### 1 .zshrc 配置增加代理

在刚刚打开的.zshrc文件最下方，eval $(thefuck --alias) 这行上面，添加两句代码

```shell
# 开启控制台翻墙
alias proxy='export all_proxy=socks5://127.0.0.1:1086'
alias unproxy='unset all_proxy'
```

这里要注意，127.0.0.1:1086 这个是你shadowsocksX-NG中的偏好设置-高级-本地Socks5监听地址，一定要设置一样的端口号。

测试 proxy 是否成功
```shell
curl cip.cc

IP  : 52.78.86.117
地址  : 韩国  首尔  amazon.com
数据二 : 韩国 | 首尔Amazon数据中心
数据三 :
URL : http://www.cip.cc/52.78.86.117
```

快了一点，或许可以再快一点（.gitConfig）

#### 2 .gitconfig github配置

```shell
# 针对GitHub进行git代理，记得修改代理端口号
[http "<https://github.com>"]
    proxy = socks5://127.0.0.1:1086
```

又快了一点点。


#### 3 验证

```shell
➜  ~ brew cask reinstall adoptopenjdk/openjdk/adoptopenjdk8
==> Downloading https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u265-b
==> Downloading from https://github-production-release-asset-2e65be.s3.amazonaws.com/140418865
###                                                                        4.5%
```

快了一点点，0.1% / 10s 的速度在爬。