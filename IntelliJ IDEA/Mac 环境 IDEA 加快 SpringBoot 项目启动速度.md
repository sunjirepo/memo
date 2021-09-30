# Mac 环境 IDEA 加快 SpringBoot 项目启动速度

## 启动查找域名时间 5s

InetAddress.getLocalHost().getHostName() took 5002 milliseconds to respond. Please verify your network configuration

在本机 hosts 文件中增加机器名{xxx.local}寻址。

```shell
$ hostname

$ vim /etc/hosts

127.0.0.1       localhost xxx.local
255.255.255.255 broadcasthost
::1             localhost xxx.local

```

结果, 启动时间 -5s

[参考文档](https://blog.csdn.net/yzh_1346983557/article/details/117626167)