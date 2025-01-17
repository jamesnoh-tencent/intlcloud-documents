


直播截图是指以固定的时间间隔截取实时直播流的图像，并生成图片。您可以通过回调通知获取截图信息，截图数据可应用于直播鉴黄、直播房间封面等多种场景。

## 直播截图整体流程
![](https://qcloudimg.tencent-cloud.cn/raw/c0412cf3d639a0f9804a7fc08373a9de.png)

整体流程：
1. 在控制台或者直接调用云 API 配置直播截图功能。
- 进行直播推流。 
- 截图服务根据配置生成截图数据，存储于对象存储系统。
- 生成的截图的相关信息以回调形式通知到您。

## 直播截图配置

### 截图配置方式
- [云直播 API](https://intl.cloud.tencent.com/document/product/267/30760#.E6.88.AA.E5.9B.BE.E9.89.B4.E9.BB.84.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3)
- 【云直播控制台】>【功能模板】>【[截图鉴黄配置](https://console.cloud.tencent.com/live/config/jtjh)】，详情请参见 [直播截图鉴黄](https://cloud.tencent.com/document/product/267/20386)。

### 截图间隔配置

您可按照业务需要指定截图频率，即截图时间间隔（SnapshotInterval），取值范围为5秒 - 300秒，默认间隔为10秒。

### 截图宽高配置

截图服务支持指定宽（Width）高（Height）截图：

 ![](https://main.qcloudimg.com/raw/86e3ce12a58b5125cca87a2d19ff922f.png)

>! 若无需指定特殊宽高，默认截图宽高（设置为 0）则为推流视频画面宽高，可不看如下进阶配置，直接跳过查看下一小节内容。

先看如下3个宽高概念：

- 推流宽高，即直播流视频画面宽高，本文设为（X，Y）。
- 配置宽高，即通过控制台/云 API 配置的宽高，本文设为（W，H）。
- 截图宽高，即截图服务生成截图的宽高，本文设为（N，M）。

截图服务支持以下几种场景配置：

- 不设置，即取默认（W，H）=（0，0），此时截图宽高与推流宽高一致，即 （N，M）=（X，Y）。
- 只设置宽 W，此时截图宽 N = W，而截图高则等比例缩放，即 M = N / X \* Y。
- 只设置高 H，此时截图高 M = H，而截图宽则等比例缩放，即 N = M / Y \* X。
- 同时设置 （W，H），此时截图宽高与配置宽高一致，即 （N，M）=（W，H）。

配置宽高自动交换特性，考虑如下场景：

- 若设置 W < H，且 W 和 H 都大于0，若推流时 X > Y，即配置宽小于高，而推流宽大于高。

此时若直接截图，图像则会出现扭曲变形，为避免变形出现，直播截图服务后台自动交换 W 与 H 的值，确保配置的宽高大小关系与直播推流画面保持一致。


## 直播截图事件消息通知

事件消息通知配置请参见 [事件消息通知](https://intl.cloud.tencent.com/document/product/267/31566)，截图回调通知以 JSON 格式，用 HTTP POST 协议通知到客户事先配置好的接收服务端。

### 截图回调相关字段

| 字段名称 | 类型 | 说明 |
| --- | --- | --- |
| event\_type | int | 回调信息类型，截图回调固定为200 |
| stream\_id | string | 直播流名称 |
| channel\_id | string | 同直播流名称 |
| create\_time | int64 | 截图生成 Unix 时间戳 |
| file\_size | int | 截图文件大小，单位为字节 |
| width | int | 截图宽，单位为像素 |
| height | int | 截图高，单位为像素 |
| pic\_url | string | 截图文件路径 /path/name.jpg，详见下文 [部分字段详解](#jump) |
| pic\_full\_url | string | 截图完整 URL，详见下文 [部分字段详解](#jump) |
| sign | string | 回调签名，详见 [事件消息通知](https://intl.cloud.tencent.com/document/product/267/31566) |
| t | int64 | 回调签名过期 Unix 时间戳，详见 [事件消息通知](https://intl.cloud.tencent.com/document/product/267/31566) |

### <span id="jump">部分字段详解</span>
- `pic_url`详解：
 - path：年-月-日
 - name：直播流名称-screenshot-时-分-秒-宽x高.jpg
 例子：
```
 /2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg
```
该字段可用于拼接自定义的 COS CDN 域名，若不需要 CDN 域名可直接使用 pic_full_url。

- `pic_full_url`详解：
 - http://COS域名+pic_url
	例子：
```
	http://testbucket-1234567890.cos.region.myqcloud.com/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg
```


### 截图回调示例

```
{

"event_type":200,

"stream_id":"stream_name",

"channel_id":"stream_name",

"create_time":1545030273,

"file_size":7520,

"width":640,

"height":352,

"pic_url":"/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg",

"pic_full_url":"http://testbucket-1234567890.cos.region.myqcloud.com/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg",

"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",

"t":1545030873

}
```
