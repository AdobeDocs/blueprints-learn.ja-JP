---
title: 匿名オーディエンスアクティベーションのブループリント
description: 匿名および行動顧客データに基づいて、web および広告チャネルをまたいでオーディエンスをターゲットする方法を説明します。この機能を使用すると、デバイスをまたいでパーソナライズされた一貫性のあるリアルタイムカスタマーエクスペリエンスを実現します。
landing-page-description: 匿名および行動顧客データに基づいて、web および広告チャネルをまたいでオーディエンスをターゲットする方法を説明します。
short-description: 匿名および行動顧客データに基づいて、web および広告チャネルをまたいでオーディエンスをターゲットする方法を説明します。
solution: Audience Manager
kt: 7211
thumbnail: null
exl-id: f17599f1-2e75-4cbe-841a-9fd1dae71ada
source-git-commit: 3a6a98eded28baee2cbb44de2262bbd580fa0c94
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 100%

---

# 匿名オーディエンスアクティベーションのブループリント

匿名オーディエンスのアクティベーションは、匿名デバイスおよび行動データに基づいて、web、モバイル、広告の各チャネルをまたいでオーディエンスをターゲティングしてパーソナライズする機能です。

## ユースケース

* Web サイト、モバイルアプリ、またはサポートされる広告チャネルで、匿名デジタルオーディエンスのターゲティングとパーソナライゼーションを実行します。
* 既知のデバイスや行動特性に基づいて、ランディングページと事前認証エクスペリエンスを最適化します。
* Audience Manager のサードパーティデータネットワークを活用して、ターゲティング用のオーディエンスをさらに絞り込み、拡張します。


## アプリケーション

* Audience Manager
* Real-time Customer Data Platform

Audience Manager と Real-time Customer Data Platform の両方を活用して、匿名オーディエンスアクティベーションをオンサイトと広告の宛先に使用できます。Real-time Customer Data Platform は、[宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=ja)に記載されている匿名デバイス識別子を持つ広告の宛先のサブセットのみをサポートしていることに留意してください。

Microsoft Bing、Google DV360、TradeDesk は、匿名デバイスベースのターゲティングでサポートされる、主な Real-time Customer Data Platform の広告の宛先です。この他にも、Real-time Customer Data Platform は多数の既知の顧客ベースの宛先をサポートします。それらは[宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=ja)に記載され、また[既知の顧客のアクティベーションブループリント](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=ja)で説明されています。

## アーキテクチャ

<img src="assets/anonymous_activation.svg" alt="匿名オーディエンスアクティベーションブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

<br>

## Audience Manager の実装手順

* Audience Manager の実装について詳しくは、次の[ドキュメント](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=ja)を参照してください.

## Real-time Customer Data Platform の実装手順

* Real-time Customer Data Platform の実装手順については、次の[ドキュメント](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=ja)を参照してください。

## 関連ドキュメント

* [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html?lang=ja)
* [Experience Cloud [!UICONTROL Audiences]](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=ja)
* [Audience Manager と Target の統合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html?lang=ja)
* [Audience Manager を使用した Adobe Analytics セグメント共有](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=ja)
* [既知の顧客のアクティベーションブループリント](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=ja)。
* [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=ja)
