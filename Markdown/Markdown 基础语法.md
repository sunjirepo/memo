# Markdown 基础语法示例

#### 换行

行尾部加空格（会换行）  
下一行

行尾部不加空格（不会换行）
下一行

> 引用部分和基础内容部分一样
> 
> 行尾部加空格（会换行）  
> 下一行
> 
> 行尾部不加空格（不会换行）
> 下一行

    四个空格和其他不一样
    尾部不加两个空格也会自动换行

```shell
# 代码格式和四个空格一样
# 尾部不加两个空格也会自动换行
# 下一行
```

#### 图片

![图片](https://d33wubrfki0l68.cloudfront.net/2585cf9757d316b9030cf36d6a4e6b8ea7eedf5a/1509f/images/docs/user-guide/logging/logging-with-node-agent.png)

#### 脚注

hello[^1]
[^1]: hi

#### 链接注脚

[Google][1]
> 然后在文档的结尾为变量赋值（网址） 
> 
> [1]: http://www.google.com/

#### 分割线

---

***

___

中间加空格

- - -

#### table （已掌握）

|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |


| 左对齐 | 右对齐 | 居中对齐 |
| :-| --: | :---: |
| 单元格 | 单元格 | 单元格 |
| 单 | 单 | 单 |

#### link url 超链接 （已掌握）

[超链接名](超链接地址 "超链接title")

#### ul ui 列表 （已掌握）

- 列表内容
    - 嵌套列表内容
    - 四个空格
+ 列表内容
* 列表内容

1. 列表内容
    1. 有序嵌套列表
    2. 有序嵌套列表
        1. 第三层 
2. 列表内容
3. 列表内容

<ol>
<li>First item</li>
<li>Second item</li>
<li>Third item</li>
<li>Fourth item</li>
</ol>

#### 引用 格式 （已掌握）

> 引用的内容123
> 
> 引用的内容456

##### 引用 格式高阶

> 一层引用
>> 二层引用
>>>三层引用

#### 代码 格式 （已掌握）

```shell
# 这里是 shell 代码
pwd
cd /
pwd
```

```java
// 这里是 java 代码
String s = new String('hello world');
System.out.println(s);
```

[1]: http://www.google.com/
