### Mac 环境多 JDK 配置

1. 利用 brew 下载多个 openjdk

```shell
root# brew cask install adoptopenjdk/openjdk/adoptopenjdk8
root# brew cask install adoptopenjdk/openjdk/adoptopenjdk13
```

2. 利用 jenv 管理 jdk 并设置 环境 jdk

```shell
brew install jenv
```

[参考](https://codinglife.tech/2019/09/manage-multiple-java-versions-on-mac/)

检验 jdk 是否生效

3. 使用 jenv 选择对应 jdk 版本

```shell
``` 