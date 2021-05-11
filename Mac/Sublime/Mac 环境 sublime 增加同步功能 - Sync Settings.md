# Mac 环境 sublime 增加同步功能 - Sync Settings

## Sublime 配置备份

[利用插件 Sync Settings](https://packagecontrol.io/packages/Sync%20Settings)

先安装 Sync Settings 再将 SyncSettings 的 Users 配置写
```json
{
    "access_token": "xxxxxx",
    "gist_id": "xxxxxx"
}
```

## Sublime 插件备份

已经下载的插件用Github Repo保证备份。

Mac 目录：
/Users/jisun/Library/Application Support/Sublime Text 3

Github Repo 目录：
git@github.com:sunjirepo/sublime-packages.git

操作
```shell

cd /Users/jisun/Library/Application Support/Sublime Text 3
git init
git remote add origin git@github.com:sunjirepo/sublime-packages.git
git pull origin master

```