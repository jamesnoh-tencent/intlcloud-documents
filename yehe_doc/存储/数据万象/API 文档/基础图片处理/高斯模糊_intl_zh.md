## 功能概述
腾讯云数据万象通过 **imageMogr2** 接口对图片进行模糊处理。

## 接口形式

```shell
download_url?imageMogr2/blur/<radius>x<sigma>		
```

## 参数说明

操作名称：blur。

| 参数           | 含义                          |
| -------------- | ----------------------------- |
| download_url | 文件的访问链接，具体构成为`<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`，<br>例如 `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| radius&lt;radius> | 模糊半径，取值范围为1 - 50      |
| sigma&lt;sigma>   | 正态分布的标准差，必须大于0 |

>图片格式为 gif 时，不支持该参数。

## 示例

模糊半径取8，sigma 值取5，进行高斯模糊处理：

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/blur/8x5
```

高斯模糊处理后效果如下：
![](https://main.qcloudimg.com/raw/d635efeeca1d160e773737361e375801.jpeg)

