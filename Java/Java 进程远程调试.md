### Java 进程远程调试

参考1 [java remote debug](https://www.baeldung.com/java-application-remote-debugging)

参考2 [intellij remote debug](https://www.baeldung.com/intellij-remote-debugging)

#### 1 远程服务器

启动命令和Java参数

```shell
root@xxx# ps -ef | grep application
root     21815     1  0 8月25 ?       00:07:40 java -javaagent:/usr/bin/jacocoagent.jar=includes=*,output=tcpserver,port=7012,address=* -Xms128m -Xmx256m -Dspring.profiles.active=test -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:7015 -jar ./common-application.jar
```

开启远程调试命令， 端口 7015（可自定义）
```shell
java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:7015

```

Tips：address若只写端口默认监听本地

检查端口监听
```shell
root@***# lsof -i:7015
COMMAND   PID USER   FD   TYPE    DEVICE SIZE/OFF NODE NAME
java    21815 root    9u  IPv4 249150564      0t0  TCP *:talon-webserver (LISTEN)
```


#### 2 本地配置 Intellij

Intellij 提供配置，Run/Debug Configration

配置路径 菜单栏 Run -> Edit Configrations... -> 打开配置 左侧选择 Remote 添加配置

Debugger mode=Attach to remote JVM, IP Port 和远程服务器对应。

启动 debug 后 Console 打印 
```shell
Connected to the target VM, address: '{ip}:7015', transport: 'socket'
``` 
表示连接成功。

#### 3 遇到问题 & 解决记录

- 1 Intellij debug 端口连接超时 > 服务器是否开放端口（检查命令 lsof -i:{port}）
- 2 Intellij debug 端口连接拒绝 > 端口监听是否仅监听本地IP（检查命令 lsof -i:{port}）
