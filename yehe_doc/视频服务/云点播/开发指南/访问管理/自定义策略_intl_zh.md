>!本文档主要介绍**云点播**访问管理功能的相关内容，其他产品访问管理相关内容请参见 [支持 CAM 的产品](https://intl.cloud.tencent.com/document/product/598/10588)。

在访问管理中使用 [预设策略](https://intl.cloud.tencent.com/document/product/266/33971) 来实现授权虽然方便，但权限控制粒度粗，不能细化到子应用和 API 粒度。如果开发者要求精细的权限控制能力，则需要创建自定义策略。


## 自定义策略创建方法

自定义策略有多种创建方法，下方表格展示各种方法的对比，具体操作流程请参考下文。

| 创建入口   | 创建方法     | 效力<br/>（Effect） | 资源<br/>（Resource） | 操作<br/>（Action） | 灵活性 | 难度 |
| ---------- | ------------ | ------------------- | --------------------- | ------------------- | ------ | ---- |
| 控制台     | 策略生成器   | 手动选择            | 语法描述              | 手动选择            | 中     | 中   |
| 控制台     | 策略语法     | 语法描述            | 语法描述              | 语法描述            | 高     | 高   |
| 服务端 API | CreatePolicy | 语法描述            | 语法描述              | 语法描述            | 高     | 高   |

>?
>- 云点播不支持按照产品功能创建自定义策略。
>- **手动选择**是指用户在控制台所展示的候选项列表中选择对象。**语法描述**是指通过策略语法来描述对象。

## 策略语法资源描述<span id = "p1"></span>

如上文所述，云点播权限管理的资源粒度是子应用。子应用的策略语法描述方式遵循 [CAM 标准](https://intl.cloud.tencent.com/document/product/598/10606)。在下文的示例中，开发者的主账号 ID 是12345678，APPID 是1250000001（主应用 ID 等于 APPID），开发者创建了两个云点播子应用，ID 分别是1400000001和1400000002。

- **云点播所有资源的策略语法描述**
```
"resource": [
	"qcs::vod::uin/12345678:subAppId/*"
]
```
- **主应用的策略语法描述**
```
"resource": [
	"qcs::vod::uin/12345678:subAppId/1250000001"
]
```
- **单个子应用的策略语法描述**
```
"resource": [
	"qcs::vod::uin/12345678:subAppId/1400000001"
]
```
- **主应用和单个子应用的策略语法描述**
```
"resource": [
	"qcs::vod::uin/12345678:subAppId/1250000001",
	"qcs::vod::uin/12345678:subAppId/1400000001"
]
```

## <span id ="p3"></span>策略语法操作描述

如上文所述，云点播权限管理的操作粒度是服务端 API。在下文的示例中，以`DescribeMediaInfos`、`DescribeAllClass`等服务端 API 为例。

- **云点播所有服务端 API 的策略语法描述**
```
"action": [
	"name/vod:*"
]
```
- **单个服务端 API 操作的策略语法描述**
```
"action": [
	"name/vod:DescribeMediaInfos"
]
```
- **多个服务端 API 操作的策略语法描述**
```
"action": [
	"name/vod:DescribeMediaInfos",
	"name/vod:DescribeAllClass"
]
```

## 自定义策略使用示例

### 使用策略生成器

在下文示例中，我们将创建一个自定义策略。该策略允许对1400000001这个云点播子应用进行任何操作，除了`ProcessMedia`这个服务端 API。

1. 以 [主账号](https://intl.cloud.tencent.com/document/product/598/32633) 的身份访问 CAM 控制台的[【策略】](https://console.cloud.tencent.com/cam/policy)，单击【新建自定义策略】。
2. 选择【按策略生成器创建】，进入策略创建页面。
3. 选择服务和操作。
	- 【效果(Effect)】配置项选择【允许】。
	- 【服务(Service)】配置项选择【云点播】。
	- 【操作(Action)】配置项勾选所有项。
	- 【资源(Resource)】配置项按照 [资源语法描述](#p1) 说明填写`qcs::vod::uin/12345678:subAppId/1400000001`。
	- 【条件(Condition)】配置项无需配置。
	- 单击【添加声明】，页面最下方会出现一条“允许对云点播子应用1400000001进行任何操作”的声明。
4. 在同个页面中继续添加另一条声明。
	- 【效果(Effect)】配置项选择【拒绝】。
	- 【服务(Service)】配置项选择【云点播】。
	- 【操作(Action)】配置项勾选`ProcessMedia`（可通过搜索功能选择）。
	- 【资源(Resource)】配置项按照 [资源语法描述](#p1) 说明填写`qcs::vod::uin/12345678:subAppId/1400000001`。
	- 【条件(Condition)】配置项无需配置。
	- 单击【添加声明】，页面最下方会出现一条“拒绝对云点播子应用1400000001进行`ProcessMedia`操作”的声明。
     ![](https://main.qcloudimg.com/raw/1ac34ffafb9719e36e46d4a5e7ccf1cf.png)
5. 单击【下一步】，按需修改策略名称（也可以不修改）。
6. 单击【完成】完成自定义策略的创建。后续将该策略授予子用户的方法同 [将云点播完整权限授予已存在的子用户](https://intl.cloud.tencent.com/document/product/266/33971#p2)。


### 使用策略语法

在下文示例中，我们将创建一个自定义策略。该策略允许对1400000001和1400000002这两个云点播子应用进行任何操作，但不允许对1400000001进行`ProcessMedia`操作。

1. 以 [主账号](https://intl.cloud.tencent.com/document/product/598/32633) 的身份访问 CAM 控制台的[【策略】](https://console.cloud.tencent.com/cam/policy)，单击【新建自定义策略】。
2. 选择【按策略语法创建】，进入策略创建页面。
3. 在【选择模板类型】框下选择【空白模版】。
>?所谓策略模版，指新策略是现有策略（预置策略或自定义策略）的一个拷贝，然后在此基础上做调整。在实际使用中，开发者可以根据情况选择合适的策略模版，降低编写策略内容的难度和工作量。
4. 单击【下一步】，按需修改策略名称（也可以不修改）。
5. 在【编辑策略内容】编辑框中填写策略内容。本示例的策略内容为：
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/vod:*"
            ],
            "resource": [
                "qcs::vod::uin/12345678:subAppId/1400000001",
                "qcs::vod::uin/12345678:subAppId/1400000002"
            ]
        },
        {
            "effect": "deny",
            "action": [
                "name/vod:ProcessMedia"
            ],
            "resource": [
                "qcs::vod::uin/12345678:subAppId/1400000001"
            ]
        }
    ]
}
```
>?策略内容遵循 CAM [策略语法](https://intl.cloud.tencent.com/document/product/598/10603) 规范，其中资源和操作两个元素的语法分别如上文 [策略语法资源描述](#p1) 和 [策略语法操作描述](#p3) 所述。
6. 单击【创建策略】完成自定义策略的创建。后续将该策略授予子用户的方法同 [示例：将云点播完整权限授予已存在的子用户](https://intl.cloud.tencent.com/document/product/266/33971#p2)。

### 使用服务端 API

对于大多数开发者来说，在控制台完成权限管理操作已经能满足业务需求。但如果需要将权限管理能力自动化和系统化，则可以基于服务端 API 来实现。
策略相关的服务端 API 属于 CAM，具体请参见 [CAM 官网文档](https://intl.cloud.tencent.com/zh/document/product/598)。此处仅列出几个主要接口：

- [创建策略](https://intl.cloud.tencent.com/document/product/598/32248)
- [删除策略](https://intl.cloud.tencent.com/document/product/598/32247)
- [绑定策略到用户](https://intl.cloud.tencent.com/document/product/598/32249)
- [解除绑定到用户的策略](https://intl.cloud.tencent.com/document/product/598/32245)
