您可以参考本文档对 Grafana 版本进行升级操作。

## 操作步骤

1. 登录 [Grafana 可视化服务控制台](https://console.cloud.tencent.com/monitor/grafana/list)。
2. 在实例列表中，选择需要被销毁或退还的 Grafana 实例，单击右侧的**更多 > 实例状态 > 升级**。
3. 在弹出窗口中选择支持升级的版本，进行升级。
   ![](https://qcloudimg.tencent-cloud.cn/raw/6ecaabcc084baad3beae8ec289bd7dab.png)
4. 完成所有步骤后，实例将进行升级重建。

## 相关说明

1. 开源 Grafana 只支持一个大版本内的升级兼容，对于超过两个版本的实例，可以选择通过多次分别升级。
2. 实例升级时后台会进行数据备份，实例升级失败后会自动回退到升级前状态。
