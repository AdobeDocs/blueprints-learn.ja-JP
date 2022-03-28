---
title: 匿名オーディエンスアクティベーションブループリント
description: 匿名および行動顧客データに基づいて、web および広告チャネルをまたいでオーディエンスをターゲットする方法を説明します。この機能を使用すると、デバイスをまたいでパーソナライズされた一貫性のあるリアルタイムカスタマーエクスペリエンスを実現します。
landing-page-description: 匿名および行動顧客データに基づいて、web および広告チャネルをまたいでオーディエンスをターゲットする方法を説明します。
solution: Experience Platform, Audience Manager
kt: 7211
thumbnail: null
exl-id: f17599f1-2e75-4cbe-841a-9fd1dae71ada
source-git-commit: 4a46b7a4c278107c806d3ddd14591c7abe1a13d3
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 35%

---

# 匿名オーディエンスアクティベーションブループリント

匿名オーディエンスのアクティベーションは、匿名デバイスおよび行動データに基づいて、Web、モバイル、広告の各チャネルにわたってオーディエンスに対するターゲティングとパーソナライズをおこなう機能です。

## ユースケース

* Web サイト、モバイルアプリ、またはサポートされる広告チャネルで、匿名のデジタルオーディエンスのターゲティングとパーソナライゼーションを実行します。
* 既知のデバイスや行動特性に基づいて、ランディングページと事前認証エクスペリエンスを最適化します。
* Audience Managerのサードパーティデータネットワークを活用して、ターゲティング用のオーディエンスをさらに絞り込み、拡張します。


## アプリケーション

* Audience Manager
* Real-time Customer Data Platform

Audience ManagerとReal-time Customer Data Platformの両方を、AnonymousAudience Activationをオンサイトと広告の宛先に活用できます。 Real-time Customer Data Platformは、匿名デバイス識別子が ( [宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=en).

Microsoft Bing、Google DV360、TradeDesk は、匿名デバイスベースのターゲティングでサポートされる主なReal-time Customer Data Platform広告先です。 これら以外にも、Real-time Customer Data Platformは、 [宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=en) そして、 [既知の顧客アクティベーションブループリント](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).

## アーキテクチャ

<img src="assets/anonymous_activation.svg" alt="匿名オーディエンスアクティベーションブループリントの参照アーキテクチャ" style="width:80%; border:1px solid #4a4a4a" />

<br>

## 実装手順 Audience Manager

* Audience Managerの実装について詳しくは、次を参照してください [ドキュメント](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=ja).

## Real-time Customer Data Platformの実装手順

* Real-time Customer Data Platformの実装手順については、以下を参照してください [ドキュメント](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).

## 関連ドキュメント

* [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html?lang=ja)
* [Experience Cloud [!UICONTROL Audiences]](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=ja)
* [Audience Manager と Target の統合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html?lang=ja)
* [Audience Manager を使用した Adobe Analytics セグメント共有](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=ja)
* [既知の顧客アクティベーションブループリント](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html).
* [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html)
