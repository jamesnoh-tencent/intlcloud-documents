従量課金（後払い）方式はCloud Object Storage(COS)のデフォルトの課金方式であり、[全リージョン](https://intl.cloud.tencent.com/document/product/436/6224)でサポートされています。ユーザーのストレージ容量、リクエスト、トラフィック等の課金項目の具体的な使用量に応じて課金され、1日単位または月単位でユーザーアカウントから差し引かれます。


## 製品料金

COSの従量課金料金に関しては、[製品価格](https://intl.cloud.tencent.com/pricing/cos)をご参照ください。

## 課金項目

COSの各課金項目と、課金項目の計算式の説明は次のとおりです。
<table>
   <tr>
      <th>課金項目</th>
      <th>課金項目の説明</th>
      <th>課金の計算式</th>
   </tr>
   <tr>
      <td nowrap="nowrap">ストレージ容量料金</td>
      <td>ストレージ容量のサイズに基づいて計算されます。ストレージタイプごとに単価が異なります</td>
      <td nowrap="nowrap"><li>ストレージ容量料金 = ストレージ容量単価 * 月間ストレージ容量<br><li>月間ストレージ容量 = 当月の「1日あたりのストレージ容量」の合計 / 当月の日数<br><li>1日あたりのストレージ容量 = 当日の「5分ごとのストレージ容量」の合計 / 288（サンプリングポイント数）</td>
   </tr>
   <tr>
      <td>リクエスト料金</td>
      <td>リクエスト料金はリクエストの回数に基づいて計算されます。リクエスト単価はストレージタイプごとに異なります</td>
      <td nowrap="nowrap">リクエスト料金 = リクエスト1万回あたりの単価 * 月間累計リクエスト回数 / 10000</td>
   </tr>
   <tr>
      <td>データ取得料金</td>
      <td>データ取得量に基づいて計算されます。低頻度ストレージおよびアーカイブストレージタイプのダウンロード時にこの項目の料金が加算され、取得単価はストレージタイプごとに異なります</td>
      <td nowrap="nowrap">データ取得料金 = 1GBあたりの単価 * 月間データ取得量</td>
   </tr>
   <tr>
      <td>トラフィック費用</td>
      <td>パブリックネットワークダウンストリームトラフィック、CDN back-to-originトラフィック、地域間コピートラフィック、グローバルアクセラレーショントラフィックが含まれます。トラフィックのタイプごとに料金が異なります</td>
      <td nowrap="nowrap">トラフィック料金 = 1GBあたりの単価 * 1日の累計トラフィック</td>
   </tr>
   <tr>
      <td rowspan=4>管理機能料金</td>
      <td rowspan=4>管理機能料金とは、ユーザーが管理機能（リスト、検索、一括処理、オブジェクトタグなどの機能）を有効化し、使用した際に発生する料金を指します。現時点での管理機能料金には、リスト機能料金、検索機能料金、バッチ処理料金、オブジェクトタグ料金があります
      <td nowrap="nowrap">リスト機能料金 = リストアップしたオブジェクト数/100万 * 単価</td>
   </tr>
   <tr>
      <td nowrap="nowrap">検索機能料金 = 1GBあたりの単価 * 1日の累計データ検索量</td>
   </tr>
   <tr>
			<td nowrap="nowrap">バッチ処理料金にはタスク料金とオブジェクト処理料金が含まれます。<br><li>タスク料金 = 作成したタスク数 * 単価<br><li>オブジェクト処理料金 = オブジェクト処理数/10000 * 単価</td>
   </tr>
   <tr>
			<td nowrap="nowrap">オブジェクトタグ料金 = 1万個あたりのタグ数 * 単価</td>
   </tr>
</table>


> ?課金項目の詳細な説明および課金制限については、[課金項目](https://intl.cloud.tencent.com/zh/document/product/436/33776)のドキュメントをご参照ください。


## 課金周期

COS課金項目には月単位の課金と1日単位の課金の2種類があります。課金周期は課金項目ごとに異なります。具体的には下表のとおりです。

| 課金項目       | 課金周期 | 説明                                   |
| ------------ | -------- | -------------------------------------- |
| ストレージ容量料金 | 月単位課金 | 毎月1日に、前月1か月間に発生した料金を決済        |
| リクエスト料金 | 月単位課金 | 毎月1日に、前月1か月間に発生した料金を決済        |
| データ取得料金 | 月単位課金 | 毎月1日に、前月1か月間に発生した料金を決済        |
| トラフィック料金 | 1日単位課金 | 毎日、前日の00:00 - 23:59:59に発生した料金を決済        |
| 管理機能料金 | 1日単位課金 | 毎日、前日の00:00 - 23:59:59に発生した料金を決済 |

>?
> 請求書システムにはある程度の遅延が発生する可能性があり、毎日または毎月の請求書は当日8:00頃に発行されます。


## 事例の説明

小雲さんは2019年3月1日にCOSに100Gの標準ストレージファイルをアップロードし、3月15日にパブリックネットワークを通じて10Gのデータをダウンロードし、それ以外の時間は何も操作を行いませんでした。この場合、3月に発生する料金の合計は次のとおりです。

- 標準ストレージ容量料金：当月のストレージ容量合計100Gの料金。
- トラフィック料金：当月のパブリックネットワークダウンストリームトラフィック合計10Gの料金。
- リクエスト料金：当月のデータアップロードおよびダウンロードによって発生したリクエスト数の料金。

