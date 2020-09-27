### Linux 环境 比cp命令更好用的rsync

拷贝整个目录下的全部文件的同时不拷贝某些文件

结论：
```shell
rsync -av --progress frontend-tpl-admin/ ai-coach-admin --exclude='node_modules'

# -a 递归同步以外，还可以同步元信息
# -n 模拟执行的结果
# -v verbose 输出执行内容

# --exclude 文档名称 不要用路径，'node_modules' 即可 ‘tenant-product-admin/node_modules' 不对的，别想当然。
```

前端项目 copy, 去掉 node_modules

$ man rsync 
```shell
	-a, --archive               archive mode; same as -rlptgoD (no -H)
        --no-OPTION             turn off an implied OPTION (e.g. --no-D)
	-v, --verbose
	-h, --human-readable        output numbers in a human-readable format
        --progress              show progress during transfer
    -P                          same as --partial --progress
```

PS：对应的 cp 命令（全部拷贝）

```shell
cp -a tenant-product-admin/ servier-admin
```
> 注意 tenant-product-admin 和 tenant-product-admin/ 两者的区别
> 
>  带 / 表示拷贝源目录下的子文件，不带 / 表示包括源目录本身。
>  