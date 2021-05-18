# Java面试题集合


Java面试题1 - 幂等，锁，并发

    积分兑换奖励，每个人只能兑换一个，如何保证每个人用户只能兑换一个奖励？
    （前端loading页面）
    （多次HTTP请求）
    （数据库幂等）
    加试：有没有更简单的做法？

Java面试题2 - 单例

    Spring 框架中有没有单例的实践？ 平时是如何用的？ 为什么需要单例，单例有什么作用？ 
    加试：Spring如何实现单例？如果有两个类名称一样的@Service会不会有问题？

Java面试题3 - 集合

    HashMap都用过，get和put是基本方法，HashMap是如何构建的，保证get/put效率
    加试：为什么会出现Hash冲突，如何避免？或者说 hash 冲突怎么解决的。


Java面试题4 - 并发

    ConcurrentHashMap 用到过吗？ 什么业务场景用到？ 合理性。

Java面试题7 - 数据库 索引/B+树/锁

    上述用户病症信息表数量很多，如何能够查的更快？假如有用户病症信息表需要按照疾病名称和指标查询，如何设计索引？ 
    加试：疾病名称很长怎么办？
    如何利用 MySQL 实现乐观锁？
    聊一聊 MySQL 的锁级别？ 
    额外：为什么会出现表锁？ 如何避免？


Java面试题8 - 微服务
    
    用过或者了解过微服务吗？ 微服务的注册中心是什么？ 在你了解的微服务体系中，服务发现和服务治理是如何做到的？

Java面试题9 - 消息中间件

    用过哪些消息中间件？ 
    为什么需要用到消息？ 是否保证一定送达？ 消息消费的时候需要保证幂等，请问为什么需要做到幂等？幂等有什么好处？ 如何做到幂等（唯一性约束）？

    消息消费是否保证顺序？保证顺序和不保证顺序有什么区别。

Java面试题10 - 日志/异常

    如何保证线上服务运行平稳？或者说出现问题如何能够快速定位？
    打日志，日志收集，统一日志平台。 监控系统。
    平时查询线上日志用什么？

Java笔试题1 - 并发，阻塞，缓存

面试系统有多种面试途径（音频、视频、人机对话等），假如每种面试途径的可用性需要通过调用远程服务获取。 在外部资源环境不变情况下，请编写一个方法以最短响应时间获得尽可能多的可用面试途径列表。
假定面试途径的可用性咨询接口定义：InterviewRemoteSerivce 接口方法：ConsultResult isEnabled(String interviewType); 返回结果：

```java
public class ConsultResult {
    public ConsultResult(boolean isEnable, String errorCode) {
        this.isEnable = isEnable;
        this.errorCode = errorCode;
    }
    /**
     * 咨询结果是否可用
     */
    private boolean isEnable;
    /**
     * 错误码
     */
    private String errorCode;
    
    public boolean getIsEnable() {
        return isEnable;
    }
    public String getErrorCode() {
        return errorCode;
    }
}
```

Java 笔试题2 - 循环，算法

    简单算法题： 给一个数组，数字=k，把这个数组里面的所有K 都放在数组最后。
    讲讲思路。

开放性问题：

    新知，最近有学什么新东西吗？

    对公司有什么问题需要问？

