### Git 命令统计提交代码行数

#### 一些 git log 命令
```shell
git log --author="username" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }' -
```
```shell
git log --format='%aN' | sort -u | while read name; do echo -en "$name\t"; git log --author="$name" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }' -; done
```

#### gitstats 工具，貌似蛮有趣。

[gitstats 官网](http://gitstats.sourceforge.net/)

[gitstats python3版本](https://github.com/hanzhichao/gitstats)

Mac 安装
```shell
brew install --HEAD homebrew/head-only/gitstats
# 不行了，官网不维护， head-only 不能用。
```
> 安装依赖：Git，Python，Gnuplot。
> 所以直接安装以上三个软件即可, Mac 自带 python 2.7 (正好也是需要使用的版本)
> 一般项目肯定有 git
> 

```shell
# brew install git
# brew install python
brew install gnuplot
```

clone 目标软件 gitstats
```shell
git clone git://github.com/hoxu/gitstats.git
```

进入 gitstats 目录并执行操作
```shell
$ cd gitstats

$ cp gitstats gitstats.py

$ python gitstats.py ../xxx_pro/ ./test
# ../xxx_pro/ 为工程所在目录。
# ./test 为结果文件目录。
```

生成报告目录 ./test；入口 ./test/activity.html。
