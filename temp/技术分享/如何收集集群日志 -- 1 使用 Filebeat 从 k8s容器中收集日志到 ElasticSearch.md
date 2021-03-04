## 如何收集集群日志 -- 1 使用 Filebeat 从 k8s容器中收集日志到 ElasticSearch

### 一、 目的

将 k8s 容器业务服务日志，收集到 ES 搜索引擎。

工具： kubectl + 腾讯云后台

### 二、 步骤

1. [k8s 日志架构][1] 
> Kubernetes 集群：
> ![k8s 集群](https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg)
> 
> 集群级日志架构：
> 
> 1）节点级日志记录 
> 
> ![节点级日志记录](https://d33wubrfki0l68.cloudfront.net/2585cf9757d316b9030cf36d6a4e6b8ea7eedf5a/1509f/images/docs/user-guide/logging/logging-with-node-agent.png)
> 
> 2）使用 sidecar 容器和日志代理 
> 
> ![传输数据流的 sidecar 容器](https://d33wubrfki0l68.cloudfront.net/5bde4953b3b232c97a744496aa92e3bbfadda9ce/39767/images/docs/user-guide/logging/logging-with-streaming-sidecar.png)
> 
> 3）具有日志代理功能的 sidecar 容器
> 
> ![具有日志代理功能的 sidecar 容器](https://d33wubrfki0l68.cloudfront.net/d55c404912a21223392e7d1a5a1741bda283f3df/c0397/images/docs/user-guide/logging/logging-with-sidecar-agent.png)
> 

尝试过第三种，比较占用集群空间，最后使用第一种。

```shell
$ kubectl get pods
# 获取 pod 列表

$ kubectl logs {pod_name}
# 获取日志

$ kubectl node-shell 10.0.0.2
# 获取 node-shell，进入节点服务器找到具体日志地址
# node-shell 是 kubectl 插件，需自行下载安装
```

2. ES集群
> 购买腾讯云服务。 ElasticSearch 版本 7.5.1， filebeat 版本同 ES。
> 
> Elastic Stack：That's Elasticsearch, Kibana, Beats, and Logstash (also known as the ELK Stack).
> 
> ![Elastic Stack 架构图](http://assets.processon.com/chart_image/5ffeac6c1e0853437c421a68.png)

3. 安装 filebeat
> [Run Filebeat on Kubernetesedit][2]
> 
> https://raw.githubusercontent.com/elastic/beats/7.x/deploy/kubernetes/filebeat-kubernetes.yaml
> 
> k8s 对象 和 yaml 文件。
> 
> k8s 对象是我们和集群交互所使用的统一对象，通过传递对象，集群可以理解我们的意图，新增/关联各种组件，可以理解为同集群通信的基本语言。
> 
> k8s 对象使用 yaml 格式的文件描述的。 yaml 是一种文件格式，类似于 json， 通过工具可以和 json 互转。  
```shell
$ kubectl apply -f {xxx.yaml}
# 文件形式 申明 k8s 对象
```
    1. 理解 filebeat-kubernetes.yaml 
        
        包含 5 个对象（用 --- 隔开）： k8s配置（CofigMap）/ k8s DaemonSet / k8s RBAC(Role-RoleBinding-ServiceAccount)

        1. 大体上 ConfigMap 用来配置 filbeat 收集的日志目录 和 推送到远端的ElasticSearch 集群信息

        2. DaemonSet 决定 filebeat 镜像版本 并 挂载 configmap 配置 并 设置一些Pod启动配置

        3. Role-RoleBinding-ServiceAccount 用于配置角色，当前使用的是 default 用户。需要添加 管理 Pods 的部分权限，以便抓取的日志中携带 Pods信息。

替换选择 fluentd 。

### 三、 概念

一堆概念集合，包括容器 / kubernetes / elasticsearch 相关概念，熟悉可略过。

#### docker 相关概念

    dockerfile： 打包工具，最后产出一个容器。

#### k8s 相关概念

    kubectl： 命令行操作界面，类似 shell。

    node： 节点，物理概念 ~= 服务器。

    Pod： 豌豆（Pod），集群最小可管理（销毁/重建/新建）的对象。

    container： 容器，运行业务服务的系统环境，在 Pod 中运行，用的 docker。

    Deployment： 部署集，官方推荐用来管理 Pod 的工具。

    DaemonSet： 节点级别的Pod，类似守护进程。

    workload： 上述Pod/Deployment/DaemonSet 都是 k8s 集群的工作负载（workload）。

    volume： 卷，概念，~= 共享空间。（主机目录/ConfigMap）。 相关概念 volumeMount 卷挂载。

#### elasticsearch 相关概念

    ElasticSearch： 搜索引擎 基于 Lucene。

    Kibana： ES展示层，界面工具。

    Filebeat： 基于文件的收集工具。

    ELK： E=ElasticSearch L=Logstash K=Kibana， ELK是日志解决方案。L用Filebeat替代

[1]: https://kubernetes.io/zh/docs/concepts/cluster-administration/logging/
[2]: https://www.elastic.co/guide/en/beats/filebeat/7.10/running-on-kubernetes.html

