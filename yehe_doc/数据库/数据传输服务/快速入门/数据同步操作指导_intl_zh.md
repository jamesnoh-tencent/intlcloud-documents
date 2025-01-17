## 相关知识

- [数据同步功能描述](https://intl.cloud.tencent.com/document/product/571/42667)。
- [数据同步支持的数据库](https://intl.cloud.tencent.com/document/product/571/42579)。

## 整理流程

| **操作流程**              | **说明**                                                     |
| ------------------------- | ------------------------------------------------------------ |
| 1. 准备工作               | 同步任务前，需要对源库、目标库和网络环境做一些 [准备工作](https://intl.cloud.tencent.com/document/product/571/42652)，以满足环境要求。 |
| 2. 创建数据同步任务       | 本章节仅提供了基础的同步任务示例，更多场景请参考 [数据同步](https://intl.cloud.tencent.com/document/product/571/42624)。 |
| 3. 查看同步进度或其他操作 | <li>查看整体的同步进度，进行校验、重试等操作，请参考 [任务管理](https://intl.cloud.tencent.com/document/product/571/42620)。<li>查看数据同步的各项指标，请参考 [查看监控指标](https://intl.cloud.tencent.com/document/product/571/42606)。</li> |
| 4. 对比同步项，结束任务   | 同步任务完成后，确认源库和目标库内容同步一致，手动结束同步任务，请参考 [结束任务](https://intl.cloud.tencent.com/document/product/571/42616)。 |

## 数据同步任务示例

1. 登录 [数据同步购买页](https://buy.cloud.tencent.com/dts)，选择相应配置，单击**立即购买**。
2. 购买完成后，返回 [数据同步列表](https://console.cloud.tencent.com/dts/replication)，可看到刚创建的数据同步任务，刚创建的同步任务需要进行配置后才可以使用。
3. 在数据同步列表，单击**操作**列的**配置**，进入配置同步任务页面。
![](https://qcloudimg.tencent-cloud.cn/raw/afe583b0dd3569cad36da0f3f19acba0.png)
4. 在配置同步任务页面，配置源端实例、帐号密码，配置目标端实例、帐号和密码，测试连通性后，单击**下一步**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/dcad48b082c4bfc8bc25b2aff7a0f579.png"  style="margin:0;">
5. 在设置同步选项和同步对象页面，将对数据初始化选项、数据同步选项、同步对象选项进行设置，在设置完成后单击**保存并下一步**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/a8df8150f387ffd56e11f60a6384adba.png"  style="margin:0;">
<strong>库表映射</strong>：在已选对象中，鼠标放在右侧将出现编辑按钮，单击后可在弹窗中填写映射名。
<img src="https://qcloudimg.tencent-cloud.cn/raw/fb3dfa032310e444729a805b503e019b.png"  style="margin:0;">
6. 在校验任务页面，完成校验并全部校验项通过后，单击**启动任务**。
>?在校验结果中出现告警项不影响启动任务，但推荐单击**查看详情**获取建议进行调整。
>
![](https://qcloudimg.tencent-cloud.cn/raw/898e1d8ced68446dfd3e889fb77d7011.png)
7. 返回数据同步任务列表，任务开始进入**运行中**状态。
>?选择**操作**列的**更多** > **结束**可关闭同步任务，请您确保数据同步完成后再关闭任务。
>
![](https://qcloudimg.tencent-cloud.cn/raw/058cf11d354d64ae32e881a421e0d686.png)

