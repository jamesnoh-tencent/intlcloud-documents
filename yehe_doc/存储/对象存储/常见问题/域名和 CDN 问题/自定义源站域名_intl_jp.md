### 独自ドメイン名を使用してオブジェクトにアクセスするにはどうすればよいですか。

カスタムドメイン名をバインドすることで実現できます。詳細については、[カスタムオリジンサーバードメイン名の有効化](https://intl.cloud.tencent.com/document/product/436/31507)をご参照ください。

### カスタムドメイン名を使用するには、Tencent CloudのICP登録を行う必要がありますか。

状況に応じて判断してください。

- ドメイン名で国内のCDNにアクセスするには、ICP登録が必要です。ただしICP登録はTencent Cloudを通じて行わなくてもよく、アクセスするドメイン名が確実にICP登録されていればアクセスできます。
- ドメイン名で海外のCDNにアクセスする場合は、ICP登録は不要です。

### COSのカスタムドメイン名はHTTPSをサポートしていますか。

COSのカスタムドメイン名におけるHTTPS設定機能は現在アップグレード中です。現時点では香港、上海、成都、北京、南京などのリージョンでホスト証明書をサポートしており、その他のリージョンでも順次サポート予定です。未対応のリージョンでは、[カスタムドメイン名の設定によるHTTPSアクセスのサポート](https://intl.cloud.tencent.com/document/product/436/11142)のドキュメントを参照し、ドメイン名にリバースプロキシを設定する方法で実現できます。

### COSにファイルをアップロードした際に、カスタムドメイン名のアクセスリンクを返すようにするにはどうすればよいですか。

COSは現時点ではファイルのアップロード後にカスタムドメイン名のアクセスリンクを返す設定をサポートしていませんが、ドメイン名のスプライシングによって実現できます。カスタムドメイン名を[デフォルトドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)に置き換えて使用するだけです。

### カスタムドメイン名を使用してCOSにアクセスするには、CDNを有効にする必要がありますか。

カスタムドメイン名を使用したCOSアクセスは、CDNを有効にしなくても可能です。[COSコンソール](https://console.cloud.tencent.com/cos5)にログインし、カスタムオリジンサーバードメイン名を設定できます、詳細な操作については、[カスタムオリジンサーバードメイン名の有効化](https://intl.cloud.tencent.com/document/product/436/31507)のドキュメントをご参照ください。

### CDNコンソールでオリジンサーバーを変更すると、COSコンソールの元のカスタムドメイン名が消えてしまいましたが、なぜですか。

**一度バージョンV5コンソールを使用し、JSONバージョンを有するドメイン名を設定した場合、COS V5コンソールでは新しいドメイン名を表示できなくなります。**バケットにJSONドメイン名が設定されているかどうかをチェックし、JSONバージョンドメイン名の設定をXMLドメイン名に変更してください。

### カスタムドメイン名をCOSバケットにバインドする場合、先に軽量サーバーの解決を削除する必要がありますか。

1つのドメイン名には1つのCNAMEレコードしか設定できないため、 先に軽量サーバーの解決関係を削除してから、ドメイン名の解決関係をCOSのバケットにバインドする必要があります。


### ドメイン名の解決が有効になっていない、またはCNAMEが有効になっていないと表示された場合は、どうすればよいですか。

ドメイン名の解決またはCNAMEの設定後、有効になるまでには数分間かかります。しばらく待ってから、カスタムオリジンサーバードメイン名を使用してバケットへのアクセスをお試しください。それでも有効にならない場合は、DNSコンソールにログインし、解決関係の設定が正しいかどうか確認することができます。

