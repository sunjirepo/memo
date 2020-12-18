### TypeScript 如何处理类和多态

#### 场景：

某个数据，服务端返回 type + config + value，前端通过 type 区分如何展示 value。

剪除业务逻辑后，type 可分为三种，1 直接显示value，2 config中存有Map<k,v> 按照map.get(value) 来显示，3 通过config中的接口来查询显示

#### 设计：

ViewFactory 类 + ViewInterface 类 + 3个 ViewInstance 类（ ViewDirect ViewMap ViewApi ）。

```js
class ViewFactory {
    static enum = types;
    static viewInstances = Map<type, ViewInterface>;
    static ViewInterface getInstance();
}

class ViewInterface {
    const origin_data;
    translate();
}

class ViewDirect extents ViewInterface{
    translate() {
    }
}

class ViewMap extents ViewInterface{
    translate() {
    }
}

class ViewApi extents ViewInterface{
    translate() {
    }
}
```

#### 实现：


