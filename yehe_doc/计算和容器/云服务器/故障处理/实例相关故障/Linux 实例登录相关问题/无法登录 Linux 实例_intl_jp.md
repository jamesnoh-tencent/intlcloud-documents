このドキュメントでは主にLinuxインスタンスが接続できない場合のトラブルシューティング方法と、Linuxインスタンスに接続できない主な原因について解説し、問題のトラブルシューティング、特定および解決について説明します。


## 問題の特定
### 自己診断ツールの使用
Tencent Cloudは、帯域幅、ファイアウォールおよびセキュリティグループの設定などの一般的な問題が原因であるかどうかを判断するのに役立つ自己診断ツールを提供しています。 障害の70％はツールで特定でき、検出された問題をもとにログインできない原因となっている可能性のある障害を特定できます。
1. [セルフチェック](https://console.intl.cloud.tencent.com/workorder/check)をクリックし 、自己診断ツールを開きます。
2. 下図のように、ツールインターフェースのプロンプトに基づき、診断したいCVMを選択し、**検出開始**をクリックします。
   ![](https://qcloudimg.tencent-cloud.cn/raw/1956fb3b3a0f0d93da0edf1fed51f2f7.png)


## 考えられる原因
Linuxインスタンスにログインできない主な原因：
- [SSHの問題によりログインできない](#UseSSHLogin)
- [パスワードの問題によりログインできない](#CryptographicProblem)
- [帯域幅利用率が高すぎる](#BandwidthUtilization)
- [サーバーの過負荷](#HighServerLoad)
- [セキュリティグループルールの設定不備](#SafetyGroupRule)

## トラブルシューティング
### VNC 方式を介したログイン[](id:VNC)

標準の方法（Webshel​​l）またはリモートログインソフトウェアを使用してLinuxインスタンスにログインできない場合は、Tencent Cloud VNCを介してログインし、障害の原因を特定できます。
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. 下図のように、インスタンスの管理画面で、ログインしたいインスタンスを選択し、**ログイン**をクリックします。
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. ポップアップした「標準ログイン | Linuxインスタンス」ウィンドウで、**VNCログイン**を選択します。
<dx-alert infotype="explain" title="">
 ログイン中に、パスワードを忘れた場合は、コンソールでこのインスタンスのパスワードをリセットできます。具体的な操作については、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)をご参照ください。
</dx-alert>
4. ユーザー名とパスワードを入力してログインし、ログインを完了します。


### SSH問題によりログインできない[](id:UseSSHLogin)
**障害事象**：[SSHを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32501) した場合に、「接続できません」または「接続に失敗しました」と表示される。
**処理手順**：[SSH方式を介してLinuxインスタンスにログインできない](https://intl.cloud.tencent.com/document/product/213/32486)を参照してトラブルシューティングを行います。

<span id="CryptographicProblem"></span>
### パスワードの問題によりログインできない
**障害の現象**：パスワードの入力間違い、パスワード忘れまたはパスワードのリセット失敗によるログインが失敗しました。
**対処方法**： [Tencent Cloudコンソール](https://console.cloud.tencent.com/cvm/index) で当該インスタンスのパスワードをリセットした後、インスタンスを再起動します。
**対処手順**：インスタンスのパスワードのリセット方法は、[インスタンスのパスワードのリセット](https://intl.intl.cloud.tencent.com/document/product/213/16566)をご参照ください。


### 帯域幅利用率が高すぎる[](id:BandwidthUtilization)
**障害の現象**：セルフ診断ツールにより診断された問題は帯域幅利用率が高すぎることです。
**対処手順**：
1.  [VNC ログイン](#VNC)の方法でインスタンスにログインします。
2. [高い帯域幅利用率によりログインできない](https://intl.cloud.tencent.com/document/product/213/32542)を参考にし、インスタンスの帯域幅使用状況及び障害対処を確認します。


### サーバー負荷が高い[](id:HighServerLoad)
**障害の現象**：セルフ診断ツール又はクラウド監視により、サーバーのCPU負荷が高いためシステムがリモート接続をできないか、或いはアクセスできないことが判明しました。
**考えられる原因**：ウィルスやトロイの木馬、サードパーティーのアンチウィルスソフト、アプリケーションの異常、ドライバーの異常またはバックグラウンドでのソフトウェア自動更新により、CPU利用率が高くなり、CVMにログインできなかったり、アクセス速度が遅くなったりすることが発生しました。
**対処手順**：
1.  [VNC ログイン](#VNC)の方法でインスタンスにログインします。
2. [Linuxインスタンス：CPUとメモリ占用率が高いため、ログインできない](https://intl.cloud.tencent.com/document/product/213/32387)を参照し、「タスクマネージャー」で負荷の高いプロセスを特定します。


### セキュリティグループルールが不適切[](id:SafetyGroupRule)
**障害の現象**：セルフ診断ツールで検査した結果、セキュリティグループの規則設定の不具合によりログインできなくなったことが判明しました。
**対処手順**： [セキュリティグループ（ポート）検証ツール](https://console.cloud.tencent.com/vpc/helper) で確認します。
![](https://main.qcloudimg.com/raw/278c7f0abd9b7224d32fa5402554544a.png)
セキュリティグループポート設定の問題であると判断された場合は、ツールの**ワンクリック開放**機能を使用してポートを開放できます。
![](https://main.qcloudimg.com/raw/e4a40dafcc9607ce18ee7001129d9655.png)
セキュリティグループルールをカスタマイズしたい場合は、 [セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)を参照して、セキュリティグループのルールを再設定してください。



## その他ソリューション
上述のトラブルシューティングを行っても、Linuxインスタンスに接続できない場合は、セルフチェック結果を保存し、[チケットを提出]（https://console.intl.cloud.tencent.com/workorder/category
) し、フィードバックしてください。
