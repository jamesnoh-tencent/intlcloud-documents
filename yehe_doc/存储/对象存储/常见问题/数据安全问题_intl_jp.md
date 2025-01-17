

## バージョン管理に関するご質問

### 誤って削除したデータを元に戻すことはできますか。

人為的に誤って削除されたファイルの復元は現時点ではサポートしていません。バケットのバージョン管理機能を有効にすると、バケット内にオブジェクトの複数のバージョンを保存でき、なおかつ指定したバージョンのオブジェクトを検索、削除または復元できるようになります。ユーザーが誤って削除したデータや、アプリケーションプログラムの障害によって消失したデータの回復に役立ちます。詳細については、[バージョン管理の設定](https://intl.cloud.tencent.com/document/product/436/19881)をご参照ください。

### COSではデータ障害復旧の問題をどのように解決していますか。

COSは次の方法で障害復旧を実現できます。

1. [バージョン管理](https://intl.cloud.tencent.com/document/product/436/19883)を有効にします。バージョン管理は同一のバケット内に同一オブジェクトの複数のバージョンを保存するために用いられます。バージョン管理の設定方法については、[バージョン管理の設定](https://intl.cloud.tencent.com/document/product/436/19884)をご参照ください。
2. [バケットのコピー](https://intl.cloud.tencent.com/document/product/436/19237)を使用してリモートディザスタリカバリを実現できます。詳細については、[バケットコピーの設定](https://intl.cloud.tencent.com/document/product/436/19239)をご参照ください。


### COSバケットでバージョン管理を有効にした後、過去のバージョンのデータを削除するにはどうすればよいですか。

過去のバージョンのファイルを削除するには、[ライフサイクルの設定](https://intl.cloud.tencent.com/document/product/436/14605)で**過去バージョンオブジェクト管理**オプションを有効にすることで、過去のバージョンのオブジェクトを移行または削除することができます。


### COSで同名のファイルをアップロードしても上書きされないように設定することは可能ですか。

COSで同名のファイルをアップロードすると、デフォルトでは上書きされます。バケットの[バージョン管理機能](https://intl.cloud.tencent.com/document/product/436/19881)を有効にすると、バケット内にオブジェクトの複数のバージョンを保存できるようになります。バージョン管理に関するその他の説明については、[バージョン管理の概要](https://intl.cloud.tencent.com/document/product/436/19883)をご参照ください。

### COSで指定したバージョンのファイルをダウンロードするにはどうすればよいですか。

APIインターフェースまたはSDKを使用してファイルをダウンロードする場合は、リクエストパラメータversionIdを追加することで実現できます。APIの詳細な操作については、[GET Object](https://intl.cloud.tencent.com/document/product/436/7753)のドキュメントをご確認ください。

コンソールからファイルをダウンロードする場合は、上部のナビゲーションバーで過去のバージョンのステータスを**表示する**に設定すると、必要なファイルをダウンロードすることができます。

### COSで過去のバージョンのファイルを一括削除するにはどうすればよいですか。

COSBrowserツールを使用すると、バケット内の過去のバージョンのファイルをワンクリックで削除することができます。詳細については、[COSBrowserのデスクトップでの使い方](https://intl.cloud.tencent.com/document/product/436/32565)をご参照ください。

また、[ライフサイクルポリシーの設定](https://intl.cloud.tencent.com/document/product/436/14605)によって実現することもできます。ライフサイクルポリシーを設定する際は、現在のバージョンのファイル管理を無効にし、過去のバージョンのファイル管理を有効にし、ファイルを変更から1日後に削除するよう設定します。

## 地域間コピーに関するご質問

### COSで地域間コピーを有効にした場合、コピーする際に使用するのはプライベートネットワークとパブリックネットワークのどちらですか。

COSの地域間コピー機能はデフォルトでプライベートネットワークを使用してコピーを行います。

>?地域間コピー機能を使用すると、それに応じた地域間コピートラフィック料金が発生します。現時点では対応するリソースパックはなく、発生した料金は翌日0時に決済され、アカウント残高から差し引かれます。

### 2つのリージョンのCOSリソースを同期することは可能ですか。

同一アカウントの2つのリージョンのCOSリソースを、地域間コピー機能によって増分コピーすることが可能です。詳細については、[地域間コピーの設定](https://intl.cloud.tencent.com/document/product/436/19235)をご参照ください。

### あるアカウントのCOSリソースを別のアカウントのCOSにすばやく移行（またはコピー）するにはどうすればよいですか。

データマイグレーションについては、COSMigrationツールによってバケット間の移行が実現できます。[COS Migrationツール](https://intl.cloud.tencent.com/document/product/436/15392)をご参照ください。あるいは地域間コピーを設定することでバケット間のリソースコピーを実現することもできます。[バケットコピーの設定](https://intl.cloud.tencent.com/document/product/436/19235)をご参照ください。

### 地域間コピー機能は既存データのコピーをサポートしていますか。

地域間コピー機能は既存データのコピーをサポートしていません。既存データをコピーしたい場合は、[バッチ処理](https://intl.cloud.tencent.com/document/product/436/32958)のドキュメントを参照し、既存データの一括コピーを行うことができます。

### バケットのコピー機能を有効にすると、ソースバケットでファイルを削除した場合、ターゲットバケットで操作が同期されますか。

バケットのコピー機能を有効にしたソースバケットにおいて、COSは次のコンテンツをコピーします。
- バケットコピールールを追加した後に、ユーザーがソースバケットに新たにアップロードしたあらゆるオブジェクト。
- オブジェクトのメタデータおよびバージョンIDなどのオブジェクトの属性情報。
- オブジェクトの操作に関する情報。新たに追加された同名のオブジェクト（新規追加オブジェクト）、削除されたオブジェクトなど。

>?
>- ソースバケット内で特定のオブジェクトのバージョンを削除するよう指定（バージョンIDを指定）した場合、その操作はコピーされません。
>- ソースバケットに、例えばライフサイクルルールのような、バケットレベルの設定を追加している場合、これらの設定によって発生したオブジェクトの操作もターゲットバケットにはコピーされません。

その他の説明については、ドキュメント[コピーアクションの説明](https://intl.cloud.tencent.com/document/product/436/19923)をご参照ください。

## データ暗号化に関するご質問

### COSはファイルの暗号化をサポートしていますか。
COSはバケットの暗号化、オブジェクトの暗号化などのファイル暗号化方式をサポートしています。バケット暗号化の操作ガイドについては[バケット暗号化の設定](https://intl.cloud.tencent.com/document/product/436/33455)のドキュメントを、オブジェクトの暗号化については[オブジェクト暗号化の設定](https://intl.cloud.tencent.com/document/product/436/30929)のドキュメントをそれぞれご参照ください。

### COSファイルの暗号化はパフォーマンスに影響しますか。
ファイルの暗号化には、お客様側のキー、またはCOSホスティングキー、またはKMSキーを使用してファイルの内容を暗号文にすることが必要です。そのためある程度のパフォーマンスロスが発生し、それは主にアクセス遅延の増加として表れます。この遅延の増加は大容量ファイルの読み取り/書き込みではあまり目立ちませんが、小容量ファイルの読み取り/書き込みにはある程度の影響を及ぼします。

### 暗号化されたファイルを取得するにはどうすればよいですか。

ファイルがすでに暗号化されている場合、ファイルを取得するには、ファイルを読みとる際に暗号化ヘッダーを挿入する必要があります。暗号化ヘッダーは暗号化アルゴリズムによって異なります。具体的な説明は、[サーバーの暗号化ヘッダー](https://intl.cloud.tencent.com/document/product/436/7728)をご参照ください。


## その他の問題

### COSの標準ストレージ、低頻度ストレージ、アーカイブストレージデータにはすべてバックアップがありますか。

COSのデータはマルチレプリカまたはイレージャーコーディング方式によって下層で保存されます。分散型ストレージエンジンが1つのリージョンの複数のアベイラビリティーゾーンに分散することで、99.999999999%の信頼性を実現します。マルチレプリカおよびイレージャーコーディングストレージは下層のロジックのため、ユーザーには見えません。
