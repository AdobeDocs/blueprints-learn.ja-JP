---
title: イベント転送ブループリント
description: SDK による収集データ  [!DNL Experience Platform]  宛先へのストリーミング配信
solution: Data Collection
kt: 7202
exl-id: 8d6f0705-628b-44e4-a3fc-da6c5e308a5b
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 55%

---

# イベント転送のブループリント

イベント転送のブループリントは、Web および Mobile SDK[!DNL Experience Platform]Adobeで収集されたデータを [!DNL Experience Platform] [!DNL Edge Network] から目的の宛先に転送する方法を示しています。 SDK から収集された生のデータをすべて転送することも、タグプロパティ（旧称 Launch）で設定されたイベントおよびルールに基づいて特定のデータを転送することもできます。

## ユースケース

* 単一の収集タグを使用して Web またはモバイルからデータを収集し、クライアントブラウザーおよびアプリのコードを軽量化します。データ収集の単一のソースとするため、収集したデータを様々なエンドポイントに伝達します。
* 収集されたデータをパートナーアプリケーションやデータ保存場所に転送して、収集されたデータに対するインサイトおよびアプリケーションを構築します。

## アプリケーション

* データ収集 [!DNL Experience Platform]Adobe

## アーキテクチャ

<img src="assets/enterprise_collection.svg" alt="エンタープライズデータ収集の参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## 関連ドキュメント

* [イベント転送のドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ja)
* [イベント転送のビデオ](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html?lang=ja)
* Web SDK チュートリアルの[イベント転送のレッスン](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=ja)

## 関連するブログ投稿

* [Adobe [!DNL Experience Platform] Web SDK を使用した web サイトのパフォーマンスの向上  [!DNL Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [Adobe [!DNL Experience Platform] Web SDK を使用した実装上の問題点の解決  [!DNL Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [Audience Management のAdobe [!DNL Experience Platform] Web SDK](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [Adobe [!DNL Experience Platform] Web SDK - Adobe Target](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [Adobe AnalyticsのAdobe [!DNL Experience Platform] Web SDK 移行シナリオ ](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [Adobe [!DNL Experience Platform] Web SDK を使用したAdobe [!DNL Experience Platform]  サービスの統合 ](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [Adobe [!DNL Experience Platform]  モバイル SDK と Launch を使用したモバイルアプリケーションの開発の高速化 ](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [Adobe [!DNL Experience Platform] Web SDK を使用したカスタマーワークフローのシンプル化 ](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
