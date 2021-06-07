# StateMachine 状态机

实际工作遇到利用状态机业务，抽取核心代码，学习理解状态机。

## 分析各种状态机角色

StateMachine包内类图：
![StateMachine 图][0]

1. StateMachineFactory 状态机工厂
2. StateMachine 状态机
3. StateMachineConfig 状态机配置
4. StateConfigration 状态配置
5. AbstractHandler 抽象操作类
6. XXXHandler 具体操作类实现
7. TransactionContext 状态机操作上下文
8. BaseStateMachineKey 上下文数据Key
9. HcStateMachineInit AiStateMachineInit SpringBoot初始化


### 边缘类：

HcStateMachineInit 和 AiStateMachineInit

### 状态机核心类：




[0]: https://raw.githubusercontent.com/sunjirepo/memo/master/temp/StateMachine.png
