本文将为您介绍如何查看实例基本信息。


## 操作步骤

1. 登录 [Grafana 可视化服务控制台](https://console.cloud.tencent.com/monitor/grafana/list)。
2. 在实例列表中，找到对应的实例，单击**实例 ID** 或者右侧的**管理**，即可查看实例基本信息。
![](https://qcloudimg.tencent-cloud.cn/raw/aa3a9b55b0e73b09f4e8346f38ed6f38.png)
3. 在基本信息页支持如下操作：
 - 修改实例名称。
 - 编辑实例对应的标签。
 - 开启外网访问地址。
 - 设置外网 IP 白名单。您可以通过白名单管控提升安全性。
 - 开启 SSO 单点登录。SSO是一种统一认证和授权机制，开启后将可以使用腾讯云账号登录 Grafana。
 - 自定义 DNS。您可以按需自定义 DNS，让 Grafana 通过您的私有 DNS 解析并访问对应的域名。

### SSO 单点登录注意事项
1. SSO 单点登录支持标签，您可以对实例设置对应标签，对标签有权限的子账号将自动获得登录权限。
2. 通过 SSO 登录的账号权限为 Admin，Grafana 本身不支持通过 SSO 获取 Server Admin 权限，您可以使用账号密码登录并给 SSO 登录账号设置 Server Admin 权限。



