### Linux 环境 find 命令

目录及子目录中查找内容。

```shell
find ./ -name '*.ts' | xargs grep "window.URL.revokeObjectURL"
```

上面不对，更新可用的

```shell
find ./ -name '*.md' -print0 | xargs -0 grep "git remote"

.//Linux/Linux 环境 find 命令.md:find ./ -name '*.md' -print0 | xargs -0 grep "git remote"
.//Git/Git 使用代理提速 github（更换代理遇到的问题）.md:> git remote 使用的 ssh 协议头。
.//Git/Git 如何恢复删除 .git 文件后的分支.md:2. git init ; git remote add origin #源地址 ; git pull / add / commit / push

pwd
/xxx/xxx/xx/memo
```