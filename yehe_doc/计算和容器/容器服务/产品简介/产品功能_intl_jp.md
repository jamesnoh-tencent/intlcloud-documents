## クラスター管理
TKEを使用すると、シンプルで効率的なコンテナクラスターの管理が可能です。プロセス全体が安全で信頼性が高く、Tencent Cloudのコンピューティング、ストレージ、ネットワークにシームレスに接続することができます。

|モジュール|機能要点|
|---|------|
|クラスター構成|<li>CVMすべてのモデルをサポートし、CVMの新規作成および既存のCVMの追加が可能です</b><br> <li>クラスター内CVMはアベイラビリティーゾーン間のデプロイ</b><br> <li>従量課金をサポートします</b><br><li>ユーザー排他クラスター、VPCセキュリティ隔離</b><br><li>カスタムクラスターネットワークをサポートし、コンテナネットワークの柔軟な構成が可能です|
|クラスター管理|<li>クラスターの動的なスケーリングをサポートし、ノードの昇降には</b><br> <li>豊富な監視指標があり、カスタマイズされたアラームポリシーをサポートします</b><br>|
|Kubernetes管理|<li>kubernetes複数バージョンをサポートし、バージョンアップ機能、</b><br><li>Kubernetes証明書管理をサポートし、kubectlで直接クラスターを操作できます</b><br> <li>コンソールで簡単にNamespaceを管理できます|

## アプリケーション管理
TKEが提供するアプリケーション管理機能により、複数のサービスをワンクリックで迅速に作成し、さまざまな環境のアプリケーションをデプロイすることができます。

|モジュール|機能要点|
|---|------|
|アプリケーション構成|<li>TKEの複数のサービスタイプをサポートします</b><br> <li>Kubernetes Deployment、DaemonSetなどの複数のリソースをサポートします|
|アプリケーション管理|<li>アプリケーションはマイテンプレート、テンプレートマーケティングの迅速な作成をサポートします</b><br> <li>更新アプリケーションのリアルタイム比較表示をサポートします。</b><br> <li>アプリケーション内のサービスをワンクリックでデプロイ/停止できます|
|テンプレート管理|<li>私のテンプレートのサポート、テンプレートマーケティングをサポートします。</b><br> <li>テンプレートはワンタッチでコピーできます|

## サービス管理
サービス管理は、効率的なコンテナ管理ソリューションを提供し、サービスの迅速な作成、迅速な拡張・圧縮、CLB、サービス検出、サービス監視、ヘルスチェックなどの特徴をサポートします。サービス管理によりユーザーのコンテナを簡単で速やかに管理できます。

|モジュール|機能要点|
|---|------|
|サービスのデプロイ|<li>単一インスタンス・マルチコンテナのサービスデプロイをサポートします。</b><br> <li>複数のサービスアクセス方法をサポートします</b><br> <li>サービス内インスタンスのアベイラビリティーゾーン間のデプロイをサポートします</b><br> <li>アフィニティおよびアンチアフィニティのスケジュール設定をサポートします|
|サービス管理|<li>サービスのローリング更新と迅速な更新をサポートします</b><br> <li>サービスの動的な容量拡張圧縮をサポートします</b><br> <li>サービコンテナのリモートログインをサポートします|
|サービス運用維持|<li>サービス詳細な監視メトリックの表示をサポートします</b><br> <li>サービスコンテナのstdoutとstderrログの表示をサポートします</b><br> <li>サービスアラームポリシーの設定をサポートします</b><br> <li>生存チェックと準備完了チェックの二つのヘルスチェック方法の設定をサポートします</b><br> <li>コンテナ異常の自動回復|

## 設定項目の管理
設定項目は、いくつかのプログラムが起動時にどのような設定を読み込むために使用されます。プログラムの設定を変更する方法を提供しており、オブジェクトによって異なる設定項目を使用することができます。

|モジュール|機能要点|
|---|------|
|設定項目の管理|<li>設定項目の複数バージョンがサポートされます</b><br> <li>ビジュアルとYAMLの二つの編集形式がサポートされます|
|設定項目の使用|<li>設定項目はデータボリュームとしてコンテナディレクトリにマウントされます</b><br> <li>設定項目は環境変数としてインポートされます</b><br> <li>設定項目はアプリケーションテンプレート変数に入れ替えます|

## イメージ管理
Tencent Cloud Mirror WarehouseにはDockerhubの公式イメージとユーザーのプライベートイメージが含まれます。イメージ管理によって迅速なイメージの新規作成とサービスの迅速なデプロイが可能になります。

|モジュール|機能要点|
|---|------|
|イメージ管理|<li>プライベートイメージリポジトリの新規作成をサポートします</b><br> <li>DockerHubイメージリポジトリの表示と使用をサポートします</b><br> <li>TencentHubイメージリポジトリの表示と使用をサポートします</b><br> <li>複数のイメージネームスペースの管理をサポートします|
|イメージ使用|<li>イメージ新規作成サービス用の高速イントラネットチャネルを提供します</b><br><li>パブリックネットワークイメージのアップロードとダウンロードをサポートします|
|CI/CD|<li>プライベートイメージの自動構築設定をサポートします</b><br> <li>イメージのトリガ設定をサポートします</b><br>|
