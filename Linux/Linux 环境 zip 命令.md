# Linux 环境 zip 命令

zip 压缩和解压缩命令
> -q 安静模式 quit  
> -r 递归 recursion

```shell
zip -q -r html.zip /home/html
# 将 /home/html 目录下的文件打包成 html.zip 文件
```


unzip 解压缩命令
> -l 列出解压文件列表 list
> -v

```shell
unzip -l abc.zip
# 不解压，仅展示压缩包包含文件

unzip abc.zip
# 真正解压文件
```