## 如何收集集群日志 -- 2 使用 Kibana 搜索 ElasticSearch 已收集的日志

### 一、 目的

使用 Kibana 能够搜索到日志

### 二、 使用例子集合

默认情况下 filebeat 每天产生一个 index（索引），Kibana 查询界面 首先 需要 配置一个 Index Pattern。
> [ElasticSearch output.index](https://www.elastic.co/guide/en/beats/filebeat/current/elasticsearch-output.html#index-option-es)
> 
> The default is "filebeat-%{[agent.version]}-%{+yyyy.MM.dd}"
> 
> 目前 index = filebeat-ds-logging-dev-%{[agent.version]}-%{+yyyy.MM.dd}
> 
> 开发/测试/线上 index 名称前缀不同。

k8s 日志
> 腾讯云界面 / kubectl logs
> 

kibana 日志

地址：https://es-79mdsbf1.kibana.tencentelasticsearch.com:5601/app/kibana

用户名 / 密码： common / common

1. Discover
    
    根据 容器名称（=服务名） + 时间段 获取日志。
    
    例子:

    ![截图](https://ftp.bmp.ovh/imgs/2021/01/e2bfac94a470c527.png)

2. Visualize

    可视化，和之前 Discover 类似，可以有图形

    例子：

    ![截图](https://ftp.bmp.ovh/imgs/2021/01/614b05afd7f591e6.png)

3. Dashboard

    展板，多个 Visualize 组合，实时刷新数据。

    例子：

    ![截图](https://ftp.bmp.ovh/imgs/2021/01/d17665d4fd2598f2.png)


### 三、 进一步

[kibana quick start](https://www.elastic.co/guide/en/kibana/current/get-started.html)

[kibana 数据探索](https://www.elastic.co/guide/cn/kibana/current/discover.html)

