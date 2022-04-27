---
title: Web／Mobile SDK データ収集ブループリント
description: このブループリントは、Experience Platform Web および Mobile SDK を使用したアーキテクチャと取り込みを示しています。
solution: Data Collection
kt: null
thumbnail: null
exl-id: 3cc9e849-a75d-40ad-a604-6acf4c2c9f89
source-git-commit: 3c134d6a4f8afb091631c14b05f34d6133a8865b
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 33%

---


# 概要

Web SDK、Mobile SDK、および Edge Network Server API の概要と詳細については、以下を参照してください。
* [WebSDK の概要](https://experienceleague.adobe.com/docs/web-sdk.html?lang=ja)
* [MobileSDK の概要](https://aep-sdks.gitbook.io/docs/)
* [Edge Network Server API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html)

WebSDK でサポートされるアプリケーション機能の詳細な概要については、次のドキュメントを参照してください。
* [WebSDK アプリケーション機能のサポート](https://github.com/orgs/adobe/projects/18/views/1)

アプリケーション固有の SDK から Web および Mobile SDK への移行に関する詳細は、次のドキュメントを参照してください。
* [ID サービス](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html)
* [Analytics](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/analytics-overview.html)
* [Target](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html)
* [Analytics for Target](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/a4t/overview.html)

## Experience PlatformWeb/Mobile SDK または Edge Network Server API のデプロイメント

次のアーキテクチャ図は、Experience PlatformWeb SDK を使用したデプロイメントとデータ収集を示しています。

<img src="assets/web_sdk_flow.svg" alt="Experience Platform Web および Mobile SDK を使用した実装の参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" />

Experience Edge、Experience Platformサービス、アプリケーションのシーケンス図

<img src="assets/web_sdk_sequence.svg" alt="オンライン／オフライン Web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" />

## リファレンスドキュメント

* [Web SDK を使用した Adobe Experience Cloud の実装チュートリアル](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ja)
* [モバイルアプリでの Adobe Experience Cloud の実装のチュートリアル](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=ja)