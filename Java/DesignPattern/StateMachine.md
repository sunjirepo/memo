# StateMachine 状态机

实际工作遇到利用状态机业务，抽取核心代码，学习理解状态机。

## 分析各种状态机角色

StateMachine包内类图：
![StateMachine 图][0]

- [x] 1. StateMachineFactory 状态机工厂
- [x] 2. StateMachine 状态机
- [x] 3. StateMachineConfig 状态机配置
- [ ] 4. StateConfigration 状态配置
- [ ] 5. AbstractHandler 抽象操作类
- [ ] 6. XXXHandler 具体操作类实现
- [x] 7. TransactionContext 状态机操作上下文
- [ ] 8. BaseStateMachineKey 上下文数据Key  
- [x] 9. HcStateMachineInit AiStateMachineInit SpringBoot初始化


### 入口类：

依赖 Spring 做类实例管理。

HcStateMachineInit 和 AiStateMachineInit 两个类作用类似，初始化 HC 和 AI 业务的状态机，以 HC 为例

```java
@Service
public class HcStatemachineInit {

  /** 初始化状态机 */
  @PostConstruct
  public void init() {
    StateMachineFactory.register(ServicePlanServeTypeEnum.hc, buildCallStateMachine());
  }

  /**
   * 服务包状态机
   *
   * @return
   */
  private StateMachine buildCallStateMachine() {
    StateMachineConfig<ServicePlanStatusEnum, ServicePlanEventEnum, Handler> stateMachineConfig =
        new StateMachineConfig();

    /** 创建服务 */
    stateMachineConfig
        .from(ServicePlanStatusEnum.zero)
        .permit(ServicePlanEventEnum.createServcie)
        .handle(createHandler)
        .to(ServicePlanStatusEnum.waitActivate)
        .build();

    /** 激活服务 */
    stateMachineConfig
        .from(ServicePlanStatusEnum.waitActivate)
        .permit(ServicePlanEventEnum.activate)
        .handle(activateServiceHandler)
        .to(ServicePlanStatusEnum.waitStart)
        .build();

    /** 服务启动 */
    stateMachineConfig
        .from(ServicePlanStatusEnum.waitStart)
        .permit(ServicePlanEventEnum.startService)
        .handle(startServiceHandler)
        .to(ServicePlanStatusEnum.managing)
        .build();

    /** 服务到期 */
    stateMachineConfig
        .from(ServicePlanStatusEnum.managing)
        .permit(ServicePlanEventEnum.due)
        .handle(dueHandler)
        .to(ServicePlanStatusEnum.done)
        .build();

    /** 订单关闭 */
    stateMachineConfig
        .from(ServicePlanStatusEnum.unknown)
        .permit(ServicePlanEventEnum.closeOrder)
        .handle(closeOrderHandler)
        .to(ServicePlanStatusEnum.close)
        .build();

    /** 过期 */
    stateMachineConfig
        .from(ServicePlanStatusEnum.waitActivate)
        .permit(ServicePlanEventEnum.expire)
        .handle(expireHandler)
        .to(ServicePlanStatusEnum.expire)
        .build();

    return new StateMachine(stateMachineConfig);
  }
```

主要是向工厂类注册状态机。 
```java
StateMachineFactory.register(ServicePlanServeTypeEnum.hc, buildCallStateMachine());
```

### 状态机工厂和状态机

StateMachineFactory#register 方法的实现比较简单，类拥有一个静态Map对象

```java
public final class StateMachineFactory {

  private static Map<Enum, StateMachine<Object, Object, Handler>> stateMachineMap = new HashMap<>();

  private StateMachineFactory() {}

  public static void register(Enum key, StateMachine stateMachine) {
    stateMachineMap.put(key, stateMachine);
  }

  public static StateMachine<Object, Object, Handler> getStateMachine(ServicePlanServeTypeEnum key) {
    return stateMachineMap.get(key);
  }
}
```

工厂类被 final 修饰且构造方法私有，操作均通过类静态方法和静态对象实现。

```java
@Slf4j
public class StateMachine<S, E, H extends Handler> {

  private final StateMachineConfig<S, E, H> stateMachineConfig;

  public StateMachine(StateMachineConfig<S, E, H> config) {
    this.stateMachineConfig = config;
  }

  public ServicePlan fire(E event, TransactionContext context) throws Exception {
    S mainStateEnum = (S) context.getData(BaseStateMachineKey.CURRENT_STATE);
    if (null == mainStateEnum) {
      throw new HttpGlobalError("未找到当前状态，状态机无法继续");
    }
    H handle = stateMachineConfig.getHandle(mainStateEnum, event);
    if (handle == null) {
      log.info("状态和指令不匹配,state={},event={}", mainStateEnum, event);
      throw new HttpGlobalError(
          String.format(
              "当前服务已为"
                  + ServicePlanStatusEnum.dataMap.get(mainStateEnum.toString()).getMsg()
                  + "状态,无法操作,请刷新页面尝试"));
    }
    S nextState = stateMachineConfig.getNextState(mainStateEnum, event);
    context.setData(BaseStateMachineKey.NEXT_STATE, nextState);
    log.info(
        "[StateMachine] runing currentState=[{}], event=[{}], handle=[{}], nextState=[{}]",
        mainStateEnum,
        event,
        handle.getClass().getSimpleName(),
        nextState);
    return handle.doHandle(context, this, (ServicePlanEventEnum) event);
  }
}

```

状态机对象持有一个 StateMachineConfig， 对外提供一个 fire 方法，用于驱动状态机流转。

fire 方法实现：从外部获取事件 Event 和 当前状态（存在 TransactionContext.getData(CURRENT_STATE)），同时将状态机自身的下一个状态（StateMachineConfig.getNextState）塞入上下文 TransactionContext，然后将以上三种信息交给具体执行（StateMachineConfig.getHandle(state, event))

### 状态机的具体操作类：

以 CreateHandler 为例
```java
@Slf4j
@Service
public class CreateHandler extends AbstractHandler {
  
  @Override
  @Transactional(rollbackFor = Exception.class)
  // ... 做创建 CreateHandler 自己的业务
  public ServicePlan handle(TransactionContext context, StateMachine stateMachine, ServicePlan servicePlan) {
    servicePlan = new ServicePlan();
    // ...
    serviceMainService.insertServicePlan(servicePlan);
    return servicePlan;
  }
}
```

CreateHandler#handle 方法实现业务逻辑，和状态机相关的操作封装在 AbstractHandler#doHandler 方法里。
相关代码片段
```java
public class StateMachine<S, E, H extends Handler> {
  public ServicePlan fire(E event, TransactionContext context) throws Exception {
    //...
    return handle.doHandle(context, this, (ServicePlanEventEnum) event);
  }
}
```

```java
@Service
public abstract class AbstractHandler implements Handler {
  @Override
  public ServicePlan doHandle(TransactionContext context, StateMachine stateMachine, 
    ServicePlanEventEnum servicePlanEventEnum) throws Exception {

    ServicePlan servicePlan = null;
    if (!context.getData(BaseStateMachineKey.CURRENT_STATE).equals(ServicePlanStatusEnum.zero)) {
      servicePlan = (ServicePlan) context.getData(BaseStateMachineKey.SERVICE_PLAN);
      Long operateId = (Long) context.getData(BaseStateMachineKey.OPERATE_ID);
      if (servicePlan == null) {
        throw new HttpGlobalError("服务没传");
      }
      /** 获取handler后把当前状态改回来 */
      if (ServicePlanStatusEnum.unknown.equals(context.getData(BaseStateMachineKey.CURRENT_STATE))) {
        context.setData(BaseStateMachineKey.CURRENT_STATE, servicePlan.getServiceStatus());
      }
      servicePlan.setLastModifier(operateId);
      servicePlan.setServiceStatus((ServicePlanStatusEnum) context.getData(BaseStateMachineKey.NEXT_STATE));
    }

    servicePlan = handle(context, stateMachine, servicePlan);
    if (servicePlan == null) {
      return null;
    }

    return servicePlan;
  }
}
```

---  

目前为止，状态机初始化和状态机流转已完成，初始化是 StateMachineFactory#register 存放多个状态机实体，流转是从 StateMachine#fire 调用 AbstractHandler#doHandle 到调用子类 CreateHandler#handle 实现具体业务内容。

最后给一个状态机调用的例子，


[0]: https://raw.githubusercontent.com/sunjirepo/memo/master/temp/StateMachine.png
