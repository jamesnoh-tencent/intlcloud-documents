低頻度ストレージ、アーカイブストレージおよびディープアーカイブストレージタイプのデータを読みとる際に、データ取得料金が発生する場合があります。データ取得量は、ユーザーが実際に読み取った上記のタイプのデータのサイズに基づいて計算されます。

>?
>- タイプごとのデータ取得単価については、[製品価格](https://buy.cloud.tencent.com/price/cos)をご確認ください。
>- ストレージタイプに関するその他の説明は、[ストレージタイプの概要](https://cloud.tencent.com/document/product/436/33417)をご参照ください。
>


## 低頻度ストレージのデータ取得料金

| 課金項目説明                                                   | 適用されるストレージタイプ | 適用される課金方式 |
| ------------------------------------------------------------ | -------------- | -------------- |
| 低頻度ストレージタイプのデータは、データの読み取りまたはダウンロードを行う場合、バックエンドが先にデータを取得してからでなければ読み取りまたはダウンロードを行うことができません。このタイプのデータの取得料金は、ユーザーが実際に読み取ったデータのサイズに基づいて計算されます。 | 低頻度ストレージ       | 従量課金       |

## アーカイブストレージ/ディープアーカイブストレージのデータ取得料金

| 課金項目説明                                                   | 適用されるストレージタイプ            | 適用される課金方式 |
| ------------------------------------------------------------ | ------------------------- | -------------- |
| アーカイブストレージ、ディープアーカイブストレージタイプのデータは、復元（解凍）しなければ読み取りとダウンロードを行うことができません。このタイプのデータの読み取りとダウンロードを行いたい場合は、先に標準ストレージタイプのレプリカとして復元する必要があります。この場合、データの取得は解凍（アーカイブデータを標準データに復元するプロセス）とも呼ばれます。 </br></br>料金は、アーカイブのタイプと復元モードの違いに応じて次の数種類に区分されています。<li>アーカイブクイック取得料金<br><li>アーカイブ標準取得料金</li><li>アーカイブ一括取得料金</li><li>ディープアーカイブ標準取得料金</li><li>ディープアーカイブ一括取得料金</li> | アーカイブストレージ</br>ディープアーカイブストレージ | 従量課金       |


## データ取得料金の課金方式と計算方法

<table>
   <tr>
      <th>課金方式</td>
      <th>適用される課金項目</td>
      <th>計算方法 </td>
   </tr>
   <tr>
      <td rowspan=2>従量課金</td>
      <td><li>低頻度ストレージデータ取得料金</li><li>アーカイブストレージデータ取得料金</li></td>
      <td><li>月次決済<br><li>データ取得料金 = 1GBあたりの単価 x 月間データ取得量</td>
   </tr>
   <tr>
      <td>ディープアーカイブ取得料金</td>
      <td><li>日次決済<br><li>データ取得料金 = 1GBあたりの単価 x 1日あたりのデータ取得量"</td>
   </tr>
</table>


## 課金の例

>?
>- 次の例に記載した料金価格は参考用です。実際の価格についてはCOS[製品価格](https://buy.cloud.tencent.com/price/cos)をご参照ください。
>- ストレージ量は2進数で計算されます。例えば、1TB = 1024GBとなります。
>- リクエスト料金は**1万回**を最小計数単位とします。このため、月間累計リクエスト回数が1万回未満の場合は、リクエストの成否にかかわらず、1万回として計算されます。
>

### 事例：低頻度ストレージ容量料金 + 低頻度ストレージデータ取得料金 + 低頻度ストレージリクエスト料金 + パブリックネットワークダウンストリームトラフィック料金

ユーザーのBさんが2020年11月1日に5GBの低頻度ストレージタイプのデータを広州リージョンのCOSバケットにアップロードし、翌日にパブリックネットワークを使用し、かつCDNを有効化せずにこのデータを読みとり、100回のリクエストが発生し、それ以外の時間には他の操作を何も行わなかったとします。ストレージ容量料金、リクエスト料金、データ取得料金は月次決済、トラフィック料金は日次決済となります。この場合、2020年11月3日にパブリックネットワークダウンストリームトラフィック料金が、2020年12月1日に低頻度ストレージ容量料金、低頻度ストレージ取得料金、低頻度ストレージリクエスト料金がそれぞれ決済され、従量課金方式の分析は次のようになります。

- 従量課金：
 - 低頻度ストレージ容量料金 = 0.018米ドル/GB/月 x 5GB = 0.09米ドル。
 - 低頻度ストレージデータ取得料金 = 0.002米ドル/GB x 5GB = 0.01米ドル。
 - 低頻度ストレージリクエスト料金 = 0.01米ドル/万回 x 1万回 = 0.01米ドル
 - パブリックネットワークダウンストリームトラフィック料金 = 0.1米ドル/GB x 5GB = 0.5米ドル

上記の分析を総合すると、11月中のBさんの料金総額は0.09 + 0.01 + 0.01 + 0.5 = 0.65米ドルとなります。