---
title: 匿名オーディエンスアクティベーションブループリント
description: 匿名オーディエンスアクティベーション。
solution: Experience Platform, Audience Manager
kt: 7211
thumbnail: null
exl-id: f17599f1-2e75-4cbe-841a-9fd1dae71ada
source-git-commit: 53914ce36ef0e48734c04818fbf8a5285fbb14ab
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 100%

---

# 匿名オーディエンスアクティベーションブループリント

匿名および行動顧客データに基づいて、Web および広告チャネルをまたいでオーディエンスをターゲットできます。この機能を使用すると、デバイスをまたいでパーソナライズされた一貫性のあるリアルタイムカスタマーエクスペリエンスを実現します。

## ユースケース

* 匿名デジタルオーディエンスのターゲティングおよびパーソナライズ機能を実行します。
* サポートされている広告ネットワークでのターゲティング用にオーディエンスを作成します。

## アプリケーション

* Adobe Audience Manager

## アーキテクチャ

<img src="assets/anonymous_activation.svg" alt="匿名オーディエンスアクティベーションブループリントの参照アーキテクチャ" style="border:1px solid #4a4a4a" />

## 実装手順

<!-- These steps should link to help. -->

1. [Audience Manager を実装します](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=ja#implementation-integration-guides)。
1. Audience Manager にデータを収集します。
1. セグメント定義に使用するシグナルおよび特性を設定します。
1. Audience Manager でセグメントを作成します。
1. Audience Manager で宛先を設定して、オーディエンスを共有します。

## 関連ドキュメント

* [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html?lang=ja)
* [Experience Cloud [!UICONTROL Audiences]](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=ja)
* [Audience Manager と Target の統合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html?lang=ja)
* [Audience Manager を使用した Adobe Analytics セグメント共有](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=ja)
