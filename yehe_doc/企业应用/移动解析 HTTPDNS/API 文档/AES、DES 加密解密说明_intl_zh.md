
## 操作场景
使用 DES、AES 加密算法可以对请求参数进行加密，并对其响应数据解密，防止明文请求在传输过程中被恶意篡改。本文将指导您如何使用 DES、AES 加密算法。

>? 使用 HTTPS 请求方式查询，传输的数据会因为 TLS 通道而被加密保护，因此不需要主动对传入的数据额外加密。
## 前提条件
- [已开通移动解析 HTTPDNS](https://intl.cloud.tencent.com/document/product/1130/44461) 并已获取授权 ID 和加密密钥及 HTTPS Token 等配置信息。详情可参见 [配置信息说明](https://intl.cloud.tencent.com/document/product/1130/44467)。
- 已在移动解析 HTTPDNS 控制台添加需要查询的域名。详情可参见 [添加域名](https://intl.cloud.tencent.com/document/product/1130/44465)。

## 操作流程

**步骤1：确定加密方式。**
目前移动解析 HTTPDNS，HTTP 请求查询方式支持 DES、AES、两种加密方式。
>? 
>- 若您使用 HTTPS 请求查询方式，详情可参见 [HTTPS 请求方式查询](https://intl.cloud.tencent.com/document/product/1130/44469)。
>- 使用对应的密钥和算法将要解析的域名进行加密（如需使用 ip 参数，也需要将该参数值进行加密），并将加密后的结果与 ID （不需要加密）作为请求参数。
>
**步骤2：发送加密的请求。**
**步骤3：接受加密的应答。**
**步骤4：将结果解密，即可获得所查询的域名对应的解析结果。**


## 加密与解密算法使用说明[](id:state)

### DES 算法
>? 使用 DES 进行加密与解密，密码长度为8字节，分组加密模式为 `ECB`，Padding 算法是 `PKCS5Padding` 。
>
加密后数据使用 `Hex（Base16）` 编码，将二进制数据转换为可见十六进制字符标识，`Hex` 编码后的数据长度将会加倍。具体流程如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/e6a82a00c98cc6ac15862bfca214ad32.png)

解密响应数据，先使用 `Hex` 解码为二进制数据，再使用 DES 算法解密为明文数据。具体流程如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/5210e5a220e55e0ecc9d54817c78f746.png)

例如：您的域名为 `www.dnspod.cn`、加密密钥为：`dnspodpass`。流程如下：
1. 在 [HTTPDNS 控制台](https://console.cloud.tencent.com/httpdns/domain) 添加域名。
2. 使用 `DES-ECB-PKCS5` 加密算法与 [DES 加密密钥](https://intl.cloud.tencent.com/document/product/1130/44467) `dnspodpass` 加密域名将得到加密字符串 `87ae992c1321f299da3c0210a9900ae7`。
3. 使用接口 `curl "http://119.29.29.98/d?dn=87ae992c1321f299da3c0210a9900ae7&id={授权ID}"` 请求 A 记录将得到
数据长度加倍的加密字符串，如：`55915a682ea20840ff74aa6e7bebf11454ed0f4050a63e93e6e89521553a01a8`。
4. 得到加倍的加密字符串后，使用 `DES-ECB-PKCS5` 加密算法与 [DES 加密密钥](https://intl.cloud.tencent.com/document/product/1130/44467) `dnspodpass` 进行解密后将得到明文的信息 `121.12.53.35;106.227.19.35`。

>?以上字符串仅做示例使用，用于正常请求将无法使用。


### AES 算法
>?使用 AES 进行加密与解密，密钥长度为 16 个字符，分组加密模式为 `CBC`，Padding 算法是 `PKCS7`。
>
CBC 模式要求使用随机化 `IV` 作为初始加密与解密输入，因此该 `IV` 也会被带入到请求和响应中。加密后的数据，连同 `IV` 一起使用 `Hex` 编码，转换为可见十六进制标识。具体流程如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/40c662defb24b83cb2f0565cb9e8e37c.png)
解密时，使用 `Hex` 解码为二进制数据，前16字节为 `IV` 值，`IV` 后面为待使用 AES 算法解密的数据。使用 AES 算法解密后即为明文数据。具体流程如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/da8d8f54eec6140d2262e7e37cad62e8.png)





