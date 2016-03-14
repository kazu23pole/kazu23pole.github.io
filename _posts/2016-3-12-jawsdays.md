---
layout: post
title: JAWS DAYS 2016参加報告
--

#### AWS-UGのこれまでとこれから
##### 金春さん@アールスリーインスティテュート

[資料](http://www.slideshare.net/tkonparu/20160312-jaws-days-2016-keynote)


#### Cognitoでお手軽ソーシング
##### 足立さん@来栖川電算

[資料](http://www.slideshare.net/youheiyamaguchi/jawsdays2016-technical-deep-dive)

##### 業務

* 教師モデルを利用している
  * そのためにデータ入力が必要
  * データ入力はリモートワーク
  * 開発はデータ入力に専念したい：ユーザ管理とかはしたくない

##### Cognito

* Cognito Identity
  * アプリ用のユーザIDプール
* Cognito Sync
  * データのオフライン編集
  * ユーザのデータ同期

* Cognito Identity
  * ユーザ認証機能を外部化したユーザID管理サービス
    * 認証済ユーザID(ひも付け)：外部IDに対応するIDを発行
    * 未認証ユーザID(ゲスト)：認証していなくてもIDを発行
    * ユーザIDのマージ(名寄せ)：ゲストユーザとかと本IDをマージ
    * AWS資源のユーザ領域への安全なアクセス
  * フロー：シーケンス図Check
    * 4パターン
      * IDプロバイダ：一般的なID(GoogleAccountとか)や独自ID(自社のID)
      * ロール：静的(あらかじめ設定したロール)、動的(ユーザや状況ごとに変化)
    * Enhanced Flow(一般的ID×静的ロール)
    * Basic Flow(一般的ID×動的ロール)
    * 独自Enhanced Flow(独自ID×静的ロール)
    * 独自Basic Flow(独自ID×動的ロール)


#### Cognito Deep Dive
##### 塚田さん@AWS SA

[資料](http://www.slideshare.net/akitsukada/amazon-cognito-deep-dive-jaws-days-2016)

##### 2-Tier Architecture

* AWSへのリソースをMobile SDKから直接叩く
* サーバなどのインフラメンテナンスをより少なくする

##### Cognito Identity

* STSとの関係
  * STSはAWSリソースへのアクセスを制御している
  * Cognitoはいい具合にラップしている

* Cognito Sync
  * アプリのデータ、設定などをいい感じに保存してくれる
  * オフラインをサポート


#### スマートニュースにおけるストリーム処理の過去・現在・未来
##### 坂本さん@スマートニュース

[資料]()


#### Big DataとContainerとStreaming – AWSでのクラスタ構成とストリーミング処理
##### 岩永さん@AWS SA

[資料]()

* イベントプロセス
* マイクロバッチプロセス
  * Spark streaming

##### 例

* Sliding window
  * 1分ごとに1分間の処理を見るのではなく、10秒ごとに前1分の処理を見て処理する
* 重要なポイント
  * 入と出を分離する
  * ダータを途中途中で保存する
  	→Kinesis
  * コスト見合いを考慮

##### Kinesis

* Kinesis Streams
  * 自身でストリーミングアプリケーションを実装できる
  * ストリーム処理の入と出はAPI
  	* HTTPとかSDKとか
  	* 出はSparkとかEMRとかも可能
  * シャードという単位で処理をおこなう
  	* Hadoopのノードみたいな？
  	* パーティションキーごとにシャードを分ける
  * 保持期間は24時間〜7日間

* Kinesis Firehose
  * ストリームのデータをストレージに保存するまでをmanageしてくれる
    * サーバレスに処理&保存ができる
  * Fluent plugin for Kinesisを作成中
  	* GitHubで提供中

* Kinesis Analytics
  * データストリームを標準的なSQLで継続的に分析する
  * 開発中

##### Container

* OSレベルの仮想化
  * プロセスで起動するisolateな環境
* どこに持って行っても同じ環境
* メジャーなコンテナ
  * Docker, JVM, Lambda(一種のContainer)
* BigData
  * スケーラビリティ
    * Containerはどこに持って行っても同じ
  * コスト
    * アプリの使用量とかを制御できるので、コスト効率が高い
  * スピード
    * OSの変更時などにコンテナを使っていればコンテナが動けば変更は不要


#### IoTプラットフォーム”SORACOM”最新動向
##### 玉川さん@SORACOM

[資料](http://www.slideshare.net/SORACOM/jaws-days-iotsoracom)




#### オペ担当がAPI Gateway + Lambdaでチケット処理を自動化した話。
##### 植木さん@AWS-UG

[資料](http://www.slideshare.net/kazukiueki76/20160312jaws-days-2016-api-gatewaylambda)

##### 学習法

* BluePrintで色々やってみる
  * コードを読む
* Qiita, Developers.io


#### Amazon API Gateaway / AWS Lambda Deep Dive（の触りだけ）
##### 西谷さん@AWS SA

[資料](http://www.slideshare.net/keisuke69/aws-lambda-amazon-api-gateway-deep-dive)

##### Lambdaの利用パターン

* Data processing
  * ほとんどがこのパターン
  * リアルタイムファイル処理
  * s3+Lambda, DynamoDB+Lambda, Kinesis+Lambda
  * ログルーティングとかフィルタリング
* バックエンド
  * APIバックエンド、IoTバックエンド
* Worker
  * アラームとか

##### Tips

* Lambdaのブラウザエディタはカラースキームが変更可能
* コンテナの再利用
  * Lambda Functionはコンテナ単位で管理されてる
  * 初回時にコンテナを作成して、初期化処理
  * 終了後、ある程度時間が経過すると破棄される
    * 破棄されたら再実行しても初期化される
    * 短期間であれば、破棄されないのでソースの読み込みなどが省略される
  * 初期化コストはJava>Node.js、コードコストはJava<Node.js
    * Pythonが安定してるかも
  * メモリサイズしか指定できない
    * CPUもメモリサイズに比例して大きくなる
  * 設定したタイミングからインターネットアクセスができなくなる
    * 必要な場合はNATインスタンスを用意
  * ENIとサブネットIPが無い場合はリクエストが失敗する
    * この場合エラーがCloudWatchLogsに出ない
    * AZごとにサブネットを指定する
    * 必要なロールを割り当てる
  * cronはUTC
  * 冪等性はコード上で保証する必要がある
    * 最低1回実行することは保証している
      * 2回実行されるかもしれないのでコード上で冪等性を担保する
  * Lambdaのリトライはイベントソースによって異なる
  * 同時実行数の考え方
    * イベントソースがKinesisの場合はシャード数と等しくなるので、シャード数以上に同時実行数が増えることはない
    * DynamoDBはパーティション数
    * 1秒あたりのリクエスト数*関数の実行時間　最大の同時実行数を確認する
    * 同時実行数を超えた場合
      * ファンクションによって異なる
        * 同期の場合は429エラーが返る
        * 非同期の場合
          * スロットルされたイベントは最大6時間まで試行
  * Lambdaに環境変数
    * そういった機能はないが、エイリアスを使うとできるかも
  * ソースの新規アップロード
    * ダウンタイムはない
  * IP
    * プライベートIPは固定できない
    * インターネットに出るときはNAT
  * ENIは複数のLambdaFunctionから共用される


##### API Gateway

* WAFはCloudFrontを使うしかない
* ACMはCloudFrontを使うしかない
* API Gateway はCloudFront・・・
