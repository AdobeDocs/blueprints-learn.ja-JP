---
title: 顧客アクティビティハブブループリント
description: '[!UICONTROL リアルタイム顧客プロファイルを検索し、担当者がサポートおよび販売を支援する際のコンテキストを提供します。]'
solution: Experience Platform,Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c,4f15aa5d-9ee3-4d92-8012-3e2f0c0d615f
translation-type: tm+mt
source-git-commit: d6eaf978a8f587b881480c14f192cb9e29e3c7e2
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 73%

---

# 顧客アクティビティハブブループリント

顧客アクティビティハブブループリントは、外部アプリケーションが Adobe Experience Platform の[!UICONTROL リアルタイム顧客プロファイル]にアクセスする方法を示します。

外部アプリケーションは、APIGETリクエストを使用してプロファイルにアクセスできます。 これにより、プロファイルに格納された属性、イベント、セグメントメンバーシップおよびモデル主導の機能を、外部のアドビ以外のアプリケーションで使用できます。

この機能によって、顧客がコールセンターに問い合わせる際にリッチコンテキストを表示できます。サポート担当者は、例えば、顧客のライフタイムバリュー、チャーン傾向またはマーケティングキャンペーンのエクスポージャーなどを表示できます。また、販売担当者は、より多くのコンテキストや顧客へのインサイトというメリットを得られます。

>[!NOTE]
>
>Profile Lookup API でサポートされている現在の待ち時間は約 500 ミリ秒なので、このアプローチは、リアルタイムディシジョンエンジン（同じページの web やモバイルのパーソナライズ機能など）とプロファイルの統合には適していません。

## ユースケース

* 担当者がサポートするインタラクションに、詳細な消費者コンテキスト（サポートおよび販売エクスペリエンスなど）を提供する。Experience Platform のプロファイルルックアップを使用して、担当者は、最近の購入、キャンペーンインタラクション、傾向、オーディエンスメンバーシップ、リアルタイム顧客プロファイルに格納されたその他の属性およびインサイトなど、消費者に対するより詳細なコンテキストを受け取ることができる。

## 構造

<img src="assets/customer_activity_hub.svg" alt="顧客アクティビティハブブループリントの参照アーキテクチャ" style="border:1px solid #4a4a4a" />


## ガードレール

* [リアルタイム顧客プロファイルデータのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)

## 実装手順

1. [取り込むデータの](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) スキーマを作成します。
1. [取り込むデータの](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) データセットを作成します。
1. [取り込まれたデータが統合プロファイルに確実にステッチできるようにするために、スキーマに正しい ID および ID 名前空間を設定します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html)
1. [プロファイルのスキーマとデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html)。
1. [データを Experience Platform に取り込みます。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion)
1. [マージポリシーを設定します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html)。
1. [エンティティAPIを使用して、レコードエンティティまたはエクスペリエンスイベントエンティティからプロファイル属性](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html)を検索します。

## 関連ドキュメント

* [Adobe Experience Platform Activation 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-platform0.html)
* [リアルタイム顧客プロファイルドキュメント](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=ja)
* [プロファイルのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [Profile Lookup API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
