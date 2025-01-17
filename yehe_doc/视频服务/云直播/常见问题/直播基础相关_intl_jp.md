<span id="Que1"></span>
###  プッシュストリーム、ライブストリーミング、オンデマンドとはそれぞれ何ですか。
- **プッシュストリーム**：キャスターがローカルのビデオソースと音声ソースをTencentビデオストリーミングCVMにプッシュします。一部のシナリオでは、「RTMP公開」とも呼びます。
- **ライブストリーミング**：ライブストリーミングのビデオソースはリアルタイムに生成され、ライブストリーミングをプッシュする人がいることで有効となり、一度キャスターが配信を停止すれば、ライブストリーミングURLも無効となります。さらにリアルタイムなライブストリーミングのため、プレーヤーでビデオのライブストリーミングを再生するときに、プログレスバーの表示はありません。   
- **オンデマンド**：オンデマンドのビデオソースはクラウドのファイルで、ファイルがプロバイダに削除されない限り、随時再生することができます（Tencent Videoに類似）。さらに、すべてのビデオがサーバー上にあるため、再生時にプログレスバーの表示があります。

<span id="Que2"></span>
### CSS再生ドメイン名の要件は何ですか。	
コンソールでドメイン名の管理を送信する前に、ドメイン名をICP登録する必要があります。ドメイン名の桁数は45桁までで、現時点では大文字のドメイン名をサポートしていません。45桁を超えない小文字のドメイン名アドレスを入力してください。詳しくは[ドメイン名管理](https://intl.cloud.tencent.com/document/product/267/35970)をご参照ください。

<span id="Que3"></span>
### ライブストリーミングドメイン名のアクセス再生ドメイン名とプッシュドメイン名を同じにすることはできますか。セカンドレベルドメイン名を使用できますか。
アクセス再生ドメイン名とプッシュドメイン名は異なるドメイン名である必要がありますが、セカンドレベルドメイン名で区別できます。
例えば、`123.abc.com`をプッシュドメイン名に、`456.abc.com`を再生ドメイン名に使用します。

<span id="Que4"></span>

### どのプッシュプロトコルがサポートされていますか。
RTMPはライブストリーミング分野ではそれほど使用されませんが、「キャスター」から「サーバー」にデータをプッシュするサービスでは、RTMPは主流となっています。現在、ほとんどの中国国内のビデオクラウドサービスは、RTMPを主なプッシュプロトコルとして使用しています（モバイルライブストリーミングSDKの最初の機能モジュールはキャスタープッシュであるため、RTMP SDKとも呼ばれます）。

<span id="Que5"></span>

### どの再生プロトコルがサポートされていますか。
現在、一般的なライブストリーミングプロトコルには、RTMP、FLV、HLSがあります。
- **RTMP**：RTMPプロトコルはより充実しており、プッシュとライブストリーミングの両方に使用できます。そのコアコンセプトは、大きなビデオフレームとオーディオフレームを分割して、小さなデータパケットの形式でインターネット上で転送することです。また、RTMPは暗号化をサポートしているため、プライバシーがより確実に確保されますが、パケットの組み立てと分解が複雑なため、同時接続数が多い場合、予期しない安定性の問題が発生する可能性があります。 
- **FLV**：FLVプロトコルは主にAdobe社によって推奨されています。フォーマットは非常にシンプルで、タグヘッダー情報を大きなブロックのビデオフレームおよびオーディオビデオヘッダー部に追加するだけです。このシンプルさにより、遅延パフォーマンスと大規模な同時接続数において非常に優れています。スマホブラウザに対するサポートが非常に限られていることが唯一の欠点ですが、スマホAppのライブストリーミングプロトコルとしては、非常に適切です。  
- **HLS**：Apple社によって推進されたソリューションです。ビデオを5～10秒のビデオパートに小分けしてから、m3u8インデックステーブルで管理します。クライアントがダウンロードするビデオはすべて5～10秒の完全なデータなので、ビデオの再生が滑らかですが、大きな遅延も発生します（HLSの遅延は一般的に10～30秒程度です）。FLVに比べて 、HLSはiPhoneおよびほとんどのAndroidスマホブラウザでのサポートが非常に整っています
- **WebRTC**：名前は、Web Real-Time Communicationの略に由来し、ウェブページブラウザでのリアルタイムな音声対話またはビデオ対話をサポートするAPIです。2011年6月1日にオープンソース化され、Google、Mozilla、Operaのサポートのもと、W3C（World Wide Web Consortium)の推奨規格に取り込まれています。ライブイベントストリーミングで使用するのが、まさにこのWebRTCプロトコルであり、標準ライブストリーミングを超低遅延再生シナリオにおいて拡張したものとなります。従来型のライブストリーミングプロトコルと比較して遅延がより少なく、視聴者に、ミリ秒レベルの究極のライブストリーミング視聴体験を提供します。eラーニング、スポーツの試合のライブストリーミング、オンラインQAなど、遅延性能の要求がより高い特定のシナリオのニーズを満たすことが可能です。

| ライブストリーミングプロトコル  | 利点                   | 欠点                 | 再生遅延  |
| --------- | ---------------------- | -------------------- | --------- |
|FLV       | 成熟度が高く、高い同時接続数にストレスなく対応できる | 再生するにはSDKを統合する必要がある  | 2s～3s   |
| RTMP      | 遅延が比較的少ない               | 同時接続数が多い状況ではパフォーマンスが低下する | 1s～3s   |
| HLS(m3u8) | スマホブラウザのサポート度が高い     | 遅延が非常に大きい          | 10s～30s |
| WebRTC    | 遅延が最も少ない               | 再生するためにはSDKの統合が必要  | < 1s      |

[](id:Que6)
### 再生アドレスは何で構成されていますか。
次に例示するとおり、Tencent Cloud再生アドレスは、主に再生プレフィックス、再生ドメイン名（domain）、アプリケーション名（AppName）、ストリーム名（StreamName）、再生プロトコルサフィックス、認証パラメータ、およびその他のカスタムパラメータで構成されます。
```
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
https://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
https://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
-  **再生プレフィックス**
RTMP再生プロトコル：**rtmp://** 。
HTTP-FLV再生プロトコル：**http://**または**https://** 。
HLS再生プロトコル：**http://**または**https://** 。
WebRTC再生プロトコル：**webrtc://**。
- **アプリケーション名（AppName）**
アプリケーション名はCSSストリームメディアファイルを保存するパスを指します。デフォルトでは、CSSは**live**のパスを割り当てます。
- <span id="streamname">**ストリーム名（StreamName）**</span>
ストリーム名（StreamName）は各CSSストリームの一意の識別子を指します。
- **認証パラメータおよびその他のカスタムパラメータ**
認証パラメータ：**txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)**。


<span id="Que7"></span>
### 一般的なプッシュ方法は何ですか。
- **モバイル端末Android/iOSでカメラを使用**：サードパーティのソフトウェアまたは[モバイルライブストリーミングSDK](https://cloud.tencent.com/product/mlvb)を使用してカメラの映像をキャプチャし、ビデオストリームをCSSストリームのプッシュアドレスにプッシュします。
- **デスクトップまたはノートパソコンでカメラまたはスクリーンキャプチャを使用**：サードパーティのソフトウェアを使用してビデオまたはデスクトップの画像をキャプチャし、ビデオまたはデスクトップのコンテンツを、CSSストリームのプッシュアドレスにプッシュします。サードパーティのプッシュソフトウェアには[OBS（推奨）](https://intl.cloud.tencent.com/document/product/267/31569)、XSplit、FMLEなどがあります。
- **ビデオキャプチャデバイス**：HDカメラにHDMIまたはSDI出力ポートを備えている場合、エンコーダに接続してRTMPプッシュの方法でライブストリーミングのコンテンツをライブストリーミングサービスにプッシュできます。CSSプッシュアドレスをエンコーダのRTMP公開アドレスとして設定する必要があります。
Webカメラタイプのデバイスの場合、RTMPプッシュをサポートしていれば、CSSプッシュアドレスをカメラのRTMP公開アドレスとして設定できます。
- **ビデオファイルをビデオストリームに変換**：ビデオファイルを読み取り、RTMPストリーム出力をビデオソースとして使用して、ライブストリーミングサービスのRTMPプッシュアドレスにプッシュしてビデオを公開します。`ffmpeg`コマンドを使用して実装できます（Windows、LinuxおよびMacのいずれにも対応）。

<span id="Que8"></span>
### ストリームの中断とストリームの禁止の違いは何ですか。
-  **ストリームの中断機能**：ライブストリーミングのストリームの1つで、ストリームが中断された場合、今回のプッシュも中断され、視聴者はライブストリーミングを見ることができなくなります。ストリームが中断されると、キャスターはプッシュを再開してライブストリーミング活動を再開できます。
-  **ストリームの禁止機能**：ライブストリーミングのストリームの1つで、ストリームが禁止された場合、今回のプッシュストリームも中断され、視聴者はライブストリーミングを見ることができなくなります。ストリームが中断されると、キャスターは禁止期間中にはプッシュを再開できません。ストリームの禁止機能はCSSコンソールのストリーム管理ページで設定できます。禁止されたCSSストリームは禁止されたストリームリストページに表示され、【有効】をクリックすると再開できます。
[](id:Que10)
### ライブストリーミングは文字チャット機能をサポートしていますか。
文字チャット機能はInstant Messaging製品が提供するサービスで、IMはこれ以外に弾幕コメント、いいねギフト、商品プッシュ、カルーセル広告などのインタラクションもサポートしています。ルーム管理機能によりキャスターのマイク接続PKや、視聴者に対するミュート権限の管理、ユーザーの身分識別などの機能を実現します。
[](id:Que11)
### ライブストリーミング使用申請の終了後、アカウントを変更して再申請することはできますか。 
それぞれのTencent Cloudアカウントの実名認証が完了した後、いずれもCSSサービスをアクティブ化することができます。 
[](id:Que13)
### 企業ユーザー以外の商用ライブストリーミングにはネットワーク文化経営許可証が必要ですか。
ライブストリーミングサービスの試用には許可証は必要ありませんが、ライブストリーミングコンテンツが商用の用途（たとえばApp、ウェブサイト）として使用する場合、事前に関連部門に確認した上で、関連するライブストリーミング要件を準備する必要があります（例：ネットワーク文化経営許可証、付加価値電信業務経営許可証など）。
[](id:Que15)
### CSSはそのまま使用できるソフトウェアですか。
 いいえ。CSSはインターフェースによる二次開発が必要な製品です。 

[](id:Que16)
### ライブストリーミング視聴人数を確認するには、どうすればいいですか。
CSS API 3.0の[ストリームの再生情報リストコネクタのクエリー](https://intl.cloud.tencent.com/document/product/267/37297) を呼び出して、オンライン視聴人数を確認することをおすすめします。
