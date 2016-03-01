---
layout: post
title: OpsJAWS#4参加報告
---

### OpsJAWSとは

* AWS運用管理のノウハウを広く発信
* 次回4/20 LT中心

### OpsWorks概要

* AWS SA 船崎さん
* 構成管理、オペレーションタスクの自動化をいい感じにしてくれるやつ
* http://www.slideshare.net/AmazonWebServicesJapan/aws-black-belt-tech-2015-aws-opsworks

### AWS OpsWorks

* Amir Gordan (Senior Product Manager)
* OpsWorksのケーススタディなど

* OpsWorksが必要な理由
  * アプリケーションのモデリングやグルーピング
  * インスタンスのライフサイクルの管理
  * 権限の管理（インスタンスへのSSHやRDPの管理）
  * リソースのヘルスチェック
  * ログの分析
  * オペレーション上の問題を修正するプログラムの実行

* OpsWorksではインスタンスの構成にChefを利用

* グルーピング
  * フレキシブルにレイヤを定義することが可能

* ライフサイクルイベント
  * それぞれに紐付いているChefのCookbookがイベント発火時に起動する
  * setup
    * インスタンスが起動したとき
  * configure
    * インスタンスのステータスが変更されたとき
  * deploy
    * ソフトウェアのバージョンをデプロイする時

* 権限の管理
  * IAMユーザごとにSSHやRDP、rootの権限をStack上で細かく管理できる
  * RDPへ接続できる時間を決めることが可能

* ヘルスチェック
  * 14種類の監視が1分間隔で可能

* ログ
  * Chefの実行結果をログに出力することが可能
  * CloudWatch Logsにあげることも可能

* 使用例
  * リモートからbashを実行するDemo(サーバにSSHせずに)
  * rootになれるユーザを追加するDemo(サーバにSSHせずに)

* まとめ
  * ホストベースで管理することが可能
  * 権限管理が可能
  * 運用もChefのタスクを実行するだけなので楽
    * 時間での管理もできる


### CloudWatchEventハンズオン






