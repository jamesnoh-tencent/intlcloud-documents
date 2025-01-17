﻿﻿子账号默认没有前端性能监控任何权限。需要主账号授予子账号相关权限，子账号才能正常访问前端性能监控资源。

## 操作前提
使用主账号或拥有 QcloudCamFullAccess 权限的子账号登录腾讯云控制台，并参考 [新建子用户](https://intl.cloud.tencent.com/document/product/598/13674) 操作步骤创建子账户。

## 自定义策略
1. 使用主账号或拥有 QcloudCamFullAccess 权限的子账号进入**访问控制** > [**策略**](https://console.cloud.tencent.com/cam/policy)。
2. 单击**新建自定义策略** > **按策略语法创建**，选择空白模板。根据 [策略语法说明](https://intl.cloud.tencent.com/document/product/1131/44511) 完成策略编辑。
<img src = "https://main.qcloudimg.com/raw/426416f0b157a3ee22babae44976747d.png" style = "width:90%">

## 策略授权
>?前端性能监控为您创建默认策略 QcloudRUMFullAccess（前端性能监控（RUM）全读写访问权限）和 QcloudRUMReadOnlyAccess（前端性能监控（RUM）只读访问权限），您可以通过搜索策略名称快速进行默认策略授权。也可以对自定义策略进行授权。授权成功后，子账号才能正常访问相关资源。

1. 使用主账号或拥有 QcloudCamFullAccess 权限的子账号进入**访问控制** > [**策略**](https://console.cloud.tencent.com/cam/policy)。
2. 进入策略管理页，在策略名称搜索框中输入对应的策略名称。
3. 选择只读访问或全读写访问权限，在操作列中单击**关联用户/组**。
![](https://main.qcloudimg.com/raw/80bc9e1d0b3908deacb1cd5d7ecd867f.png)
4. 在弹框中勾选对应的用户，单击**确定**即可。
