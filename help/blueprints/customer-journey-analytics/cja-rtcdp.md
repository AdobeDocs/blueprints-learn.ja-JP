---
title: Real-time Customer Data Platform ブループリントとのCustomer Journey Analytics
description: Customer Journey Analytics のカスタマージャーニー全体からデータと顧客行動を統合および分析し、CJA から RTCDP にオーディエンスを公開します。
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
source-git-commit: 9fe44d93dcc05711c77ce1325b6549bb6c27a860
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 94%

---

# Real-time Customer Data Platform ブループリントとのCustomer Journey Analytics

Customer Journey Analytics（CJA）で識別されたオーディエンスを作成し、Adobe Experience Platform のリアルタイム顧客プロファイルに公開して、顧客のターゲティングとパーソナライゼーションを実現します。Customer Journey Analytics の詳細なフィルターおよび計算済みフィールドから、履歴データの使用や、より絞り込まれたオーディエンスを使用てのオーディエンスの作成に最適です。

## Customer Journey Analytics オーディエンス公開ガイド

Customer Journey Analytics から Real-time Customer Data Platform へのオーディエンスの公開に関する実装と設定ガイダンスについては、次のドキュメントを参照してください。[ドキュメント](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ja)

## Customer Journey Analytics ブループリントのアーキテクチャ

![アーキテクチャ図](assets/CJA.svg){zoomable="yes"}

## Customer Journey Analytics ブループリントのガードレール図

* ガードレールの詳細とエンドツーエンドの遅延については、[デプロイメントガードレールドキュメント](../experience-platform/deployment/guardrails.md)を参照してください

![ガードレール図](../experience-platform/deployment/assets/CJA_guardrails.svg){zoomable="yes"}

## よくある質問

* CJA が送信した RTCDP に対応するプロファイルが存在しない場合、新しいプロファイルが作成されますか、それとも既に存在するプロファイルの CJA からのみ視聴者が記録されますか。はい、新しいプロファイルが作成されます。その結果、RTCDP 実装が既知の顧客のみを対象としている場合、既知の ID を持つプロファイルのみをフィルタリングするように CJA オーディエンスルールを作成する必要があります。これにより、RTCDP プロファイルカウントが、望まれていない場合には、匿名プロファイルから増加しないことが保証されます。

* CJA はどの ID を送信しますか。CJA は、CJA の設定時に「ユーザー ID」として設定された ID を介して送信します。

* 何がプライマリ ID として設定されますか。CJA をプライマリ「人」ID として設定した際にユーザーが選択した ID です。

* ID サービスは CJA メッセージも処理しますか。すなわち、CJA は、オーディエンス共有を通じてプロファイル ID グラフに ID を追加することができますか。いいえ。ID サービスは CJA メッセージを処理しません。