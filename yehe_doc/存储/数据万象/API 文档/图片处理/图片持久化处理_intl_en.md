## Processing upon Upload
The feature of processing upon upload provided by CI helps you implement image processing when uploading an image. You only need to add Pic-Operations to the request header and set related parameters to implement image processing when uploading an image, and store the input image and processing result in COS. Currently, this feature supports the processing of a file up to 20 MB.

### Sample request

The request for uploading an image is the same as that of the API for simply uploading a COS V5 file. The only difference is that image processing parameters are added to the request header.

```shell
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: <PicOperations>
```

>?
>- For more information about the simple upload API of COS, please see [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749).
>- Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)
>- The QPS for persistent processing is limited to 100. If you need a higher QPS, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder).
>

### Request content

`Pic-Operations` is a JSON string. Its parameters are as follows:

| Parameter | Type | Required | Description |
| ----------- | ----- | ---- | -------------------------------------- |
| is_pic_info | Int | No | Whether to return the input image information <br>`0` (default): no <br>`1`: yes |
| rules | Array | No | Processing rules (up to 5 rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. |

 Parameters of `rules` (a JSON array) are as follows:

| Parameter | Type | Required | Description |
| ------ | ------ | ---- | ---------------------------------------- |
| bucket | String | No | Name of the destination bucket to store the results, formatted as `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket. |
| fileid   | String | Yes | The path and name of the output file <br>Example: `/p1/test1.jpg`<br>1. A value starting with a slash (/) indicates an absolute path. For example, if `fileid` is set to `/p2/test2.jpg`, the `test2.jpg` file will be stored in the `p2` folder. <br>2. A value not starting with a slash indicates a relative path. For example, if `fileid` is set to `p2/test2.jpg`, a folder named `p2` is created in the `p1` folder, and the `test2.jpg` file will be stored in the `p2` folder.<br>3. Note: Do not end the value with a slash. Otherwise, an empty filename will be generated.    | 
| rule | String | Yes | The processing parameter. For more information, please see the image processing API of CI. If the image needs to be stylized, prefix `style/` to the style name. For example, if the style name is `test`, you can set this parameter to `style/test`. |

### Response
Parameters in the response body are as follows:

| Parameter | Type | Description |
| ---------------- | --------- | ---- |
| UploadResult | Container | Input image information |

 Content of `UploadResult`:

| Parameter | Type | Description |
| -------------- | --------- | ------ |
| OriginalInfo | Container | Input image information |
| ProcessResults | Container | Image processing results |

 Content of `OriginalInfo`:

| Parameter | Type | Description |
| --------- | --------- | ------ |
| Key | String | Name of the input image |
| Location | String | Location of the image |
| ImageInfo | Container | Input image information |
|      ETag     | String    | ETag of the input image. If the output image overwrites the input image, the value of `ETag` will be that of the output image. |

 Content of `ImageInfo`:

| Parameter | Type | Description |
| ----------- | ------ | ------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Image average hue |
| Orientation | Int | Image rotation angle |

 Content of `ProcessResults`:

| Parameter | Type | Description |
| ------ | --------- | --------- |
| Object | Container | Processing result of each image |

 Content of `Object`:

| Parameter | Type | Description |
| -------- | ------ | ---- |
| Key | String | Filename |
| Location | String | Image path |
| Format | String | Image format |
| Width    | Int    | Image width             |
| Height | Int | Image height |
| Size     | Int    | Image size             |
| Quality | Int | Image quality |
| ETag | String | ETag of the output image |

### Example
#### Request

```shell
PUT /filename.jpg HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Date: Wed, 28 Oct 2015 20:32:00 GMT
Authorization:XXXXXXXXXXXX
Pic-Operations: {"is_pic_info":1,"rules":[{"fileid":"test.jpg","rule":"imageView2/format/png"}]}
Content-Length: 64

[Object]
```

#### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
Status: 200 OK
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8z****

<UploadResult>
		<OriginalInfo>
			<Key>filename.jpg</Key>
			<Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/filename.jpg</Location>
			<ETag>&quot;580cd6930444576523c25f86ce2af9b1fc2d5484&quot;</ETag>
			<ImageInfo>
				<Format>JPEG</Format>
				<Width>640</Width>
				<Height>427</Height>
				<Quality>100</Quality>
				<Ave>0xa18454</Ave>
				<Orientation>1</Orientation>
			</ImageInfo>
		</OriginalInfo>
		<ProcessResults>
			<Object>
				<Key>test.jpg</Key>
				<Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/test.jpg</Location>
				<Format>png</Format>
				<Width>640</Width>
				<Height>427</Height>
				<Size>463092</Size>
				<Quality>100</Quality>
				<ETag>&quot;eaa4e3d8fd498bbc63be3b71c46b9c61f23e3f0c&quot;</ETag>
			</Object>
		</ProcessResults>
</UploadResult>
```

>!Processing upon upload supports the multipart upload feature of COS V5. You can process images by adding the `Pic-Operations` request header when calling the [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) API.


```shell
POST /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: <PicOperations>
```

>?For more information, please see [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742).


## Processing In-Cloud Data

The image processing APIs of CI allow you to process images that are already stored in COS and save the results to COS.

### Sample request
```shell
POST /<ObjectKey>?image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: <PicOperations>
```

### Request content
`Pic-Operations` is a JSON string. Its parameters are as follows:

| Parameter | Type | Required | Description |
| ----------- | ----- | ---- | -------------------------------------- |
| is_pic_info | Int | No | Whether to return the input image information <br>`0` (default): no <br>`1`: yes |
| rules | Array | No | Processing rules (up to 5 rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. |

 Parameters of `rules` (a JSON array) are as follows:

| Parameter | Type | Required | Description |
| ------ | ------ | ---- | ---------------------------------------- |
| bucket | String | No | Name of the destination bucket to store the results, formatted as `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket. |
| fileid   | String | Yes | The path and name of the output file <br>Example: `/p1/test1.jpg`<br>1. A value starting with a slash (/) indicates an absolute path. For example, if `fileid` is set to `/p2/test2.jpg`, the `test2.jpg` file will be stored in the `p2` folder. <br>2. A value not starting with a slash indicates a relative path. For example, if `fileid` is set to `p2/test2.jpg`, a folder named `p2` is created in the `p1` folder, and the `test2.jpg` file will be stored in the `p2` folder.<br>3. Note: Do not end the value with a slash. Otherwise, an empty filename will be generated.    | 
| rule | String | Yes | The processing parameter. For more information, please see the image processing API of CI. If the image needs to be stylized, prefix `style/` to the style name. For example, if the style name is `test`, you can set this parameter to `style/test`. |

### Response
Parameters in the response body are as follows:

| Parameter | Type | Description |
| ---------------- | --------- | ---- |
| UploadResult | Container | Input image information |

 Content of `UploadResult`:

| Parameter | Type | Description |
| -------------- | --------- | ------ |
| OriginalInfo | Container | Input image information |
| ProcessResults | Container | Image processing results |

 Content of `OriginalInfo`:

| Parameter | Type | Description |
| --------- | --------- | ------ |
| Key | String | Name of the input image |
| Location | String | Location of the image |
| ImageInfo | Container | Input image information |
| ETag | String | ETag of the input image. If the output image overwrites the input image, the value of `ETag` will be that of the output image. |

 Content of `ImageInfo`:

| Parameter | Type | Description |
| ----------- | ------ | ------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Image average hue |
| Orientation | Int | Image rotation angle |

 Content of `ProcessResults`:

| Parameter | Type | Description |
| ------ | --------- | --------- |
| Object | Container | Processing result of each image |

 Content of `Object`:

| Parameter | Type | Description |
| -------- | ------ | ---- |
| Key | String | Filename |
| Location | String | Image path |
| Format | String | Image format |
| Width    | Int    | Image width             |
| Height | Int | Image height |
| Size     | Int    | Image size             |
| Quality | Int | Image quality |
| ETag | String | ETag of the output image |

### Example

#### Request

 ```shell
POST /filename.jpg?image_process HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Date: Wed, 18 Jan 2017 16:17:03 GMT
Authorization: XXXXXXXXXX
Pic-Operations: {"is_pic_info":1,"rules":[{"fileid":"test.jpg","rule":"imageView2/format/png"}]}
Content-Length: XX
 ```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
Status: 200 OK
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8z****

<UploadResult>
			<OriginalInfo>
				<Key>filename.jpg</Key>
				<Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/filename.jpg</Location>
				<ETag>&quot;eaa4e3d8fd498bbc63be3b71c46b9c61f23e3f0c&quot;</ETag>
				<ImageInfo>
					<Format>JPEG</Format>
					<Width>640</Width>
					<Height>427</Height>
					<Quality>100</Quality>
					<Ave>0xa18454</Ave>
					<Orientation>1</Orientation>
				</ImageInfo>
			</OriginalInfo>
			<ProcessResults>
				<Object>
					<Key>test.jpg</Key>
					<Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/test.jpg</Location>
					<Format>png</Format>
					<Width>640</Width>
					<Height>427</Height>
					<Size>463092</Size>
					<Quality>100</Quality>
					<ETag>&quot;eaa4e3d8fd498bbc63be3b71c46b9c61f23e3f0c&quot;</ETag>
				</Object>
			</ProcessResults>
</UploadResult>
```
