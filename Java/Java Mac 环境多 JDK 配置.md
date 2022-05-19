### Java  Mac 环境多 JDK 配置

参考：

[使用 jenv 管理 Mac jdk 版本 参考](https://codinglife.tech/2019/09/manage-multiple-java-versions-on-mac/)
[jenv 官网](https://www.jenv.be/)
[jenv READ.me](https://github.com/jenv/jenv/blob/master/README.md)

过程：

1. 利用 brew 下载多个 openjdk

本地已有openjdk11，再下载一个openjdk8

```shell
$ brew install --cask adoptopenjdk/openjdk/adoptopenjdk8
$ brew install --cask adoptopenjdk/openjdk/adoptopenjdk11
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

jenv 已经安装过
```shell
Warning: jenv 0.5.4 is already installed, it's just not linked.
To link this version, run:
  brew link jenv

$ brew link jenv
```

jenv doctor 先检测一下，有些异常需要排除，一般都有说明。
到如下这个阶段就可以进行下一步，添加本地 Java 地址。
```shell
❯ jenv doctor
[OK]  No JAVA_HOME set
[ERROR] Java binary in path is not in the jenv shims.
[ERROR] Please check your path, or try using /path/to/java/home is not a valid path to java installation.
  PATH : /usr/local/Cellar/jenv/0.5.4/libexec/libexec:/Users/sunji/.jenv/shims:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Users/sunji/Library/Python/3.8/bin:/Users/sunji/Library/Python/3.8/bin
[OK]  Jenv is correctly loaded
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
ln: /Users/sunji/.jenv/versions/oracle64-1.8.0.291: No such file or directory



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
$ exec $SHELL -l
$ java -version
openjdk version "11.0.7" 2020-04-14
```

Configure local version (per directory)
```shell
$ jenv local 1.8
$ exec $SHELL -l
$ java -version
openjdk version "1.8.0_265"
```

Configure shell instance version
```shell
$ jenv shell 1.8
$ exec $SHELL -l
$ java -version
```

4 jenv 设置 ${JAVA_HOME}

```shell
# To make sure JAVA_HOME is set, make sure to enable the export plugin:

$ jenv enable-plugin export
$ exec $SHELL -l


$ echo ${JAVA_HOME}
/Users/sunji/.jenv/versions/11

```




