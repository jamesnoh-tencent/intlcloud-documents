## 操作场景

**CKafka 专业版**支持高级运维特性，您可以在控制台查看 TCP 连接数、未同步副本详情、 Topic/Consumer Group 统计排行等，方便运维人员在使用 CKafka 时进行排障处理。


## 操作步骤

1. 登录 [CKafka 控制台](https://console.cloud.tencent.com/ckafka)。
2. 在实例列表中，选择好地域，单击需要查看的“实例 ID/名称”，进入实例详情页。
3. 在实例详情页顶部，单击 **Dashboard**，设置好时间范围，查看相关排行信息。
   - TCP 连接数：展示该 broker 上所有的 TCP 连接数（总和），实例连接数将满时，便于用户查看各个机器的连接数情况。
     ![](https://qcloudimg.tencent-cloud.cn/raw/ab57a66654eac5ceea9de5aebddaf858.png)
   - 未同步副本详情：未同步消息的副本详情。
     ![](https://qcloudimg.tencent-cloud.cn/raw/be1818c8e76394851da1e0507f86e3b1.png)
   - 统计排行：
     - Topic：展示 Topic 生产消费流量 Top10 和 占用磁盘容量 Top10。
       ![](https://qcloudimg.tencent-cloud.cn/raw/405243f8a514f985c33c18807cc44c97.png)
     - Consumer Group：展示 Consumer Group 消费速度 Top10。
         ![](https://qcloudimg.tencent-cloud.cn/raw/03f6ec784d56e2893851dc6afbb8711f.png)
