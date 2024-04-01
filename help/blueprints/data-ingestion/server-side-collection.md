---
title: イベント転送ブループリント
description: Experience Platform SDK で収集したデータを宛先にストリーミング
solution: Data Collection
kt: 7202
exl-id: 8d6f0705-628b-44e4-a3fc-da6c5e308a5b
source-git-commit: 60a7785ea0ec4ee83fd9a1e843f0b84fc4cb1150
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 77%

---

# イベント転送ブループリント

イベント転送ブループリントは、Adobe Experience Platform Web および Mobile SDK で収集されたデータをExperience Platform[!DNL [!DNL Edge Network]] を目的の宛先に追加します。 SDK から収集された生のデータをすべて転送することも、タグプロパティ（旧称 Launch）で設定されたイベントおよびルールに基づいて特定のデータを転送することもできます。

## ユースケース

* 単一の収集タグを使用して Web またはモバイルからデータを収集し、クライアントブラウザーおよびアプリのコードを軽量化します。データ収集の単一のソースとするため、収集したデータを様々なエンドポイントに伝達します。
* 収集されたデータをパートナーアプリケーションやデータ保存場所に転送して、収集されたデータに対するインサイトおよびアプリケーションを構築します。

## アプリケーション

* Adobe Experience Platform のデータ収集

## アーキテクチャ

<img src="assets/enterprise_collection.svg" alt="エンタープライズデータ収集の参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## 関連ドキュメント

* [イベント転送のドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ja)
* [イベント転送のビデオ](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html?lang=ja)
* Web SDK チュートリアルの[イベント転送のレッスン](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=ja)

## 関連するブログ投稿

* [Adobe Experience Platform Web SDK を使用した Web サイトのパフォーマンスの向上および [!DNL Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [Adobe Experience Platform Web SDK を使用した実装上の問題点の解決および [!DNL Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [Audience Management 用 Adobe Experience Platform Web SDK](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [Adobe Experience Platform Web SDK - Adobe Target](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [Adobe Analytics 用 Adobe Experience Platform Web SDK 移行シナリオ](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [Adobe Experience Platform サービスと Adobe Experience Platform Web SDK の統合](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [Adobe Experience Platform Mobile SDK および Launch を使用してモバイルアプリケーション開発を加速](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [Adobe Experience Platform Web SDK で顧客ワークフローをシンプルに](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
