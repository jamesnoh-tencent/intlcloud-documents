## 概述

当对象存储（Cloud Object Storage，COS）资源发生变动（例如新文件上传、文件删除），您可以及时收到通知消息。事件通知可以结合 [云函数（Serverless Cloud Function，SCF）](https://intl.cloud.tencent.com/product/scf)实现更丰富的应用场景：

- **产品间联动**：例如，当新文件上传到 COS 后，自动刷新 CDN 缓存。新文件上传到 COS 后，自动更新数据库。
- **系统集成**：当 COS 上的文件发生变更（新建、删除、覆盖），自动调用您自己的服务接口。在 UGC（User Generated Content）场景下，您就可以基于事件通知功能，完成移动端和服务端的联动。
- **数据处理**：对 COS 上的文件进行自动处理，例如，自动解压缩、AI 识别等。
![](https://main.qcloudimg.com/raw/d3b76080a15393556c8aa5b79f9439f0.png)

COS 事件通知具有以下特点：

- 异步处理：发送通知不会影响正常的 COS 操作。
- 通知目标：仅支持通知发送至同地域的 SCF 函数。

目前支持以下 COS 事件：

| 事件类型                                  | 描述                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| cos:ObjectCreated:*                       | 以下提到的所有上传事件均可触发云函数                         |
| cos:ObjectCreated:Put                     | 使用 PUT Object 接口创建文件时触发云函数                     |
| cos:ObjectCreated:Post                    | 使用 POST Object 接口创建文件时触发云函数                    |
| cos:ObjectCreated:Copy                    | 使用 PUT Object - Copy 接口创建文件时触发云函数              |
| cos:ObjectCreated:CompleteMultipartUpload | 使用  Complete Multipart Upload  接口创建文件时触发云函数    |
| cos:ObjectCreated:Origin                  | 发生镜像回源时触发云函数                                    |
| cos:ObjectCreated:Replication             | 通过跨地域复制创建对象时触发云函数                           |
| cos:ObjectRemove:*                        | 以下提到的所有删除事件均可触发云函数                         |
| cos:ObjectRemove:Delete                   | 在未开启版本控制的存储桶下，使用 DELETE Object 接口删除对象，或者使用 versionid 删除指定版本的对象时触发云函数 |
| cos:ObjectRemove:DeleteMarkerCreated      | 在开启或者暂停版本控制的存储桶下，使用 DELETE Object 接口删除对象时触发云函数 |
| cos:ObjectRestore:Post                    | 创建了归档恢复的任务时触发云函数                             |
| cos:ObjectRestore:Completed               | 完成归档恢复任务时触发云函数                                 |

## 如何使用 COS 事件通知

使用 COS 事件通知包含以下步骤：

1. 创建 SCF 函数
   - 您可以通过 [SCF 控制台](https://console.cloud.tencent.com/scf?rid=1) 或 CLI 创建函数。创建函数过程中需要选择运行环境（根据您后续编写函数所使用的语言选择）、提交函数代码（支持在线编辑或本地上传代码包）。
   - 您也可以使用 SCF 预置的模板简化创建流程，详情请参见 [创建函数](https://intl.cloud.tencent.com/document/product/583/19806)。不同编程语言的函数写法有所区别，详情请参见 [云函数](https://intl.cloud.tencent.com/document/product/583) 文档。
2. 测试函数
   函数创建完成后，您可以使用测试模板功能进行初步测试。测试模板可以模拟 COS 事件，并触发函数执行，详情请参见 [测试函数](https://intl.cloud.tencent.com/document/product/583/14572)。
3. 添加触发器
   初步测试完成后，您可以通过创建 COS 触发器来实现绑定 SCF 函数和存储桶。您可以通过控制台或命令行添加触发器，详情请参见 [创建触发器](https://intl.cloud.tencent.com/document/product/583/31441) 文档。
4. 实际验证
   完成以上步骤后，您可以操作 COS 中的存储桶，并验证整体流程是否正常。例如，您可以通过控制台、COS Browser 等工具上传、删除文件，并前往 **[SCF 控制台](https://console.cloud.tencent.com/scf?rid=1)** > **函数服务** >  **对应函数名** > **日志查询**，验证是否正常工作。

关于 SCF COS 触发器的更多详情，请参见 [COS 触发器](https://intl.cloud.tencent.com/document/product/583/9707) 文档。
