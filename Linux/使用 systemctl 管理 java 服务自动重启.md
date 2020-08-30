### 使用 systemctl 管理 java 服务自动重启

1. 目标 

利用 systemctl 启动 java 服务，且机器重启后自动重启。

2. 工具

CentOS 自带的 systemctl 命令工具

3. 示例

jar 目录: /home/root/litemall/deploy/litemall/litemall.jar

> 3.1 创建 systemctl service 脚本
> 3.2 添加自启链接
> 3.3 启动
> 3.4 检查

- 3.1 systemctl service 脚本

在 /lib/systemd/system 目录下创建一个脚本文件 litemall.service

litemall.service
```shell
#表示基础信息
[Unit]
#描述
Description=litemall Service
#在哪个服务之后启动
After=syslog.target network.target remote-fs.target nss-lookup.target

#表示服务信息
[Service]
PIDFile=/var/run/litemall.pid
User=root
Group=root
WorkingDirectory=/root/litemall/deploy/litemall
ExecStart=/usr/bin/java -jar /home/root/deploy/litemall/litemall.jar
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

#安装相关信息
[Install]
WantedBy=multi-user.target
```

- 3.2 添加自启链接

创建软链接
```shell
ln -s /lib/systemd/system/litemall.service /etc/systemd/system/multi-user.target.wants/litemall.service

systemctl daemon-reload
systemctl enable litemall.service
```

- 3.3 启动脚本

```shell
#!/bin/bash
# 本脚本的作用是停止当前Spring Boot应用，然后再次部署
systemctl litemall stop
systemctl litemall start
```


- 3.4 查询服务状态
```shell
systemctl status litemall

● litemall.service - litemall Service
   Loaded: loaded (/usr/lib/systemd/system/litemall.service; enabled; vendor preset: disabled)
   Active: active (running) since 日 2020-08-30 14:51:45 CST; 11min ago
 Main PID: 5279 (java)
   CGroup: /system.slice/litemall.service
           └─5279 /usr/bin/java -jar /home/root/deploy/litemall/litemall.jar
```



