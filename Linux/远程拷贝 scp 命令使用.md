### 远程拷贝 scp 命令使用 

#### 复制本地目录到远程

```shell
scp -r  ./deploy root@xx.xx.xxx.xxx:/home/root/

# -r： 递归复制整个目录。
# -i identity_file： 从指定文件中读取传输时使用的密钥文件，此参数直接传递给ssh。
# -i ssh 登陆方式使用。
```

#### 复制远程数据到本地

```shell
# scp -r www.runoob.com:/home/root/others/ /home/space/music/
# -r 表示递归。
scp readonly@49.235.228.23:/var/tmp/common-gateway.jar /Users/jisun/Desktop
```
执行还是在本地，即 /Users/jisun/Desktop 所在的机器。

[参考 菜鸟教程](https://www.runoob.com/linux/linux-comm-scp.html)