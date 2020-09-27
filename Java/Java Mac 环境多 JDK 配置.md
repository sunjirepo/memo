### Java  Mac 环境多 JDK 配置

参考：

[使用 jenv 管理 Mac jdk 版本 参考](https://codinglife.tech/2019/09/manage-multiple-java-versions-on-mac/)

[jenv 官网](https://www.jenv.be/)

1. 利用 brew 下载多个 openjdk

本地已有openjdk11，再下载一个openjdk8

```shell
$ brew cask install adoptopenjdk/openjdk/adoptopenjdk8
...
location: Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk
install-time: 1598522346
🍺  adoptopenjdk8 was successfully installed!
```

2. 利用 jenv 管理 jdk 并设置 环境 jdk

```shell
$ brew install jenv
...
==> Caveats
To activate jenv, add the following to your ~/.zshrc:

  export PATH="$HOME/.jenv/bin:$PATH"
  eval "$(jenv init -)"
```

jenv 添加本地 Java 地址
```shell
$ jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home
$ jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home

# 检测
$ jenv doctor
[OK]    No JAVA_HOME set
[OK]    Java binaries in path are jenv shims
[OK]    Jenv is correctly loaded
```


3. jenv 选择对应 jdk

```shell
$ jenv versions
* system (set by /Users/jisun/.jenv/version)
  1.8
  1.8.0.265
  11
  11.0
  11.0.7
  openjdk64-1.8.0.265
  openjdk64-11.0.7
```

Configure global version
```shell
$ jenv global 11
$ exec zsh -l 
$ java -version
openjdk version "11.0.7" 2020-04-14
```

Configure local version (per directory)
```shell
$ jenv local 1.8
$ exec zsh -l 
$ java -version
openjdk version "1.8.0_265"
```

Configure shell instance version
```shell
$ jenv shell 1.8
$ java -version
```

