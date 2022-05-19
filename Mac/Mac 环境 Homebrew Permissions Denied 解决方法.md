# Mac 环境 Homebrew Permissions Denied 解决方法


## Homebrew Permissions Denied Issues Solution
```shell
$ sudo chown -R $(whoami) $(brew --prefix)/*
```

Thanks to [Homebrew Permissions Denied Issues Solution](https://gist.github.com/irazasyed/7732946)