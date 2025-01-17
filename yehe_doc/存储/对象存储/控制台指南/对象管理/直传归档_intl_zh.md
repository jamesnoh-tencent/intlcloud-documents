## 简介
目前对象存储（Cloud Object Storage，COS）支持直传归档，您可直接将对象设置为归档类型并上传到 COS，直传归档的方式包括控制台、API、SDK、COSCMD 工具。此外您还可以通过 COS 的生命周期功能将已上传的对象沉降为归档存储类型或深度归档存储类型。关于归档类型的详细介绍，请参见 [存储类型概述](https://intl.cloud.tencent.com/document/product/436/30925)。


## 直传归档的方式

- 控制台上传
 [COS 控制台](https://console.cloud.tencent.com/cos5) 的【上传文件】，选择上传对象后，在设置对象属性中将存储类型选择为【归档存储】或【深度归档存储】，详情请参见 [上传对象](https://intl.cloud.tencent.com/document/product/436/13321)。
![](https://main.qcloudimg.com/raw/8f3b05d1407a9017c54c86c9cec693c7.png)

- API 上传
通过在 PUT Object、POST Object 或 Initiate Multipart Upload 中将 x-cos-storage-class 设置为 ARCHIVE 或 DEEP_ARCHIVE，实现直传归档。
>! Append Object 不支持直传归档。
>

- SDK 上传
当前 COS 发布所有 SDK 都支持直传归档，具体方式为在文件上传时，将 StorageClass 参数设置为 ARCHIVE 或 DEEP_ARCHIVE，实现直传归档。

- COSCMD 工具上传
COSCMD 工具支持直传归档，具体方式为在文件上传时，通过增加头部字段 x-cos-storage-class，并设置为 ARCHIVE 或 DEEP_ARCHIVE，实现直传归档。

#### 归档恢复与下载
对归档存储和深度归档存储类型的对象进行下载操作，与标准存储/低频存储不同，归档存储在下载前，需要先执行恢复操作（解冻），恢复完成后才可以进行下载，恢复操作有如下三种方式：
- 极速模式：时间最短，通常只需要1到5分钟完成数据取回。
- 标准模式：使用标准模式，一般可在3到5小时完成数据取回。
- 批量模式：成本最低，一般在5到12小时可完成数据取回。

>?深度归档存储类型的文件不支持使用极速模式进行恢复。在标准模式下恢复时间为12 - 24小时；在批量模式下恢复时间为24 - 48小时。

同时控制台、API、SDK、COSCMD 工具都支持归档存储恢复与下载。

#### 直传归档限制说明
- 如果下载归档存储和深度归档存储类型的对象，需要先进行恢复，然后再进行下载。
- 如果复制归档存储和深度归档存储类型的对象，需要先进行恢复，然后再进行复制。
- 归档存储和深度归档存储类型的对象不支持跨地域复制。
- 归档存储和深度归档存储类型的对象不支持转换为较活跃的存储类型，例如标准存储、低频存储。

