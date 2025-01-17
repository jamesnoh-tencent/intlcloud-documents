## 功能概述
腾讯云数据万象通过 **imageMogr2** 接口提供图片缩放功能。

>?处理图片时，原图大小不超过20MB、宽高不超过30000像素且总像素不超过2.5亿像素，处理结果图宽高设置不超过9999像素。
>

## 接口形式

```shell
download_url?imageMogr2/thumbnail/<imageSizeAndOffsetGeometry>
```

## 参数说明

操作名称：thumbnail。

| 参数                          | 含义                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| download_url | 文件的访问链接，具体构成为`<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`，<br>例如`examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /thumbnail/!&lt;Scale>p          | 指定图片的宽高为原图的 Scale%                             |
| /thumbnail/!&lt;Scale>px         | 指定图片的宽为原图的 Scale%，高度不变                     |
| /thumbnail/!x&lt;Scale>p         | 指定图片的高为原图的 Scale%，宽度不变                     |
| /thumbnail/&lt;Width>x           | 指定目标图片宽度为 Width，高度等比压缩                    |
| /thumbnail/x&lt;Height>          | 指定目标图片高度为 Height，宽度等比压缩                   |
| /thumbnail/&lt;Width>x&lt;Height>   | 限定缩略图的宽度和高度的最大值分别为 Width 和 Height，进行等比缩放 |
|  /thumbnail/&lt;Width>x&lt;Height>>  |  限定缩略图的宽度和高度的最大值分别为 Width 和 Height，进行等比缩小，比例值为宽缩放比和高缩放比的较小值，如果目标宽（高）都大于原图宽（高），则不变   |
|  /thumbnail/&lt;Width>x&lt;Height><  |   限定缩略图的宽度和高度的最大值分别为 Width 和 Height，进行等比放大，比例值为宽缩放比和高缩放比的较小值。如果目标宽(高)小于原图宽(高)，则不变   |
| /thumbnail/!&lt;Width>x&lt;Height>r | 限定缩略图的宽度和高度的最小值分别为 Width 和 Height，进行等比缩放 |
| /thumbnail/&lt;Width>x&lt;Height>!  | 忽略原图宽高比例，指定图片宽度为 Width，高度为 Height ，强行缩放图片，可能导致目标图片变形 |
| /thumbnail/&lt;Area>@            | 等比缩放图片，缩放后的图像，总像素数量不超过 Area          |
| /pad/            | 将原图缩放为指定 Width 和 Height 的矩形内的最大图片，之后使用 color 参数指定的颜色居中填充空白部分；取值0或1，0代表不使用 pad 模式，1代表使用 pad 模式          |
| /color/       | 填充颜色，缺省为灰色，需设置为十六进制 RGB 格式（如 #FF0000），详情参考 [RGB 编码表](https://www.rapidtables.com/web/color/RGB_Color.html)，需经过 [URL 安全的 Base64 编码](https://intl.cloud.tencent.com/document/product/1045/33430)，默认值为 #3D3D3D |

## 示例

原图如下：
![](https://main.qcloudimg.com/raw/3d4682ff8e622425ebd29913810a5c38.jpeg)

#### 缩放宽高

假设缩放图片宽高为原图50%，示例如下：
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50p
```

最终效果如下：
![](https://main.qcloudimg.com/raw/2b64595a4a7046dc03f43a2a578764de.jpeg)

#### 缩放宽度，高度不变

假设缩放指定图片宽度为原图50%，高度不变，示例如下：
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/!50px
```

最终效果如下：
![](https://main.qcloudimg.com/raw/988ad350c611a662156e34c28aa5f8a2.jpeg)

#### Pad模式缩放

将原图缩放为600 x 600的矩形内的最大图片，并使用指定颜色填充空白部分，示例如下：
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/thumbnail/600x600/pad/1/color/IzNEM0QzRA
```

最终效果如下：
![](https://main.qcloudimg.com/raw/5f1d9423eaa73e2115fa969667738dee.jpg)

