### COSにはプライベートネットワークドメイン名はありますか。

COSのデフォルトのオリジンサーバードメイン名の形式は&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.comです。デフォルトでパブリックネットワークアクセスおよび同一リージョン内のプライベートネットワークアクセスをサポートしています。プライベートネットワーク環境下でこのドメイン名を使用してCOSにアクセスすると、COSはインテリジェントにプライベートIPに解決します。その際に発生するトラフィックはすべてプライベートネットワークトラフィックであり、トラフィック料金はかかりません。



