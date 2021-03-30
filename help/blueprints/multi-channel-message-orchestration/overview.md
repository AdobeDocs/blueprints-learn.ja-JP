---
title: 複数チャネルメッセージオーケストレーションのブループリント
description: 画面全体で個々のジャストインタイムの顧客エクスペリエンスを提供します。
solution: Experience Platform
kt: null
thumbnail: null
translation-type: tm+mt
source-git-commit: e1a9881996a181310bdc32cb083e4c5654139bf0
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# 複数チャネルメッセージオーケストレーションのブループリント

マルチチャネルメッセージオーケストレーションブループリントは、ブランドがEメール、SMS、モバイルアラートなどのチャネルを通じて、お客様と積極的に関わり合い、コミュニケーションを取る方法を示します。

オーケストレーションツールは、オーディエンス状態を他のチャネルの意思決定エンジンと共有することで、Webおよびモバイルパーソナライゼーションのために、他のインタラクションチャネル(受信チャネルなど)と統合できます。 様々な要因によって、顧客のインタラクションがトリガーベースかスケジュール済みか、ターゲット設定とパーソナライゼーションに必要なデータかなど、使用するアプリケーションとデプロイメントオプションを決定できます。 これらの要因により、メッセージオーケストレーション機能を構築する際に、様々なシナリオや展開オプションが発生する可能性があります。

## シナリオ


| シナリオ | 説明 | Experience Cloudアプリ |
|---|---|---|
| **バッチおよびトランザクションメッセージ** | <ul><li>スケジュール済みおよびバッチアウトバウンドキャンペーンの作成と実行</li><li>トランザクションメッセージの配信</li></ul> | <ul><li>Adobe Campaign ClassicとManaged Services</li><li>Adobe Campaign Standard</li></ul> |
| **[Batch Messaging &amp;Adobe Experience Platform](batch-messaging.md)** | <ul><li>Adobe Experience Platformを顧客のプロファイルとセグメント化の中心として、スケジュール済みおよびバッチメッセージングキャンペーンを実行</li></ul> | <ul><li>リアルタイム顧客データプラットフォーム</li><li>Adobe Campaign Classic、Managed Services、Campaign Standard</li><li>サポートされるサードパーティのメッセージングプロバイダー</li></ul> |
| **[トリガーされたメッセージングとAdobe Experience Platform](triggered-messaging.md)** | <ul><li>ストリーミングジャーニーのオーケストレーションとメッセージ配信のJourney Orchestrationを備え、ストリーミングデータ、顧客プロファイル、セグメント化の中心としてAdobe Experience Platformを使用して、トリガーおよびストリーミングメッセージングを実行します。</li></ul> | <ul><li>Adobe Experience Platform</li><li>Journey Orchestration</li><li>メッセージ配信用のAdobe Campaignまたは他のサードパーティアプリケーション</li></ul> |
