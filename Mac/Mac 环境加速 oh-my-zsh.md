# Mac 环境加速 oh-my-zsh

原因

进入zsh卡顿，打开新页延迟，cd 进任何目录都能感觉到延迟。 寻找加速。

简单的 "git config --add oh-my-zsh.hide-status 1" 只能在 git 项目目录使用，未能解决问题。

> 在 oh-my-zsh 进入 包含 git 仓库目录时，会变的比平时慢/卡顿
> 原因是因为 oh-my-zsh 要获取 git 更新信息
> 解决办法：
> 设置 oh-my-zsh 不读取文件变化信息（在 git 项目目录执行下列命令）
> $ git config --add oh-my-zsh.hide-dirty 1
> 如果你还觉得慢，可以再设置 oh-my-zsh 不读取任何 git 信息
> $ git config --add oh-my-zsh.hide-status 1
> okey 了，如果想恢复，设置成0就好

[作者：Purson 链接](https://www.jianshu.com/p/bc4b8131db05)


复杂一点的

源自 [JonLuca's Blog](https://blog.jonlu.ca/posts/speeding-up-zsh)

首先 time 命令，描述到底有多慢。 time 命令在 Mac 中没有，但是有替代 gtime。 brew intsall gnu-time

```shell
for i in $(seq 1 10); do time zsh -i -c exit; done
# vs
for i in $(seq 1 10); do time bash -i -c exit; done
```

1.6s vs 0.1s 的区别，差 10x，启动明显卡顿。

特别命令 zsh -xv （x=xtrace/v=verbose)

在 .zshrc 文件头尾添加速度显示后再 打开新 zsh，有如下信息：

.zshrc 头尾添加

```shell
zmodload zsh/zprof

...

zprof
```
输出

```shell
num  calls                time                       self            name
-----------------------------------------------------------------------------------
 1)    1       56785.80 56785.80   99.64%  50353.64 50353.64   88.35%  compinit
 2)    1        5830.36  5830.36   10.23%   5830.36  5830.36   10.23%  compdump
 3)  768         603.02     0.79    1.06%    603.02     0.79    1.06%  compdef
 4)    1         116.08   116.08    0.20%    116.08   116.08    0.20%  handle_completion_insecurities
 5)    1          65.55    65.55    0.12%     65.55    65.55    0.12%  (anon)
 6)    1          10.38    10.38    0.02%     10.38    10.38    0.02%  colors
 7)    2           6.84     3.42    0.01%      6.84     3.42    0.01%  is-at-least
 8)    2           6.72     3.36    0.01%      6.72     3.36    0.01%  add-zsh-hook
 9)    1           0.13     0.13    0.00%      0.13     0.13    0.00%  detect-clipboard
10)    2           0.11     0.05    0.00%      0.11     0.05    0.00%  is_plugin
11)    2           0.06     0.03    0.00%      0.06     0.03    0.00%  env_default
12)    1           0.04     0.04    0.00%      0.04     0.04    0.00%  bashcompinit

-----------------------------------------------------------------------------------
```

可以看到排第一和第二的部分占用了绝大部分时间。

意味着 zsh 本身占据的时间很多。 删掉(disabling source $ZSH/oh-my-zsh.sh from my ~/.zshrc)

去掉以后再执行 zsh 时间下降到和 bash 一样
```shell
 for i in $(seq 1 10); do time zsh -i -c exit; done

# ===== #

num  calls                time                       self            name
-----------------------------------------------------------------------------------
zsh -i -c exit  0.01s user 0.17s system 90% cpu 0.193 total
num  calls                time                       self            name
-----------------------------------------------------------------------------------
zsh -i -c exit  0.01s user 0.17s system 97% cpu 0.181 total
num  calls                time                       self            name
-----------------------------------------------------------------------------------
zsh -i -c exit  0.01s user 0.18s system 86% cpu 0.221 total
num  calls                time                       self            name
-----------------------------------------------------------------------------------
zsh -i -c exit  0.01s user 0.18s system 91% cpu 0.200 total
num  calls                time                       self            name
-----------------------------------------------------------------------------------
zsh -i -c exit  0.01s user 0.16s system 95% cpu 0.179 total
num  calls                time                       self            name
-----------------------------------------------------------------------------------
zsh -i -c exit  0.01s user 0.16s system 94% cpu 0.178 total
num  calls                time                       self            name
-----------------------------------------------------------------------------------
zsh -i -c exit  0.01s user 0.17s system 94% cpu 0.190 total
num  calls                time                       self            name
-----------------------------------------------------------------------------------
zsh -i -c exit  0.01s user 0.17s system 94% cpu 0.190 total
num  calls                time                       self            name
-----------------------------------------------------------------------------------
zsh -i -c exit  0.01s user 0.17s system 91% cpu 0.192 total
num  calls                time                       self            name
-----------------------------------------------------------------------------------
zsh -i -c exit  0.01s user 0.16s system 93% cpu 0.179 total

```

顺便，brew install coreutils (Mac 自带的 date 命令不带毫秒，gdate 带毫秒，`gdate +%s.%N` = 1596432257.235453000)

目前 zsh 只有一个 git 的插件。

修改 /Users/jisun/.oh-my-zsh/oh-my-zsh.sh
```shell

# Load all of the plugins that were defined in ~/.zshrc
for plugin ($plugins); do
  # I use gdate from brew's core-utils because macOS date does not support nanoseconds
timer=$(($(gdate +%s%N)/1000000))

  if [ -f $ZSH_CUSTOM/plugins/$plugin/$plugin.plugin.zsh ]; then
    source $ZSH_CUSTOM/plugins/$plugin/$plugin.plugin.zsh
    now=$(($(gdate +%s%N)/1000000))
    elapsed=$(($now-$timer))
    echo $elapsed":" $plugin
  elif [ -f $ZSH/plugins/$plugin/$plugin.plugin.zsh ]; then
    source $ZSH/plugins/$plugin/$plugin.plugin.zsh
    now=$(($(gdate +%s%N)/1000000))
    elapsed=$(($now-$timer))
    echo $elapsed":" $plugin
  fi
done

```

重启 zsh 结果：

```shell

Last login: Mon Aug  3 13:29:04 on ttys005
31: git

```

额，突然就快起来了。。。啥还没做呢。。。
shit 不知道啥情况， brew update 了一下就好了。。。奇怪

执行重试的命令

```shell
➜  ~ for i in $(seq 1 10); do time zsh -i -c exit; done
22: git
zsh -i -c exit  0.07s user 0.15s system 81% cpu 0.278 total
29: git
zsh -i -c exit  0.07s user 0.18s system 92% cpu 0.264 total
28: git
zsh -i -c exit  0.06s user 0.12s system 90% cpu 0.201 total
22: git
zsh -i -c exit  0.06s user 0.14s system 88% cpu 0.233 total
21: git
zsh -i -c exit  0.06s user 0.07s system 86% cpu 0.161 total
28: git
zsh -i -c exit  0.06s user 0.09s system 88% cpu 0.169 total
33: git
zsh -i -c exit  0.07s user 0.12s system 86% cpu 0.213 total
55: git
zsh -i -c exit  0.06s user 0.20s system 94% cpu 0.282 total
23: git
zsh -i -c exit  0.06s user 0.09s system 86% cpu 0.175 total
24: git
zsh -i -c exit  0.06s user 0.09s system 85% cpu 0.176 total
```

速度在 0.2s 以内，很奇怪。。。待继续排查。
