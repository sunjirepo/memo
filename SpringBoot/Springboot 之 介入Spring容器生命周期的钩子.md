### Springboot 之 介入Spring容器生命周期的钩子

#### 需求
初始化阶段 将数据库配置数据和用户数据做比较，确定初始Atomic值，程序进行过程中Atomic增加。

#### 实现

关键代码
```java
@Component
@Order(0)
public class InvitationApplicationListener implements ApplicationListener<ApplicationReadyEvent> {

    @Resource
    private IActInvitationService invitationService;
    @Resource
    private IActInvitationCfgService invitationCfgService;

    @Override
    public void onApplicationEvent(ApplicationReadyEvent event) {
        log.info("初始化 邀请编码 开始");
        List<ActInvitationCfg> configs = invitationCfgService.list();
        for (ActInvitationCfg config : configs) {
            ActInvitation max = invitationService.getOne(Wrappers.<ActInvitation>query()
                    .eq("title", config.getTitle())
                    .orderByDesc("updated_at")
                    .last("limit 1")
            );
            InvitationContext.init(config.getTitle(), max, config);
            log.info("邀请活动={} 编码初始中 invitation={}, config={}",
                    config.getTitle(),
                    JSON.toJSONString(max),
                    JSON.toJSONString(config));
        }
        log.info("初始化 邀请编码 完成");
    }
}
```

#### 原理
通过 SpringBoot 提供的 events-listener 方式在生命周期中间增加业务代码。
[spring 官网 ](https://docs.spring.io/spring-boot/docs/2.1.9.RELEASE/reference/html/boot-features-spring-application.html#boot-features-application-events-and-listeners)

> Application events are sent in the following order, as your application runs:
> 
> 1. An ApplicationStartingEvent is sent at the start of a run but before any processing, except for the registration of listeners and initializers.
> 2. An ApplicationEnvironmentPreparedEvent is sent when the Environment to be used in the context is known but before the context is created.
> 3. An ApplicationPreparedEvent is sent just before the refresh is started but after bean definitions have been loaded.
> 4. An ApplicationStartedEvent is sent after the context has been refreshed but before any application and command-line runners have been called.
> 5. An ApplicationReadyEvent is sent after any application and command-line runners have been called. It indicates that the application is ready to service requests.
> 6. An ApplicationFailedEvent is sent if there is an exception on startup.

这里用到的是 ApplicationReadyEvent， 应用已经可以提供服务的时候初始化业务数据。
（同时初始化依赖数据库和Service Component）


TIPS：其他单个Bean启动的时候介入生命周期 可以更精细，在单个bean里控制即可。