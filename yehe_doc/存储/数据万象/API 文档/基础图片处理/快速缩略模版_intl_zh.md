## 功能概述
腾讯云数据万象通过 **imageView2** 接口提供常用图片处理模板。开发者根据业务需求，只需在下载 URL 后面附加相应的参数，就可以生成相应的缩略图，目前支持大小在20M以内、长宽小于9999像素的图片处理。

## 接口形式

```shell
imageView2/<mode>/w/<Width>
                 /h/<Height>
                 /format/<Format>
                 /q/<Quality>
                 /rq/<Quality>
                 /lq/<Quality>			
```

>质量变换参数仅针对 **jpg** 和 **webp** 格式图片。


## 参数说明

| 参数                          | 含义                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| download_url | 文件的访问链接，具体构成为`<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`，<br>例如 `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /1/w/&lt;Width>/h/&lt;Height>       | 限定缩略图的宽高最小值。该操作会将图像等比缩放直至某一边达到设定最小值，之后将另一边居中裁剪至设定值。若只指定一边，则表示宽高相等的正方形。<br>例如，原图大小为1000x500，将参数设定为?imageView2/1/w/500/h/400 后，图像会先等比缩放至800x400，之后左右各裁剪150，得到500x400大小的图像 |
| /2/w/&lt;Width>/h/&lt;Height>       | 限定缩略图的宽高最大值。该操作会将图像等比缩放至宽高都小于设定最大值。<br>例如，原图大小为 1000x500，将参数设定为?imageView2/2/w/500/h/400后，图像会等比缩放至500x250。如果只指定一边，则另一边自适应 |
| /3/w/&lt;Width>/h/&lt;Height>       | 限定缩略图的宽高最小值。该操作会将图像等比缩放至宽高都大于设定最小值。<br>例如，原图大小为 1000x500，将参数设定为?imageView2/3/w/500/h/400后，图像会等比缩放至800x400。如果只指定一边，则另一边设为相同值 |
| /4/w/&lt;LongEdge>/h/&lt;ShortEdge> | 限定缩略图的长边和短边的最小值分别为 LongEdge 和 ShortEdge ，进行等比压缩；如果只指定一边，代表另外一边为同样的值 |
| /5/w/&lt;LongEdge>/h/&lt;ShortEdge> | 限定缩略图的长边和短边的最大值分别为 LongEdge 和 ShortEdge，进行等比压缩，居中裁剪；如果只指定一边，则表示宽高相等的正方形；缩放后其中一边多余的部分会被裁剪掉 |
| /format/&lt;Format>              | 目标缩略图的图片格式，Format 可为：jpg，bmp，gif，png，webp，缺省为原图格式 |
| /q/&lt;Quality>                  | 图片质量，取值范围 0 - 100 ，默认值为原图质量；取原图质量和指定质量的最小值；&lt;Quality> 后面加!（注意为英文字符），表示强制使用指定值 |
| /rq/&lt;quality>                 | 图片的相对质量，取值范围0 - 100 ，数值以原图质量为标准。例如原图质量为80，将 rquality 设置为80后，得到处理结果图的图片质量为64（80x80%） |
| /lq/&lt;quality>                 | 图片的最低质量，取值范围0 - 100 ，设置结果图的质量参数最小值。<br>例如，原图质量为85，将 lquality 设置为80后，处理结果图的图片质量为85；<br>例如，原图质量为60，将 lquality 设置为80后，处理结果图的图片质量会被提升至80 |


## 示例
选用模板样式1，限定缩略图的宽高最小值为400×600，绝对质量为85：

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageView2/1/w/400/h/600/q/85
```

缩略图效果如下：
![](https://main.qcloudimg.com/raw/281a2f6474ad29b430355f785f158a5c.jpeg)
