---
title: デバイスベース - Audience Managerによる匿名オーディエンスターゲティング
description: 匿名および行動顧客データに基づいて、web および広告チャネルをまたいでオーディエンスをターゲットする方法を説明します。 この機能を使用すると、デバイスをまたいでパーソナライズされた一貫性のあるリアルタイムカスタマーエクスペリエンスを実現します。
landing-page-description: 匿名および行動顧客データに基づいて、web および広告チャネルをまたいでオーディエンスをターゲットする方法を説明します。
short-description: 匿名および行動顧客データに基づいて、web および広告チャネルをまたいでオーディエンスをターゲットする方法を説明します。
solution: Audience Manager
kt: 7211
thumbnail: null
exl-id: f17599f1-2e75-4cbe-841a-9fd1dae71ada
TQID: https://experienceleague.adobe.com/weUxfDND0nBp0iQbCU5gYydUBcKn-Zk2unQ05Ett44k
product_v2:
  - id: df80eeb1-8d72-467e-b0df-9d51c7d3a0a1
feature_v2:
  - id: a8b0238e-1d43-4679-a3b4-5ba1bad83baa
  - id: baaa0dd2-d27e-4921-aae3-7888623a5fa5
  - id: c814092e-2730-45e8-a12d-e084529f52cb
subfeature_v2:
  - id: e8a4c7eb-7254-4984-ac46-e651a57c7e39
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 265
ht-degree: 86%

---

# デバイスベース - Audience Managerによる匿名オーディエンスターゲティング

>[!TIP]
>このブループリントは、Personalizationの[&#x200B; ユースケースパターン &#x200B;](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md)としても利用できます。

匿名オーディエンスのアクティベーションは、匿名デバイスおよび行動データに基づいて、web、モバイル、広告の各チャネルをまたいでオーディエンスをターゲティングしてパーソナライズする機能です。

## ユースケース

* Web サイト、モバイルアプリ、またはサポートされる広告チャネルで、匿名デジタルオーディエンスのターゲティングとパーソナライゼーションを実行します。
* 既知のデバイスや行動特性に基づいて、ランディングページと事前認証エクスペリエンスを最適化します。
* Audience Manager のサードパーティデータネットワークを活用して、ターゲティング用のオーディエンスをさらに絞り込み、拡張します。


## アプリケーション

* Audience Manager
* Real-time Customer Data Platform

Audience Manager と Real-time Customer Data Platform の両方を活用して、匿名オーディエンスアクティベーションをオンサイトと広告の宛先に使用できます。 Real-time Customer Data Platform は、[宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=ja)に記載されている匿名デバイス識別子を持つ広告の宛先のサブセットのみをサポートしていることに留意してください。

## アーキテクチャ

![匿名Audience Activation ブループリントの参照アーキテクチャ &#x200B;](assets/anonymous_activation.svg)

<br>

## Audience Manager の実装手順

* Audience Manager の実装について詳しくは、次の[ドキュメント](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=ja)を参照してください.