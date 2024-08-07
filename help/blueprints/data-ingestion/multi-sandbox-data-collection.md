---
title: マルチサンドボックスイベント転送のデータコレクションブループリント
description: イベント転送を使用して、 [!DNL Experience Platform]  （AEP） SDK によって収集されたデータを複数のサンドボックスにストリーミングする
solution: Data Collection
kt: 7202
exl-id: c24a47fe-b3da-4170-9416-74d2b6a18f32
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 60%

---

# マルチサンドボックスイベント転送のデータ収集ブループリント

マルチサンドボックスイベント転送データ収集ブループリントは、Web および Mobile SDK[!DNL Experience Platform]Adobeで収集されるデータを、1 つのイベントを収集して複数の [!DNL Experience Platform] （AEP）サンドボックスに転送するように設定する方法を示しています。 このブループリントは、Adobe タグのイベント転送機能を使用する特定のユースケースです。

イベントのレプリケーションに加えて、イベント転送機能を使用して、他のサンドボックスの要件を満たす、収集された元のデータの追加、フィルタリングまたは操作をおこなうことができます。例えば、サンドボックス A はすべてのイベントデータ要素を受け取り、サンドボックス B は PII 以外のデータのみを受け取る必要があります。

イベント転送は、データ要件に必要なデータ要素、ルールおよび拡張機能を含む個別のタグプロパティを使用します。 受信イベントを使用すると、イベント転送プロパティでデータを収集し、転送の前に必要に応じて管理できます。

宛先サンドボックスには、イベント転送 HTTPS 拡張機能で使用される HTTP ストリーミングエンドポイントが設定されている必要があります。

## ユースケース

* グローバルデータレポート - 複数のサンドボックスを使用して操作環境を分離し、クロスサンドボックスレポート用にデータ収集を 1 つのサンドボックスに統合する必要がある場合。イベントをレポートサンドボックスに転送すると、各サンドボックス操作環境は、リアルタイムで収集されたデータをレポートサンドボックスに送信できます
* サンドボックスの操作環境ごとに異なるデータルールに基づいて、サンドボックス全体のデータ収集を管理します。ヘルスケアや金融サービスなどの機密データをフィルタリングする必要があるこのようなオペレーティング環境

## アプリケーション

* データ収集 [!DNL Experience Platform]Adobe

## アーキテクチャ

<img src="assets/multi-Sandbox-Data-Collection.svg" alt="マルチサンドボックスイベント転送のリファレンスアーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

1. タグ作成者は、タグプロパティとイベント転送プロパティの両方を定義します。ここでは、作成者がデータ収集を管理するデータ要素、ルール、アクションを定義します。 タグプロパティコードはクライアント上で実行され、CDN ホストによって配信されることに注意してください。[!UICONTROL  イベント転送プロパティ ] コードは、Adobe[!DNL Edge Server] で実行されます。

1. クライアントで収集されたデータは [!DNL Edge Network] に送信されます。 また、サーバーサイド収集の方法として、最初に独自のサーバーにデータを送信するオプションもあります。 Web SDK は、サーバー間収集機能を提供します。ただし、この実装には別のプログラミングモデルが必要です。以下のサーバー API の概要 **[!DNL Edge Network]関するドキュメントを参照** てください

1. Platform [!DNL Edge Network] は、データ収集ペイロードを受信し、Target や Analytics などの必要なシステムへのデータのフローを調整します。

1. イベント転送プロパティデータ要素は、ペイロードに到着したイベントデータにアクセスするために使用されます。また、転送の前に、必要に応じてイベントデータを操作する場合にも、ルールを使用することができます。ストリーミングデータ取り込みに必要な XDM へのデータの形式設定など

1. イベント転送は、イベントデータを HTTPS エンドポイントに転送する機能を提供する HTTPS 拡張機能を提供します。

1. サンドボックス 2 は、転送されたイベントを受信するストリーミングエンドポイントを使用して設定されます。

## 関連ドキュメント

* [イベント転送のドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ja)
* [イベント転送のビデオ](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html?lang=ja)
* Web SDK チュートリアルの[イベント転送のレッスン](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=ja)
* [[!DNL Experience Platform] Web SDK の概要 ](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ja)
* [[!DNL Edge Network] Server API の概要 ](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)

## 関連するブログ投稿

* [Adobe [!DNL Experience Platform] Web SDK を使用した web サイトのパフォーマンスの向上  [!DNL Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [Adobe [!DNL Experience Platform] Web SDK を使用した実装上の問題点の解決  [!DNL Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [Audience Management のAdobe [!DNL Experience Platform] Web SDK](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [Adobe [!DNL Experience Platform] Web SDK - Adobe Target](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [Adobe AnalyticsのAdobe [!DNL Experience Platform] Web SDK 移行シナリオ ](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [Adobe [!DNL Experience Platform] Web SDK を使用したAdobe [!DNL Experience Platform]  サービスの統合 ](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [Adobe [!DNL Experience Platform]  モバイル SDK と Launch を使用したモバイルアプリケーションの開発の高速化 ](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [Adobe Experience Platform Web SDK で顧客ワークフローをシンプルに](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
