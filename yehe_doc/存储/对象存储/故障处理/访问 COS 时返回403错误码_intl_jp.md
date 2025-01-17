## 障害の現象

- COS API、SDKでリソースをアップロードおよびダウンロードする際、403エラーコードが返されます。
- 臨時アカウントまたはサブアカウントを使用してCOSリソースにアクセスする際、403エラーコードが返されます。
- COS bucketの設定を変更する際、403エラーコードが返されます。

## トラブルシューティング

### Messageが「Access Denied.」の場合

COSへのアクセスの際に次のメッセージが表示された場合、
```
<Code>AccessDenied</Code>
<Message>Access Denied.</Message>
```

次の操作を実行する必要があります。

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで【バケットリスト】を選択し、バケット管理ページに進みます。
3. 操作したいバケットを見つけ、そのバケット名をクリックし、バケット設定ページに進みます。
4. 左側ナビゲーションバーで【権限管理】>【バケットアクセス許可】を選択し、バケットアクセス権限管理ページに進みます。
5. 「バケットアクセス許可」バーで、COSにアクセスするアカウントにアクセス権限が設定されているかどうかをチェックします。
 - 「はい」の場合は、次の手順に進んでください。
 - 「いいえ」の場合は【ユーザーを追加】をクリックし、COSにアクセスするアカウントに必要な権限を設定してください。

6. アクセス権限を設定するアカウントに必要な権限があるかどうかをチェックします。
 - 「はい」の場合は、次の手順に進んでください。
 - 「いいえ」の場合は【編集】をクリックし、再設定してください。
7. 「Policy権限設定」バーで、COSにアクセスするアカウントにpolicy権限承認ポリシーが設定されているかどうかをチェックします。
>! 
> - バケットのアクセス権限がプライベート読み取り/書き込みであり、かつPolicy権限が匿名アクセスの場合、Policy権限の優先順位はバケットのアクセス権限より高くなります。
> - Policy権限承認ポリシーにおいて、同一のサブユーザーが許可と禁止のポリシーを同時に設定した場合、禁止ポリシーの優先順位は許可ポリシーより高くなります。
> - Policy権限承認ポリシーにおいて、「全ユーザー」ポリシーの優先順位は「指定ユーザー」ポリシーより低くなります。
> 
 - 「はい」の場合は、次の手順に進んでください。
 - 「いいえ」の場合は【ポリシーの追加】をクリックし、実際の署名アクセス時のアカウントに必要な権限を設定してください。

8. Policy権限を設定するアカウントに必要な権限があるかどうかをチェックします。
 - 「はい」の場合は、次の手順に進んでください。
 - 「いいえ」の場合は【編集】をクリックし、再設定してください。
9. COSリソースへのアクセス時に使用するq-akパラメータがターゲットバケットに所属するアカウントかどうかをチェックします（大文字と小文字を区別する）。
 - 「はい」の場合は、次の手順に進んでください。
 - 「いいえ」の場合は、q-akパラメータを対応するターゲットバケットに所属するアカウントに変更してください。
10. COSリソースにアクセスする際にクロスアカウントアクセスではないかをチェックします。
 - 「はい」の場合は、このアカウントにクロスアカウント権限の承認を行ってください。詳細な操作については、[クロスアカウントのサブアカウントに対し指定ファイルの読み取り/書き込み権限を承認する](https://intl.cloud.tencent.com/document/product/598/11092)をご参照ください。
 - 「いいえ」の場合は、[お問い合わせ](https://intl.cloud.tencent.com/support)ください。


### Messageが「AccessForbidden」の場合

COSへのアクセスの際に次のメッセージが表示された場合、
```
<Code>AccessDenied</Code>
<Message>AccessForbidden</Message>
```

次の操作を実行する必要があります。

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで【バケットリスト】を選択し、バケット管理ページに進みます。
3. 操作したいバケットを見つけ、そのバケット名をクリックし、バケット設定ページに進みます。
4. 左側ナビゲーションバーで【セキュリティ管理】>【クロスドメインアクセスCORS設定】を選択し、クロスドメインアクセスCORS設定ページに進みます。
5. 「クロスドメインアクセスCORS設定」バーで、クロスドメインリクエストかどうかをチェックします。

 - 「はい」の場合は、次の手順に進んでください。
 - 「いいえ」の場合はルールを変更してください。
6. 次のコマンドを実行し、クロスドメインリクエストの設定が正しいかどうかをチェックします。
```
curl 'http://bucket-appid.cos.ap-guangzhou.myqcloud.com/object' -voa /dev/null -H 'Origin: クロスドメインアクセスCORS設定のソースOrigin'
```
次のような情報が返されれば、正しく設定されています。
![](https://main.qcloudimg.com/raw/67513acee63f2f632b6cba58461fbe3d.png)

### Messageが「You are denied by bucket referer rule」の場合

COSへのアクセスの際に次のメッセージが表示された場合、
```
<Code>AccessDenied</Code>
<Message>You are denied by bucket referer rule</Message>
```

次の操作を実行する必要があります。

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで【バケットリスト】を選択し、バケット管理ページに進みます。
3. 操作したいバケットを見つけ、そのバケット名をクリックし、バケット設定ページに進みます。
4. 左側ナビゲーションバーで【セキュリティ管理】>【リンク不正アクセス防止の設定】を選択し、リンク不正アクセス防止設定ページに進みます。
5. 「リンク不正アクセス防止設定」で、リンク不正アクセス防止設定を設定しているかどうかをチェックします。

 - 「はい」の場合は、次の手順に進んでください。
 - 「いいえ」の場合は、[お問い合わせ](https://intl.cloud.tencent.com/support)ください。
6. 次のコマンドを実行し、リンク不正アクセス防止設定が正しいかどうかをチェックします。
```
curl 'http://bucket-appid.cos.ap-guangzhou.myqcloud.com/object' -voa /dev/null -H 'referer: Refererの値'
```
次のような情報が返されれば、正しく設定されています。
![](https://main.qcloudimg.com/raw/acc9862c6ffab6fd81c42136b775f2ea.png)


### Messageが「InvalidAccessKeyId」の場合

COSへのアクセスの際に次のメッセージが表示された場合、
```
<Code>AccessDenied</Code>
<Message>InvalidAccessKeyId</Message>
```

次の操作を実行する必要があります。

1. リクエスト署名の中のAuthorizationのq-akパラメータが正しく入力されているかどうかをチェックします。
 - 「はい」の場合は、次の手順に進んでください。
 - 「いいえ」の場合は、q-akパラメータを変更してください。キーのSecretIdはq-akパラメータと一致し、なおかつ大文字と小文字が区別されている必要があります。
2. [APIキー管理](https://console.cloud.tencent.com/cam/capi)に進み、APIキーが有効になっているかどうかをチェックします。

 - 「はい」の場合は、[お問い合わせ](https://intl.cloud.tencent.com/support)ください。
 - 「いいえ」の場合は、そのAPIキーを有効化してください。


### Messageが「InvalidObjectState」の場合

COSへのアクセスの際に次のメッセージが表示された場合、
```
<Code>AccessDenied</Code>
<Message>InvalidObjectState</Message>
```

次の操作を実行する必要があります。

リクエストされたオブジェクトがアーカイブタイプまたはディープアーカイブタイプかどうかをチェックします。
- 「はい」の場合はオブジェクトを復元し、再度アクセスしてください。詳細な操作については、[POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633)をご参照ください。
- 「いいえ」の場合は、[お問い合わせ](https://intl.cloud.tencent.com/support)ください。


### Messageが「RequestTimeTooSkewed」の場合

COSへのアクセスの際に次のメッセージが表示された場合、
```
<Code>AccessDenied</Code>
<Message>RequestTimeTooSkewed</Message>
```

次の操作を実行する必要があります。

1. OSのタイプに基づいて、クライアントの現在時刻を確認します。
 - Windowsシステム（Windwos Server 2012の場合）：![](https://main.qcloudimg.com/raw/ac22b052ee24273ebeab1139dd7f4d58.png) > 【コントロールパネル】>【時計、言語および地域】>【日付と時刻の設定】。

 - Linuxシステム：`date -R`コマンドを実行します。
![](https://main.qcloudimg.com/raw/88288162bd1de8c2ec0b640f0df6799e.png)
2. クライアントの現在時刻とサーバーの時刻にずれが存在するか（時刻のずれが15分を超えているか）を判断します。
 - 「はい」の場合は時刻を同期してください。
 - 「いいえ」の場合は、[お問い合わせ](https://intl.cloud.tencent.com/support)ください。


### Messageが「Request has expired」の場合

COSへのアクセスの際に次のメッセージが表示された場合、
```
<Code>AccessDenied</Code>
<Message>Request has expired</Message>
```

次の原因が考えられます。
- リクエストの送信時間が署名の有効期間を過ぎている。
- ローカルのシステム時刻が所在リージョンの時刻と一致していない。

署名の有効期間を再設定するか、またはローカルのシステム時刻を同期する必要があります。それでも解決しない場合は、[お問い合わせ](https://intl.cloud.tencent.com/support)ください。


### Messageが「SignatureDoesNotMatch」の場合

COSへのアクセスの際に次のメッセージが表示された場合、
```
<Code>AccessDenied</Code>
<Message>SignatureDoesNotMatch</Message>
```

次の操作を実行する必要があります。

クライアントが計算した署名とサーバーが計算した署名が一致しているかどうかをチェックします。
- 「はい」の場合は、[お問い合わせ](https://intl.cloud.tencent.com/support)ください。
- 「いいえ」の場合は、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)のドキュメントを参照するとともに、COS署名ツールを使用して、実現した署名プロセスをチェックしてください。

