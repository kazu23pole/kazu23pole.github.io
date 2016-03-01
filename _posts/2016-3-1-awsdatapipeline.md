---
layout: post
title: AWSDataPipelineを調べてみた
---

### そういえばData Pipelineってあったよな・・・

AWS使っててとりあえず見たことあったけど使ったことなかったので、調べてみました。

### AWS Data Pipeline

AWS Data Pipelineは、AWSやオンプレでのリソース間データ処理/移動を簡単に設計できる、フルマネージドサービス。

cron処理を特定のEC2インスタンスにやらせずに、DataPipelineにやらせてcron処理の実行を保証することができる。
DataPipelineを使うことで、万が一EC2インスタンスが止まった時にcron処理が行われなくなるのを防ぐことができます。
