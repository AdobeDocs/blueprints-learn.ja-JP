---
title: 匿名Audience Activationのブループリント
description: Anonymous Audience Activation。
solution: Experience Platform, Audience Manager
kt: 7211
thumbnail: null
exl-id: f17599f1-2e75-4cbe-841a-9fd1dae71ada
translation-type: tm+mt
source-git-commit: 009a55715b832c3167e9a3413ccf89e0493227df
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 1%

---

# 匿名Audience Activationのブループリント

匿名の顧客データや行動チャネルデータに基づいて、Webや広告全体にわたるターゲットオーディエンスを行うことができます。 この機能により、複数のデバイスにわたって、パーソナライズされた一貫したリアルタイムの顧客体験を実現します。

## 使用例

* 匿名デジタルオーディエンスのターゲット設定とパーソナライゼーションを実行します。
* サポートされる広告ネットワークをターゲットにするオーディエンスを構築します。

## アプリ

* Adobe Audience Manager

## 建築

<img src="assets/aam.svg" alt="匿名Audience ActivationのBlueprintのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## 導入手順

<!-- These steps should link to help. -->

1. [Audience Managerの実装](https://experienceleague.corp.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=en#implementation-integration-guides)。
1. Audience Managerにデータを収集します。
1. セグメント定義で使用するシグナルと特性を設定します。
1. Audience Managerでセグメントを作成します。
1. オーディエンスを共有するAudience Managerで宛先を設定します。

## 関連ドキュメント

* [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html?lang=en)
* [Experience Cloudオーディエンス](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
* [Audience Managerとターゲットの統合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
* [Audience Managerを介したAnalyticsセグメントの共有](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
