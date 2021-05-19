# Java 面试题+笔试题+开放式问题 v2

Java面试题 1 - 集合 HashMap

    HashMap都用过，get和put是基本方法，HashMap是如何构建的，保证get/put效率
    加试：为什么会出现Hash冲突，如何避免？或者说 hash 冲突怎么解决的。


Java面试题 2 - 锁 synchronized ReentrantLock 分布式锁

    Java中有哪些锁？能举例说说吗？ 什么时候用到过？  有没有了解过分布式锁。
    加试：CAP原理，ReentrantLock 实现。

Java面试题 3 - 数据库 索引/B+树/锁

    最左匹配 - Like 能不能走索引？
    唯一约束+逻辑删除 - 多次插入同一个，删了以后能再次插入，能再次删除。

Java面试题 4 - 幂等，锁，并发，数据库

    积分兑换服务权益，每个人只能兑换一个？
    哪些环节容易遇到问题？ 怎么解决
        （前端页面，提交以后不可点击，转圈loading）
        （相同HTTP请求，分布式锁，扣减加唯一ID）
        （数据库唯一约束）
    加试：有没有更简单的做法？


Java面试题 5 - 微服务
    
    用过或者了解过微服务吗？ 在你了解的微服务体系中，服务发现和服务治理是如何做到的？
    假如实际开发过程中，碰到服务下线，如何快速定位问题。（接口调用什么错误？ 注册中心查看服务注册情况）

Java面试题 6 - 消息中间件

    用过哪些消息中间件？ 
    为什么需要用到消息？ 是否保证一定送达？ 消息消费的时候需要保证幂等，请问为什么需要做到幂等？幂等有什么好处？ 如何做到幂等（唯一性约束）？

Java面试题 7 - 日志/异常

    如何保证线上服务运行平稳？或者说出现问题如何能够快速定位？
    打日志，日志收集，统一日志平台。 监控系统。
    平时查询线上日志用什么？

Java笔试题 1 - 并发，阻塞，缓存

    实现一个提供可用支付渠道的接口。
    外部系统有多种支付渠道（微信，支付宝，银联，各家银行等），假如每种渠道的可用性需要通过调用远程服务获取。 
    在外部资源环境不变情况下，如何编写能够以最短响应时间获得尽可能多的可用支付渠道。

    假定支付渠道的可用性咨询接口定义：PaymentRemoteSerivce 接口方法：ConsultResult isEnabled(String channel); 返回结果：

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

    踩点答案：
    
    尽可能多 =》 阻塞 + 超时
    最短时间 =》 FurtureAndCallable / 线程池 多线程用起来

Java笔试题 2 - 循环，算法 （二选一吧）

    简单算法题： 给一个数组，数字=k，把这个数组里面的所有K 都放在数组最后。
    难一点算法题： 单链表反转。（更快的方式难讲清楚，写代码好了）
    无法笔试的话就讲讲思路。

    已知：2开方1.414，如何把结果精确到10位小数。
    讲讲思路，复杂度（时间复杂度，空间复杂度）

开放性问题：

    新知，最近有学什么新东西吗？

    平时遇到技术问题怎么解决？

    对公司有什么问题需要问？ （团队， 业务， 赛道）

