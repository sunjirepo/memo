## Java 笔试题集合 v1

### Java 笔试题1

给定一棵搜索二叉树，请写出它的中序遍历结果（中序遍历：左子树-根-右子树）
                
![搜索二叉树](https://upload.wikimedia.org/wikipedia/commons/d/da/Binary_search_tree.svg)

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

### Java 笔试题2

给定一个数字类型数组 array 如：[22,11,12,43,54,22,78,90,22]，给定数字k=22，把数组array里的所有k都放到数组最后。

```java
public Integer[] getList(Integer[] array, Integer key) {
    // TODO 待实现
    return null;
}
```

<br/>
<br/>
<br/>
<br/>

### Java 笔试题3

给定一个Integer类型数组 如：[1,2,3,4,5,6,7,8,9,0]，请使用 stream 方式将数组按奇偶区分成 Map<Boolean, List<Integer>>；奇数的Map.key=Boolean.TRUE 偶数的Map.key=Boolean.FALSE。

```java
public Map<Boolean, Integer> getOddEvenMap(Integer[] array) {
    // TODO 待实现
    return null;
}
```

<br/>
<br/>

### (附加题) Java 笔试题4

请实现一个可用支付渠道(微信，支付宝，银联)的列表接口。每种渠道的可用性通过远程服务获取。 在外部资源环境不变情况下，请考虑最短响应时间获得尽可能多的可用列表。

假定可用性查询接口定义：PayRemoteSerivce 方法：ConsultResult isEnabled(String channelType); 返回结果：

```java
public class ConsultResult {
    public ConsultResult(boolean isEnable, String errorCode) {
        this.isEnable = isEnable;
        this.errorCode = errorCode;
    }

    private boolean isEnable;
    private String errorCode;

    public boolean getIsEnable() {
        return isEnable;
    }
    public String getErrorCode() {
        return errorCode;
    }
}
```