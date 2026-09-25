---
title: リアルタイムのEdgeプロファイルアクセス
description: '[!UICONTROL  リアルタイムの顧客プロファイル ]がエッジでアクセスし、リアルタイムのwebおよびモバイルのパーソナライゼーションのコンテキストを提供します。'
solution: Real-Time Customer Data Platform, Data Collection
kt: 719
exl-id: 61b81d00-c4bd-41b2-8161-683814947b56
TQID: https://experienceleague.adobe.com/H59c3UBbNCQFs3H0VL5iVDKKZ5D3CFt4ri2RVwNlq7s
product_v2:
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
    internal-label: Real-Time Customer Data Platform
feature_v2:
  - id: ba929a52-9339-4154-9487-317dc875a3c7
    internal-label: Use cases
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
    internal-label: Behavioral data
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
    internal-label: Customer profiles
source-git-commit: 79738031788419872e32b8f754febacbfd18cc06
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 8%
---
# リアルタイムのEdgeプロファイルアクセス

>[!TIP]
>このアーキテクチャは、Personalizationの[ ユースケースパターン ](/help/blueprints/use-case-patterns/personalization/edge-profile-access.md)としても文書化されています。

この図は、web アプリケーションとモバイルアプリケーションがエッジで[!UICONTROL  リアルタイム顧客プロファイル ]のAdobe Experience Platformにアクセスし、高スループットで低遅延のパーソナライズを実現する方法を示しています。

アプリケーションは、ミリ秒単位の遅延で、エッジにあるリアルタイムのプロファイル属性およびオーディエンスにアクセスできます。 プロファイルに属性、オーディエンスメンバーシップ、モデル駆動機能を属性として保存し、webとモバイルのチャネル全体で同じページと次のページのパーソナライゼーションをリアルタイムで実行できます。

この機能を利用すれば、リアルタイムの行動から得られるオーディエンス、リアルタイムの顧客プロファイルに取り込まれた属性、計算されたインサイトなど、リアルタイムの顧客プロファイルにもとづいて、web サイトやモバイルアプリケーションで、高度にパーソナライズされた体験を提供できます。

>[!NOTE]
>
>Edgeのプロファイルアクセスは、webやモバイルのインバウンドパーソナライゼーション、リアルタイムのオファー決定など、スループットが高く低遅延のユースケース向けに設計されています。 エージェントによるサポートやセールスインタラクションなど、スループットが低いシナリオの場合は、Hub プロファイル参照APIの方が適切です。

## アプリケーション

* Real-time Customer Data Platform
* Adobe Experience Platform Data Collection （Web SDK / モバイルSDK）
* Edge Network Server API

## ユースケース

* webとモバイルのチャネルでリアルタイムにパーソナライズされ、既知の顧客体験を提供
* リアルタイムのプロファイル属性とオーディエンスにもとづく、同一ページと次のページのパーソナライゼーション
* リアルタイムの行動データ、属性、計算されたインサイトなど、顧客プロファイルにもとづくコンテンツとオファーのパーソナライゼーションを実現します
* パーソナライゼーションエンジン、コンテンツ管理システム、外部アプリケーションとの統合によるリアルタイムの意思決定
* リアルタイムのプロファイルコンテキストによるテストとコンテンツ最適化

## アーキテクチャ図

![ リアルタイム Edge プロファイル アクセスの参照アーキテクチャ ](assets/real_time_edge_profile_access.png){width="1000" zoomable="yes"}

## ガードレール

* [[!UICONTROL  リアルタイム顧客プロファイル ] データのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [Edge Network ガードレール](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* Edge プロファイルには、14日間の有効期間（TTL）があります。 ユーザーが14日間エッジでアクティブでなかった場合、エッジプロファイルは期限切れになり、ハブから取得する必要が生じる可能性があり、最初のページのパーソナライゼーションに影響を与える可能性があります。
* Edge personalizationは、エッジセグメント化の条件を満たすオーディエンスに対して、リアルタイムのオーディエンスメンバーシップの評価をサポートします。 ハブからのバッチオーディエンスとストリーミングオーディエンスも、適切な設定でエッジで利用できます。

## 関連ドキュメント

### 配信先設定

* [ カスタム Personalization Connection](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization) - プライマリ実装ガイド
* [Personalizationの宛先の概要](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/overview)
* [エッジのパーソナライゼーション宛先に対するオーディエンスのアクティブ化](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)
* [エッジ上のプロファイル属性をリアルタイムで検索し](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-profile-lookup)

### SDK ドキュメント

* [Experience Platform Web SDKのドキュメント](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html)
* [Experience Platform Mobile SDKのドキュメント](https://developer.adobe.com/client-sdks/home/)
* [Edge Network Server API ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)
* [Experience Platform Tags ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [Web SDKでのコマンド応答](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html)

### プロファイルとセグメント化に関するドキュメント

* [[!UICONTROL  リアルタイム顧客プロファイル ] ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html)
* [プロファイルガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)

### チュートリアル

* [Real-Time CDPとAdobe Targetによる次のヒットのパーソナライゼーション](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html)
* [データストリーム設定](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=ja)
