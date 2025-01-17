## 功能介绍

每个集群可以即时或定时（按天、按周）根据已选的巡检项对集群的节点和服务进行健康检查，每个集群仅可配置一个定期巡检任务以便周期性掌握集群健康情况，即时对异常或风险点进行处理。

设置即时巡检或定时巡检任务时会默认选择常规巡检项，特殊情况需要对服务功能进行巡检，可按需勾选需要增加巡检项目，但是服务功能类巡检会消耗集群性能，不推荐在业务高峰期进行有耗损的巡检。

每次巡检任务完成后生成 PDF 格式的巡检报告，用户可以下载或删除巡检报告，每个主账号最多可保留50份巡检报告，超过保存的最大限额将会删除时间较久的报告。

>?巡检系统支持服务巡检项，当前仅支持 hdfs、yarn、hbase、hive、zookeeper。


## 操作步骤
1. 登录 [EMR 控制台](https://console.cloud.tencent.com/emr)，在**集群列表**中单击对应的**集群 ID/名称**进入集群详情页。
2. 在集群详情页中选择**集群监控**>**集群巡检**可根据当前集群的节点和服务进行健康检查，每个集群仅可配置一个定期巡检任务，也可单击**即时巡检**进行巡检。配置定时巡检任务可单击**定时巡检设置**。
![](https://main.qcloudimg.com/raw/ce7e2d8727ebac8149f3eaf9e45a00e4.png)
 - 即时巡检：即时巡检是检查集群从某个时刻到当前时间节点和服务的健康状态并生成巡检报告。
![](https://main.qcloudimg.com/raw/75be9ef6b909944665a1b6a08fb780fe.png)
 - 定时巡检：定期巡检策略开启后，系统将自动检测每个巡检周期内集群节点和服务的健康状态并生成巡检报告。每个集群可配置一个定期巡检策略。
![](https://main.qcloudimg.com/raw/15c5e354c2c06f9f858406277da84034.png)
 - 巡检项：默认支持所有已开启的事件监控策略，若需调整巡检项可参考 [集群事件-设置事件策略](https://intl.cloud.tencent.com/document/product/1026/36889) 进行设置。初始巡检项系统默认勾选所有已开启监控的事件，修改后第二次设置巡检项，默认记录勾选上一次已选择的巡检项。
![](https://main.qcloudimg.com/raw/89019ff88ebf26e599e980db50647fa9.png)


