# Java 读源代码看到的问题

在读Java源码中遇到的问题，不管什么情况都可以记录下来，空的时候想想。  
格式：标题是项目，首先是类源代码，然后是问题描述，再后是猜测/解答，最后是记录时间/完全解答时间。  
顺序：最新的问题放在最前面，之前的疑问放在后面。 反复遇到就在最后的记录时间模块里增加再次遇到的时间。  


## 1 logback

### 1.1 Level.java 为什么重复定义 int / Integer？为什么 static final Level 属性不会循环创建内存空间？

```xml
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-core</artifactId>
    <version>1.2.3</version>
</dependency>
```

**Class: ch.qos.logback.classic.Level**

```java
public final class Level implements Serializable {
    private static final long serialVersionUID = -814092767334282137L;
    public static final int OFF_INT = 2147483647;
    public static final int ERROR_INT = 40000;
    public static final int WARN_INT = 30000;
    public static final int INFO_INT = 20000;
    public static final int DEBUG_INT = 10000;
    public static final int TRACE_INT = 5000;
    public static final int ALL_INT = -2147483648;
    public static final Integer OFF_INTEGER = 2147483647;
    public static final Integer ERROR_INTEGER = 40000;
    public static final Integer WARN_INTEGER = 30000;
    public static final Integer INFO_INTEGER = 20000;
    public static final Integer DEBUG_INTEGER = 10000;
    public static final Integer TRACE_INTEGER = 5000;
    public static final Integer ALL_INTEGER = -2147483648;
    public static final Level OFF = new Level(2147483647, "OFF");
    public static final Level ERROR = new Level(40000, "ERROR");
    public static final Level WARN = new Level(30000, "WARN");
    public static final Level INFO = new Level(20000, "INFO");
    public static final Level DEBUG = new Level(10000, "DEBUG");
    public static final Level TRACE = new Level(5000, "TRACE");
    public static final Level ALL = new Level(-2147483648, "ALL");
    public final int levelInt;
    public final String levelStr;

    private Level(int levelInt, String levelStr) {
        this.levelInt = levelInt;
        this.levelStr = levelStr;
    }
}
```

**问题1 为什么重复定义 int / Integer？**

猜测解答：日志可能会执行很多次，Java 自动拆箱，自动装箱肯定比内存消耗大。

**问题2 为什么 static final Level 属性不会循环创建内存空间？**

猜测解答：static 属性类全局只有一份，当发现下一个实例对象创建时不会再申请空间，和JVM内存分配模型有关，和Java ClassLoader策略也有关系。
JVM 和 Java ClassLoader 都不熟悉，需要看看呢。

### 1.1 提问时间 20210319 解答时间 20210319 部分解答。

