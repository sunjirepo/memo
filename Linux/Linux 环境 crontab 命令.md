# Linux 环境 crontab 命令

同理 Mac 环境也是一样。

## 基本命令

    crontab -e ##编辑crontab
    crontab -l ##查看crontab
    crontab -r ##删除crontab
    
    crontab {filename} ##文件创建crontab

## 例子

每天晚上18点执行 git push 备份操作，每天早上10点执行 git pull 操作。

```shell
0 10 * * * sh /Users/***/workdiary/gitpull.sh >/dev/null 2>&1
0 18 * * * sh /Users/***/workdiary/gitpush.sh >/dev/null 2>&1
## * * * * * /bin/date >> /Users/***/tmp.log ##测试用
```

## 其他

Mac 环境下没找到 crontab 的执行日志，一点遗憾。

Mac 还可以使用自有定时任务 launchctl。 好像叫 launchcd ? [tutorial-backups-with-launchd](https://macresearch.org/tutorial-backups-with-launchd/)
