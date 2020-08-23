### 使用 systemctl 管理 java 服务自动重启

1. 目标 

利用 systemctl 启动 java 服务，且机器重启后自动重启。

2. 工具

CentOS 自带的 systemctl 命令工具

3. 示例

jar 目录: /home/root/litemall/litemall/litemall.jar

> 1 创建 systemctl service 脚本
> 2 添加自启链接
> 3 启动

1 systemctl service 脚本


```shell
#!/bin/bash
# 本脚本的作用是停止当前Spring Boot应用，然后再次部署
systemctl litemall stop
ln -f -s /home/root/deploy/litemall/litemall.jar /etc/init.d/litemall
#sudo update-rc.d litemall defaults
#sudo update-rc.d litemall enable
systemctl litemall start
```

2 添加自启链接

3 启动脚本


