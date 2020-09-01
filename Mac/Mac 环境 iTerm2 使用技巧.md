### Mac 环境 iTerm2 使用技巧

#### 快捷键

> 分屏
> 
> command + D; 横向分
> 
> command + shift + D; 纵向分
> 
> 关闭分屏（关闭当前屏幕）
> 
> command + W;
> 
> 分屏切换
> 
> command + [ 或 command + ]
> 

#### 自带功能功能

> Profile -- 使用 shell 脚本 生成屏幕
> 
> 菜单 -> Profiles -> Open Profiles -> Edit Profiles
> 
> Command 选择 Login Shell
> 
> Send text at start: "expect /Users/jisun/shell/litemall_login_dev.sh"
> 
> 自动登陆脚本 litemall_login_dev.sh
> 
```shell
#!/usr/bin/expect
set user ${user}
set password ${password}
set host ${ip}
set port 22
set timeout -1
spawn ssh $user@$host
expect "password:"
send "$password\r"
interact
```
> 
> "interact" 表示登陆后交回控制权