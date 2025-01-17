### COSとは何ですか。
Tencent Cloud COSはクラウド上で提供する無階層構造の分散型ストレージ製品です。低単価かつスピーディーで信頼性の高いデータストレージソリューションをユーザーにご提供します。COSは冗長化方式により、複数のアベイラビリティーゾーンにユーザーデータを保存し、複数のクライアントまたはアプリケーションスレッドが同時にこれらのデータの読み取りまたは書き込み操作を行うことを許可します。

ユーザーはCVMインスタンスまたはインターネット経由でWeb APIインターフェースを使用することで、データの保存と検索を行うことができます。COS上のデータは、ユーザーが指定ドメイン名のURLアドレスを使用し、HTTP/HTTPSプロトコルによってそれぞれの独立したデータオブジェクトの内容を保存および検索します。

Tencent Cloud COSに関するその他の情報については、[COS製品ドキュメント](https://intl.cloud.tencent.com/document/product/436)をご参照ください。


### COSとCloud File Storageの違いは何ですか。

[Cloud Object Storage（COS）](https://intl.cloud.tencent.com/document/product/436)：ディレクトリ階層がなく、データフォーマットの制限もなく、任意の数量のデータを保存でき、バケットスペースに容量の上限がなく、パーティション管理も必要ありません。データは高可用性アーキテクチャによるデプロイをサポートし、データの最終的な整合性を保障する設計となっており、ファイルロックなどの特性はサポートしていません。APIはHTTP/HTTPSプロトコルを使用してアクセスし、またSDKやツールなどの方式で業務との統合が可能です。COSにアップロードしたオブジェクトはURLアドレスによって直接アクセスまたはダウンロードできます。

[Cloud File Storage](https://intl.cloud.tencent.com/document/product/582)：通常のネットワークを使用したファイル転送プロトコルです。ファイルシステムの作成と大規模な拡張が可能で、CVMにマウントして使用する必要があります。Cloud File Storageはウェブサイト、オンラインリリース、アーカイブの各種アプリケーションでの保存が可能です。コンピューティングのスループットが高く、極めて高い可用性と持続性を有するほか、同時実行性のニーズが比較的高いケースまたは共有ストレージが必要なケースにも適しています。

### COSとCBSの違いは何ですか。

[Cloud Object Storage（COS）](https://intl.cloud.tencent.com/document/product/436)：ファイルシステム、ディレクトリ構造、ファイル数と容量の上限がないという特性を備え、Web APIインターフェースによってストレージへのアクセスと管理を行う必要があります。SDKやツールなどによる統合が可能で、CVMに依存せず単独で使用できます。COSは大規模データへのアクセスをサポートしますが、ミリ秒レベルのレスポンスやランダムリード/ライトのケースには適しません。

[Cloud Block Storage（CBS）](https://intl.cloud.tencent.com/document/product/362)：CVMと組み合わせる必要があり、ファイルシステムを使用してパーティションまたはフォーマット化を行ってからでなければマウントして使用することができません。CBSはタイプごとに、様々なパフォーマンス指標に対応可能な、 IOPSとスループット性能の異なる製品を提供しており、スタンドアローンで使用する様々なケースに適応します。


### パブリック読み取り権限が設定されたファイルのアクセスリンクが失効する場合があるのはなぜですか。

まず初めに、[COSコンソール](https://console.cloud.tencent.com/cos)のオブジェクト詳細ページでオブジェクトアドレスおよび署名リンクを取得できます。

お客様のファイルがパブリック読み取りファイルの場合：

- 第三者がお客様のファイルに直接アクセスできるようにしたい場合は、オブジェクトアドレスをそのまま使用することをお勧めします。
- 第三者に、一定の時間内にのみお客様のファイルへのアクセスを許可したい場合は、署名リンクをそのままコピーすることをお勧めします。署名リンクには署名パラメータが含まれ、有効期間は1時間です。

お客様のファイルがプライベートファイルの場合：

- 第三者がお客様のファイルに直接アクセスできるようにしたい場合は、ファイルのアクセス権限をパブリック読み取り/プライベート書き込みに変更し、オブジェクトアドレスを使用することをお勧めします。
- 第三者に、一定の時間内においてお客様のファイルへのアクセスを許可したい場合は、署名リンクをそのままコピーすることをお勧めします。署名リンクには署名パラメータが含まれ、有効期間は1時間です。


### COSの「フォルダ」または「ディレクトリ」はどのように理解すればよいですか。

COSにはフォルダやディレクトリの概念はありませんが、ユーザーの使用上の習慣に配慮し、従来のファイル管理のディレクトリ構造を参考にして、コンソール上で「フォルダ」を模した表示方法をとっています。その他の詳細については、[フォルダとディレクトリ](https://intl.cloud.tencent.com/document/product/436/13324)のドキュメントをご参照ください。

### COSファイルは削除後に復元できますか。

COSのデータ冗長化ストレージメカニズムは、サーバーなどのハードウェアに障害が発生した場合にデータを復元する必要があるケースに対応するよう設計されています。COSのデータを自主的に手動で削除した場合、または削除するよう設定した後、Tencent Cloudがその指示に従って削除したデータは復元できません。

自主的に削除するケースには次のものがあります。

- COSコンソールで単一ファイルの削除、ファイルの一括削除、フラグメントまたはバケットのクリーンアップを行った場合。
- COSCMD、COSBrowserツールでファイルを削除した場合。
- COS APIまたはSDKでファイルを削除した場合。
- COSライフサイクル管理機能によってファイルが定期的に削除された場合。
- COSの地域間コピーの全量同期機能によって、異なるリージョンのバケット間の新規追加、変更、削除操作が同期されたことで、ターゲットバケット内の同名のファイルが上書き、削除された場合。

### 誤って削除することを防ぐにはどうすればよいですか。

- バケットのファイルに対し、定期的にバックアップ操作を行います。
  - [COSCMDツール](https://intl.cloud.tencent.com/document/product/436/10976)を使用して、COS内のオブジェクトをローカルまたはサードパーティのサーバーにダウンロードします。
  - [COS Migrationツール](https://intl.cloud.tencent.com/document/product/436/30585)または地域間コピー機能を使用して、同一リージョンまたはリージョン間のバケットデータのバックアップを実現します。
  - COS API、SDKを定期的に使用し、データをCOSの他のバケットにバックアップします。
  - バージョン管理を使用して過去のバージョンのデータを保存します。
- COS権限を使用して管理します。[アクセス管理の実践](https://intl.cloud.tencent.com/document/product/436/12469)をご参照ください。
  - 読み取りと書き込みの権限を分離し、データの読み取りのみが必要な業務については、読み取り権限のみを持つサブアカウントまたは一時キーを使用してアクセスします。
  - バケット（Bucket）の権限を分離し、異なる業務ごとに、対応する業務の範囲内のバケット、ディレクトリおよび操作権限のみを承認します。
  - ルートアカウントを使用せずにCOSにアクセスします。
  - 一時キーを使用してCOSにアクセスします。
  - Tencent Cloudアカウントパスワード、CAMサブアカウントアクセス認証情報、Tencent Cloud APIキーなどの、データアクセスの認証情報を適切に保管します。


### COSはデータ統計機能をサポートしていますか。

COSはストレージデータの監視機能を提供しており、ユーザーはデータ監視ウィンドウを通じて各データの状況および傾向を把握できます。全ディスクのデータ傾向を確認したい場合は、[COSコンソール](https://console.cloud.tencent.com/cos5)の【概要】ページで、ストレージタイプの次元ごとに、ストレージ量、リクエスト数、トラフィックなどのデータを確認できます。
単一のバケットのデータ統計状況を確認したい場合は、[監視レポートの照会](https://intl.cloud.tencent.com/document/product/436/31634)をご参照ください。

このほかに、Tencent Cloudの[BCM](https://console.cloud.tencent.com/monitor/product/COS)ページで各バケットの監視情報を確認し、業務ニーズに応じて異なるアラートポリシーを設定することもできます。

### COSは画像処理機能をサポートしていますか。

COSコンソールはCloud Infiniteを統合しており、画像のズーム、トリミング、ウォーターマークの追加などの操作を行うことができます。詳細については、[画像処理の有効化](https://intl.cloud.tencent.com/document/product/436/36569)のドキュメントをご参照ください。



### COSは画像圧縮をサポートしていますか。

COSサービスは非構造化データ向けの分散型ストレージサービスであり、サービス自体は画像圧縮をサポートしていません。画像圧縮処理については、[Cloud Infinite（CI）](https://intl.cloud.tencent.com/product/ci)をご参照ください。

### COSはサムネイル機能を提供していますか。

COSサービスは非構造化データ向けの分散型ストレージサービスであり、サービス自体は画像圧縮をサポートしていません。サムネイル機能については、[Cloud Infinite（CI）](https://intl.cloud.tencent.com/product/ci)をご参照ください。

### COSでビデオファイルのトランスコードを行うことは可能ですか。

COSサービスは非構造化データ向けの分散型ストレージサービスであり、サービス自体はビデオファイルのトランスコードをサポートしていません。ビデオファイルのトランスコードについては、[Media Processing Service（MPS）](https://intl.cloud.tencent.com/product/mps)をご参照ください。

### COSはファイルのアップロード後の自動解凍をサポートしていますか。

COSサービスは非構造化データ向けの分散型ストレージサービスであり、サービス自体はファイル解凍をサポートしていませんが、SCFサービスと組み合わせることで解凍機能を実現できます。詳細については、[ファイル解凍](https://intl.cloud.tencent.com/document/product/436/35663)をご参照ください。

### COSにはどのような仕様と制限がありますか。

詳細については、[仕様と制限](https://intl.cloud.tencent.com/document/product/436/14518)のドキュメントをご参照ください。


### バケットを作成する際、バケット名の長さについてはどのような制限がありますか。

COSコンソールは2021年9月にバージョンアップを行い、バケット名の長さ制限ポリシーを再調整しました。新しい制限ポリシーでは、バケット名の最大文字数は**リージョンの略称**および**APPID**の文字数の影響により、組み合わせたリクエストドメイン名全体の文字数合計が最大60文字までとなります。ユーザーがすでに作成している長いバケット名が業務に影響することはありませんので、調整は不要です。


### COSに過去のバージョンと現在のバージョンの両方がある場合、どちらを使用すればよいですか。

COSの過去のバージョンと現在のバージョンは実装面で比較的大きな違いがあります。過去のバージョンに比べて、現在のバージョンはより豊富な機能を備えており、また過去のバージョンに新たな性能が追加されることはないため、より豊富な体験を得るためにも**現在のバージョンの使用をお勧めします**。過去のバージョンのユーザーであれば、[お問い合わせ](https://intl.cloud.tencent.com/contact-sales)いただくことで現在のバージョンをアクティブ化できます。

現在のバージョンと過去のバージョンでは、使用するAPIとSDKインターフェースのどちらにも違いがあり、過去のバージョンはJSON APIを、現在のバージョンではXML APIを使用します。2つのAPIは基盤アーキテクチャが同じで、データには互換性があり、交差使用が可能ですが、インターフェースに互換性はなく、ドメイン名も異なります。

### エラーコード情報を監視するにはどうすればよいですか。

[BCM](https://console.cloud.tencent.com/monitor/product/COS)を使用してタイプごとのHTTP戻りコード情報を取得できます。詳細な内容については、[監視とアラーム](https://intl.cloud.tencent.com/document/product/436/31649)のドキュメントをご参照ください。BCMの使用および関連データの取得方法については、BCMの[コンソールガイド](https://intl.cloud.tencent.com/document/product/248/13517)または[APIドキュメント](https://intl.cloud.tencent.com/document/product/248/37269)をご参照ください。  


### COSの可用性はどのように計算しますか。
COSは次のような可用性計算の例を、参考までにご提供しています。
明さんはTencent Cloud COSサービスを使用してEC業務に従事しています。2018年11月1日から11月30日のサービス月度内にサービス料金として計100米ドルを消費し、なおかつこのサービス月度内に2回の利用不可の状況が発生したとします。2回の利用不可状況の記録は下表のとおりです。

<table>
   <tr>
      <th>利用不可イベント番号</th>
      <th>持続時間</th>
      <th>利用不可イベントの各5分間における記録</th>
      <th>HTTP戻りコード</th>
      <th>失敗リクエスト数</th>
      <th>有効リクエスト数</th>
   </tr>
   <tr>
      <td rowspan=3><center>1<center></td >
      <td rowspan=3>15分間</td>
      <td>2018年11月15日10:00～10:05</td>
      <td>503</td>
      <td>100</td>
      <td>100</td>
   </tr>
   <tr>
      <td>2018年11月15日10:05～10:10</td>
      <td>503</td>
      <td>99</td>
      <td>100</td>
   </tr>
   <tr>
      <td>2018年11月15日10:10～10:15</td>
      <td>503</td>
      <td>98</td>
      <td>100</td>
   </tr>
   <tr>
      <td rowspan=3><center>2<center></td>
      <td rowspan=3>15分間</td>
      <td>2018年11月20日16:00 - 16:05</td>
      <td>500</td>
      <td>150</td>
      <td>150</td>
   </tr>
   <tr>
      <td>2018年11月20日16:05～16:10</td>
      <td>500</td>
      <td>148</td>
      <td>150</td>
   </tr>
   <tr>
      <td>2018年11月20日16:10～16:15</td>
      <td>500</td>
      <td>140</td>
      <td>150</td>
   </tr>
</table>

その他の時間帯では、明さんのリクエストには**すべてリクエスト成功を示すステータスコード200が返されました**。

この場合、このサービス月度全体の可用性は次のようになります。

**（1）当月の各5分間のエラー率数値を計算する**

事例の詳細によると、明さんの業務は正常な場合、各5分間のエラー率はすべて0%です。

利用不可イベント1：持続時間は2018年11月15日10:00～10:15であり、各5分間のエラー率はそれぞれ次のとおりでした。 
- 10:00～10:05の間のエラー率の計算：**100 / 100 \* 100% = 100%**
- 10:05～10:10の間のエラー率の計算：**99 / 100 \* 100% = 99%**
- 10:10～10:15の間のエラー率の計算：**98 / 100 \* 100% = 98%**

利用不可イベント2：持続時間は2018年11月20日16:00～16:15であり、各5分間のエラー率はそれぞれ次のとおりでした。
- 16:00～16:05の間のエラー率の計算：**150 / 150 \* 100% = 100%**
- 16:05～16:10の間のエラー率の計算：**148 / 150 \* 100% = 98.67%**
- 16:10～16:15の間のエラー率の計算：**140 / 150 \* 100% = 93.33%**

**（2）当該サービス月度のサービス可用性を計算する**

この事例において、

- サービス月度の全体時間：30日 \* 24時間/日 \* 60分/時間 = 43200分
- サービス月度内の5分間の総数：43200分 / 5分 = 8640
- サービス月度内の利用不可だった5分間の総数：(15 + 15)分 / 5分 = 6
- サービス月度内の5分間エラー率の和：(100% + 99% + 98% + 100% + 98.67% + 93.33%) + (8640 - 6) \* 0% = 589%

この月のサービス可用性：**(1 - 589% / 8640) \* 100% = 99.93%**

**（3）賠償項目の計算**

この事例ではサービス可用性は99.93%であり、99.95%の可用性基準より低く、99.9%より高いです。賠償基準に基づき、Tencent Cloud COSサービスはユーザーに対し、月間サービス料総額の20%、すなわち20米ドルを賠償する必要があります。
明さんがサービス月度終了後六十（60）自然日以内、すなわち2019年1月29日までにチケットを提出して賠償申請を行えば、Tencent Cloudはクーポン配付の形で、明さんの損失に応じた賠償を行います。

### COSサービスを利用停止または課金を停止するにはどうすればよいですか。


COSにはワンクリックでサービスを停止する機能はありません。COSサービスを長期間利用しない場合は、データをアーカイブストレージタイプに移行し、ストレージコストを削減することを選択できます。移行の操作については[ライフサイクルの設定](https://intl.cloud.tencent.com/document/product/436/14605)をご参照ください。

今後COSサービスを利用しない場合は、COS内の全データ（アップロード未完了のファイルフラグメント、過去のバージョンのオブジェクトなどを含む）を完全に削除することで、それ以上課金されないようにすることが可能です。アカウントを抹消する必要はありません（他のTencent Cloudサービスをご利用の場合、アカウントを抹消すると影響が生じます）。

>?COS内のデータおよびアップロード未完了のファイルフラグメントの削除については、[オブジェクトの削除](https://intl.cloud.tencent.com/document/product/436/13323)および[フラグメントの削除](https://intl.cloud.tencent.com/document/product/436/31632)をご参照ください。

完全削除の操作を開始する前に、次の事項に必ずご注意ください。

- データは完全に削除されると復元できません。適時にデータのバックアップを行ってください。
- 料金の決済の周期に注意し、アカウントに支払い遅延が発生しないようにする必要があります。詳細については、[課金周期](https://intl.cloud.tencent.com/document/product/436/16871)をご参照ください。
- アカウント残高不足により支払い遅延が発生した（アカウント残高が0未満となった）場合、リソースパックの有効期間中かどうかにかかわらず、COSは支払い遅延発生から24時間後にサービスを停止します。
- アカウントが無料利用枠を利用している場合、支払い遅延によるサービス停止後は利用できなくなります。
