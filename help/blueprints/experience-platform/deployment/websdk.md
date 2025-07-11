---
title: Web/Mobile SDK [!DNL Edge Network]  デプロイメントアーキテクチャの図
description: このブループリントは、Experience Platform Web および Mobile SDKを介したアーキテクチャと取り込みを示し  [!DNL Edge Network] す。
solution: Experience Platform,Data Collection
kt: null
thumbnail: null
exl-id: 3cc9e849-a75d-40ad-a604-6acf4c2c9f89
source-git-commit: adddd4105afc68379116d8d7208160689ee52c1d
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 68%

---


# Experience Platform Web SDKと [!DNL Edge Network] のアーキテクチャ図

Web、Mobile SDK、[!DNL Edge Network] Server API の概要と詳細については、次を参照してください。

* [Web SDK の概要](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/deployment/websdk)
* [Mobile SDK の概要](https://developer.adobe.com/client-sdks/documentation/)
* [[!DNL Edge Network]  サーバー API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)

Web SDK でサポートされるアプリケーション機能の詳細な概要については、次のドキュメントを参照してください。

* [Web SDK アプリケーション機能のサポート](https://github.com/orgs/adobe/projects/18/views/1)

アプリケーション固有の SDK から Web および Mobile SDK への移行に関する詳細は、次のドキュメントを参照してください。

* [ID サービス](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=ja)
* [Analytics](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/analytics-overview.html?lang=ja)
* [Target](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=ja)
* [Analytics for Target](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/a4t/overview.html?lang=ja)

## Experience Platform Web/Mobile SDKまたは [!DNL Edge Network] Server API のデプロイメント

次のアーキテクチャ図は、Experience Platform Web SDK を使用したデプロイメントパスとデータ収集を示しています。

<img src="assets/web_sdk_flow.svg" alt="Experience Platform Web および Mobile SDK を使用した実装の参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

Experience Edge、Experience Platform サービス、アプリケーションのシーケンス図

<img src="assets/web_sdk_sequence.svg" alt="オンライン／オフライン web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## リファレンスドキュメント

* [Web SDK を使用した Adobe Experience Cloud の実装チュートリアル](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ja)
* [モバイルアプリでの Adobe Experience Cloud の実装のチュートリアル](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=ja)
