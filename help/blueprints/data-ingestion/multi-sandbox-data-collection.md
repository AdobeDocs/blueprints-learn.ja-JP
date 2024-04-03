---
title: マルチサンドボックスイベント転送のデータコレクションブループリント
description: 収集されたデータを次の方法でストリーミング： [!DNL Experience Platform] (AEP) イベント転送を使用した複数のサンドボックスへの SDK
solution: Data Collection
kt: 7202
exl-id: c24a47fe-b3da-4170-9416-74d2b6a18f32
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 60%

---

# マルチサンドボックスイベント転送のデータコレクションブループリント

マルチサンドボックスイベント転送のデータ収集ブループリントは、Adobeで収集されたデータの収集方法を示します [!DNL Experience Platform] Web および Mobile SDK は、単一のイベントを収集し、複数のイベントに転送するように設定できます [!DNL Experience Platform] (AEP) サンドボックス。 このブループリントは、Adobe タグのイベント転送機能を使用する特定のユースケースです。

イベントのレプリケーションに加えて、イベント転送機能を使用して、他のサンドボックスの要件を満たす、収集された元のデータの追加、フィルタリングまたは操作をおこなうことができます。例えば、サンドボックス A はすべてのイベントデータ要素を受け取り、サンドボックス B は PII 以外のデータのみを受け取る必要があります。

イベント転送は、データ要件に必要なデータ要素、ルール、拡張機能を含む個別のタグプロパティを使用します。 受信イベントを使用すると、イベント転送プロパティでデータを収集し、転送の前に必要に応じて管理できます。

宛先サンドボックスには、イベント転送 HTTPS 拡張機能で使用される HTTP ストリーミングエンドポイントが設定されている必要があります。

## ユースケース

* グローバルデータレポート - 複数のサンドボックスを使用して操作環境を分離し、クロスサンドボックスレポート用にデータ収集を 1 つのサンドボックスに統合する必要がある場合。イベントをレポートサンドボックスに転送すると、各サンドボックス操作環境は、リアルタイムで収集されたデータをレポートサンドボックスに送信できます
* サンドボックスの操作環境ごとに異なるデータルールに基づいて、サンドボックス全体のデータ収集を管理します。ヘルスケアや金融サービスなどの機密データをフィルタリングする必要があるこのようなオペレーティング環境

## アプリケーション

* Adobe [!DNL Experience Platform] データ収集

## アーキテクチャ

<img src="assets/multi-Sandbox-Data-Collection.svg" alt="マルチサンドボックスイベント転送のリファレンスアーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

1. タグ作成者は、タグプロパティとイベント転送プロパティの両方を定義します。ここでは、作成者はデータ収集を管理するデータ要素、ルール、アクションを定義します。 タグプロパティコードはクライアント上で実行され、CDN ホストによって配信されることに注意してください。The [!UICONTROL イベント転送プロパティ] コードはAdobe上で実行されます [!DNL Edge Server].

1. クライアントで収集されたデータは、 [!DNL Edge Network]. また、お客様は、サーバー側の収集方法として最初に独自のサーバーにデータを送信することもできます。 Web SDK は、サーバー間収集機能を提供します。ただし、この実装には別のプログラミングモデルが必要です。ドキュメントを参照してください。 **[!DNL Edge Network]サーバー API の概要** below

1. Platform [!DNL Edge Network] はデータ収集ペイロードを受け取り、Target や Analytics などの必要なシステムへのデータのフローを調整します。

1. イベント転送プロパティデータ要素は、ペイロードに到着したイベントデータにアクセスするために使用されます。また、転送の前に、必要に応じてイベントデータを操作する場合にも、ルールを使用することができます。ストリーミングデータ取り込みに必要な XDM へのデータの形式設定など

1. イベント転送は、イベントデータを HTTPS エンドポイントに転送する機能を提供する HTTPS 拡張機能を提供します。

1. サンドボックス 2 は、転送されたイベントを受信するストリーミングエンドポイントを使用して設定されます。

## 関連ドキュメント

* [イベント転送のドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ja)
* [イベント転送のビデオ](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html?lang=ja)
* Web SDK チュートリアルの[イベント転送のレッスン](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=ja)
* [[!DNL Experience Platform] Web SDK の概要](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ja)
* [[!DNL Edge Network] サーバー API の概要](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)

## 関連するブログ投稿

* [Adobeによる Web サイトのパフォーマンスの向上 [!DNL Experience Platform] Web SDK および [!DNL Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [実装上の問題点の解決とAdobe [!DNL Experience Platform] Web SDK および [!DNL Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [Adobe [!DNL Experience Platform] Audience Management 用 Web SDK](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [Adobe [!DNL Experience Platform] Web SDK - Adobe Target](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [Adobe [!DNL Experience Platform] Adobe Analyticsの Web SDK 移行シナリオ](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [統合Adobe [!DNL Experience Platform] サービスとAdobe [!DNL Experience Platform] Web SDK](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [Adobe [!DNL Experience Platform] Mobile SDK と Launch](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [Adobe Experience Platform Web SDK で顧客ワークフローをシンプルに](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
