

## Versioning

### Can I restore accidentally deleted data?

No. However, you can enable versioning for your bucket so that you can store multiple versions of an object in a bucket, and extract, delete, or restore a specific object version. Versioning allows you to restore data lost due to accidental deletion or application failures. For more information, please see [Setting Versioning](https://intl.cloud.tencent.com/document/product/436/19881).

### What is COS’s solution to disaster recovery?

You can achieve disaster recovery in COS by:

1. Enabling [versioning](https://intl.cloud.tencent.com/document/product/436/19883), which allows you to store multiple versions of an object in the bucket. For detailed directions, please see [Versioning Configuration](https://intl.cloud.tencent.com/document/product/436/19884).
2. Using [cross-bucket replication](https://intl.cloud.tencent.com/document/product/436/19237) to achieve remote disaster recovery. For more information, please see [Cross-Bucket Replication Configuration](https://intl.cloud.tencent.com/document/product/436/19239).


### How can I delete noncurrent object versions after I enable versioning for a bucket?

You can [set a lifecycle rule](https://intl.cloud.tencent.com/document/product/436/14605) and enable **Managing historical versions** to transition or delete noncurrent object versions.


### Can a newly uploaded object not overwrite the old one that has the same name?

No. By default, the old object with the same name will be overwritten by the new one. However, you can enable [versioning](https://intl.cloud.tencent.com/document/product/436/19881) for your bucket so that multiple object versions can be preserved. For more information, please see [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883).

### How can I download a specific version of object?

If you download with APIs or SDKs, add the `versionId` request parameter. For the API calling directions, see [GET Object](https://intl.cloud.tencent.com/document/product/436/7753).

If you download via the console, set the historical versions to **Display** in the top navigation bar so that you can download the desired object version.

### How can I delete noncurrent object versions in batches?

You can use the COSBrowser tool to one-click delete noncurrent object versions in batches. For more information, please see [COSBrowser User Guide for Desktop Version](https://intl.cloud.tencent.com/document/product/436/32565).

You can also [configure a lifecycle policy](https://intl.cloud.tencent.com/document/product/436/14605) to delete objects that were modified more than 1 day ago for noncurrent object versions.

## Cross-Region Replication

### Does cross-region replication use a private or public network?

By default, cross-region replication uses a private network.

>?Note that cross-region replication incurs traffic fees, which cannot be redeemed with a resource pack yet. The fees incurred will be deducted from your account at 00:00 the next day.

### Can I sync resources between two regions?

Yes. Resources under the same account can be synced between two regions. You can [set cross-bucket replication](https://intl.cloud.tencent.com/document/product/436/19235) to replicate objects incrementally.

### How to quickly migrate resources from one account to another account?

You can use [COS Migration](https://intl.cloud.tencent.com/document/product/436/15392) to migrate data between buckets. Alternatively, you can [set cross-bucket replication](https://intl.cloud.tencent.com/document/product/436/19235).

### Does cross-bucket replication support replicating existing data?

No. You can use [Batch Operation](https://intl.cloud.tencent.com/document/product/436/32958) instead.

### If I enable cross-bucket replication and delete a file from the source bucket, will the file be deleted as well in the destination bucket?

In a source bucket with cross-bucket replication enabled, COS will replicate the following:
- Any new objects uploaded to the source bucket after the cross-bucket replication rule is added.
- Object attributes such as object metadata and version ID.
- Object operations, such as adding an object of the same name (equivalent to adding a new object) and deleting an object.

>?
>- If you specify an object version to delete in the source bucket by specifying a version ID, COS will not replicate this delete operation.
>- If you add a bucket-level configuration such as a lifecycle rule to the source bucket, COS will not replicate any resulting object operations.

For more information, please see [Cross-Bucket Replication Actions](https://intl.cloud.tencent.com/document/product/436/19923).

## Data Encryption

### Does COS support data encryption?
Yes. COS supports encryption such as bucket encryption and object encryption. For more information, please see [Setting Bucket Encryption](https://intl.cloud.tencent.com/document/product/436/33455) and [Setting Object Encryption](https://intl.cloud.tencent.com/document/product/436/30929).

### Does COS encryption affect performance?
A client-side/COS-managed/KMS key is used to encrypt the file content into ciphertext, which affects performance to some extent (mainly by increasing access delay). The delay does not significantly affect large object reads/writes, but has a certain impact on small object reads/writes.

### How can I get an encrypted object?

To get an encrypted object, include an encryption header when reading it. The encryption header differs according to the encryption algorithm. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


## Other

### Are there backups for the STANDARD, STANDARD_IA, and ARCHIVE storage classes?

COS data is stored at the underlying layer using multiple replicas or erasure coding (both are imperceptible to users). The storage engines are distributed across multiple availability zones in a region, making the data reliability 99.999999999%.
