## Overview

The ZIP decompression feature is a data processing solution provided by Tencent Cloud COS based on [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583). When you upload a compressed file to a bucket with a ZIP decompression rule configured, the SCF preset by COS will be triggered automatically to decompress the file into the specified bucket and directory. The decompression flow is shown as follows:

![Decompression Flow](https://main.qcloudimg.com/raw/4899b5c92bb085a0f18a522dfae344ae.jpg)

You can use the ZIP decompression by the following methods:
- Console: ZIP files uploaded to the bucket will be automatically decompressed after you configure a ZIP decompression function in the console.
- API: You can call the corresponding API to trigger the ZIP decompression operation.

This document describes how to decompress ZIP files in the console. For using API to decompress ZIP files, see [Using API to Decompress ZIP Files](https://intl.cloud.tencent.com/document/product/436/45164).


## Notes

- ZIP decompression supports decompressing `.zip` files.
- If you have added a ZIP decompression rule to your bucket via the COS console, you can view the created ZIP decompression function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **Do not** delete the function. Otherwise, your rule may not take effect.
- Regions where SCF is available support ZIP file decompression, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong, Singapore, Mumbai, Toronto, and Silicon Valley, and more. For more supported regions, please see [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).
- The directory or file name in your package must be UTF-8 or GB 2312 encoded. Otherwise, the directory or file name might be garbled after decompression, or the decompression may be interrupted. If an error is reported, you can click **View Log** on the right of the function to redirect to the SCF console to view log details.
- The decompression service is not supported for archived files. To decompress an archived package, please restore it first. For detailed directions, please see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
- The maximum processing time for decompressing a single compressed file is 900 seconds, beyond which the decompression task fails. Limits of the COS file decompression feature are subjected to SCF. For more limits, please see [SCF Limits](https://intl.cloud.tencent.com/document/product/583/11637).
- The ZIP decompression feature depends on the SCF service which provides users with a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the free tier according to [SCF Product Pricing](https://intl.cloud.tencent.com/document/product/583/12280). With decompression, the larger your package, the more your resource usage; the more often you decompress packages, the more invocations you will need to use.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Choose **Bucket List** on the left sidebar.
3. Click the bucket you want to add a decompression rule for.
4. Choose **Function Service** on the left sidebar, and click **ZIP Decompression Function**.
>! If you haven’t activated the SCF service, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
5. Click **Add Function** and configure the following parameters: 
![img](https://qcloudimg.tencent-cloud.cn/raw/6400de55d3851fa371050e0cc6f38d63.png)
 - **Function Name**: uniquely identifies a function and cannot be modified after it is created. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Event Type**: an event is an operation that triggers SCF. Take upload as an example. You can initiate an upload by calling the `PUT Object` or `POST Object` API. If you choose **Create using PUT method** as the event type, decompression will only be triggered by a package uploaded via the `PUT Object` API.
>! If you intend to upload files to the bucket using multiple ways, such as simple upload, multipart upload, and cross-bucket replication, you are advised to choose **File upload** as the event type.
>
 - **Trigger Condition**: the upload path that will trigger SCF. If you select **Specified prefix**, SCF will be triggered only when the package is uploaded to a path with the specified prefix. If you choose **Not specifying prefix**, SCF will be triggered as long as a package is uploaded to any location of the bucket.
>! If the destination prefix configured overlaps with the trigger condition, a loop may be triggered, which should be avoided. For example, if the destination prefix is `prefix`, and the trigger condition is` pre`, a decompression loop will be triggered when you upload a `pref` package.
>
 - **SCF Authorization**: Required. To decompress a compressed file, SCF should be authorized to read the package from your bucket and upload the decompressed files to the specified location.
6. Click **Next** and configure the following in the pop-up window: 
![img](https://qcloudimg.tencent-cloud.cn/raw/e237f6c35b1ef440b608e28d4a951757.png)
 - **Decompression Format**: supported compression format.
 - **Destination Bucket**: a bucket to store the compressed files
 - **Destination Path**: a path to store the decompressed files of the packages that are matched. To prevent unnecessary fees from triggering the loop, it is recommended that you set a destination path different from the prefix.
 - **Extra Prefix**:
    - Package name: decompresses the package to a directory named the same as the package itself.
    - Directory of the package: decompresses the package to a directory named the same as the directory of the package.
    - Full path of the package: decompresses the package to a prefix that is named the complete path of the package.
    - Empty: decompresses the package directly to the destination path.
>? Example:
> Upload the package `123` to the `test` directory of the bucket `bucket1-125000000`, and then decompress the package to the root directory of the destination bucket `bucket2-1250000000`. If you have set one of the following extra prefixes, the storage path of the compressed files after decompression will be as follows:
>- Package name: bucket2-1250000000/123
>- Directory of the package: tbucket2-1250000000/test
>- Full path of the package: bucket2-1250000000/test/123
>- Empty: bucket2-1250000000
>
 - **Forbid Recursive Triggering**: **Enable** does not continue to decompress ZIP packages that are decompressed from the package, while **Disable** does.
7. Click **Confirm**.
![img](https://qcloudimg.tencent-cloud.cn/raw/cf15a5374c4249235c0b925d83eb8ad9.png)
You can perform the following operations on the created function:
 - Click **Log** to view the historical running status of the ZIP decompression. If an error is reported, you can click **View Log** to quickly redirect to the SCF console to view the error log details.
 - Click **Details** to view the ZIP decompression configuration rule.
 - Click **Edit** to modify the ZIP decompression rule.
 - Click **Delete** to delete the ZIP decompression rule.
