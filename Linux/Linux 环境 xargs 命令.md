# Linux 环境 xargs 命令

参考：[阮一峰的xargs解释][1]

## xargs命令的作用，是将标准输入转为命令行参数。

## 例子

### xargs 配合 管道 ｜
打印内容
```shell
$ echo "hello world" | xargs echo
hello world
```

创建文件夹
```shell
$ echo "one two three" | xargs mkdir
## 上面的代码等同于mkdir one two three
```

### xargs 单独使用

xargs后面的命令默认是echo。
```shell
$ xargs
hello (Ctrl + d)
hello
```

```shell
$ xargs find -name
"*.txt"
./foo.txt
./hello.txt
```


[1]: https://www.ruanyifeng.com/blog/2019/08/xargs-tutorial.html