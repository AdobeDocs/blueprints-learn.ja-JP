---
title: 複数サンドボックスイベント転送のデータ収集
description: Experience Platform Web SDK および Mobile SDK で収集されたデータを、単一のイベントを収集して複数の Experience Platform サンドボックスに転送するように設定する方法について説明します。
solution: Data Collection
kt: 7202
exl-id: 3d9d312a-50b6-435f-b277-076e0c442a5f
source-git-commit: cb36f47232261d6ddc6659949272c9832baec0da
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 100%

---

# 複数サンドボックスイベント転送のデータ収集

このブループリントは、Experience Platform Web SDK および Mobile SDK で収集されたデータを、単一のイベントを収集して複数の AEP サンドボックスに転送するように設定する方法を示します。このブループリントは、[!UICONTROL イベント転送]を使用してこの目標を達成する複数サンドボックスデータ収集に特化しています。

イベントのレプリケーションに加え、[!UICONTROL イベント転送]機能を使用して、オリジナルの収集データからその他のサンドボックスの要件を満たすものを追加したり、フィルタリングしたり、操作したりできます。

[!UICONTROL イベント転送]は、データ要件に必要な[!UICONTROL データ要素]、[!UICONTROL ルール]、[!UICONTROL 拡張機能]を含む個別のタグプロパティを使用します。受信イベントを使用すると、[!UICONTROL イベント転送]プロパティでデータを収集し、転送の前に必要に応じて管理できます。

宛先サンドボックスには、Adobe [!UICONTROL Cloud Connector] 拡張機能で使用される HTTP ストリーミングエンドポイントが設定されている必要があります。

## ユースケース

* グローバルデータレポート - 複数のサンドボックスを使用して操作環境を分離し、クロスサンドボックスレポート用にデータ収集を 1 つのサンドボックスに統合する必要がある場合。[!UICONTROL イベント転送]を通して Experience Edge イベントをレポートサンドボックスにルーティングすると、各サンドボックス操作環境は、リアルタイムで収集されたデータをレポートサンドボックスに送信できます。

* サンドボックスの操作環境ごとに異なるデータルールに基づいて、サンドボックス全体のデータ収集を管理します。

## アプリケーション

* [!DNL Experience Platform] データ収集
* [!UICONTROL イベント転送]
* [!UICONTROL AEP 拡張機能]
* [!UICONTROL Cloud Connector 拡張機能]

## 注意点

複数のサンドボックスにデータを送信するアプローチとして[!UICONTROL イベント転送]を使用する際、ソリューションアーキテクチャで考慮するべき懸念事項があります。

### HIPAA データなし

[!UICONTROL イベント転送は HIPAA 対応と見なされません。HIPAA データが収集される HIPAA のユースケースでは使用しないでください。]ただし、[!UICONTROL イベント転送]に使用される基盤は HIPAA 対応と見なされ、あくまでお客様の裁量に任されています。[!UICONTROL イベント転送]タグのプロパティは[!UICONTROL イベント転送]システムに存在しますが、収集されたデータペイロード全体が[!UICONTROL イベント転送]システムに送信されて処理されます。HIPAA のユースケースに関して[!UICONTROL イベント転送]が懸念されるのは、このプロセスです。ペイロード全体が[!UICONTROL イベント転送]システムに送信された場合、これに HIPAA 値が含まれます。[!UICONTROL イベント転送]のルールにより、該当データは宛先に送信する前にフィルタリングされますが、それでも HIPAA データは HIPAA 非対応の基盤に送信されます。ただし、ペイロードデータは保存されず、単に通過します。

### 異なるデータストリームとストリーミングエンドポイント

データは [!UICONTROL Platform Edge Network] からデータストリームを流れるので、[!UICONTROL イベント転送]を別の AEP サンドボックスに対して使用する場合、オリジナルのコレクションを作成するデータストリームと同じデータストリームまたはストリーミングエンドポイントを絶対に使用しないでください。AEP インスタンスに悪影響を与え、DoS の状況が発生する可能性があります。

### 推定トラフィック量

トラフィック量は、各ユースケースでの確認に必要です。トラフィック量が多いとスロットルが発生する可能性があるので、この処理は重要です。発生した場合はお客様に通知されます。

## アーキテクチャ

![複数サンドボックス[!UICONTROL イベント転送]](assets/multi-sandbox-data-collection.png)

1. [!UICONTROL イベント転送]を使用するには、イベントデータを収集して [!UICONTROL Platform Edge Network] に送信する必要があります。お客様は、クライアントサイド用のアドビのタグや、サーバー間データ収集用の [!UICONTROL Platform Edge Network Server API] を使用できます。[!UICONTROL Platform Edge Network API] は、サーバー間収集機能を提供します。ただし、この実装には別のプログラミングモデルが必要です。[Edge Network Server API の概要](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)を参照してください。

1. 収集されたペイロードは、タグ実装から [!UICONTROL Platform Edge Network] に[!UICONTROL イベント転送]サービスに送信され、独自の[!UICONTROL データ要素]、[!UICONTROL ルール]、[!UICONTROL アクション]で処理されます。タグとイベント転送の違いについて詳しくは、[タグと[!UICONTROL イベント転送]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ja#differences-from-tags)を参照してください。

1. 収集されたイベントデータを [!UICONTROL Platform Edge Network] から受け取るには、[!UICONTROL イベント転送]プロパティも必要です。デプロイ済みのタグ実装またはサーバー間コレクションによって、イベントデータが Platform Edge Network に送信されたかどうか。作成者は、2 番目のサンドボックスに転送する前にイベントデータのエンリッチメントに使用する、データ要素、ルール、アクションを定義します。カスタムコードの [!DNL JavaScript] データ要素を使用して、サンドボックス取り込み用のデータを構造化するのに役立てることを検討してください。Platform のデータ準備機能と組み合わせて、データ構造を管理するオプションがいくつかあります。

1. 現状、[!UICONTROL イベント転送]プロパティ内で Adobe [!UICONTROL Cloud Connector 拡張機能]を使用する必要があります。ルールがイベントデータを処理またはエンリッチメントすると、Cloud Connector は、2 番目のサンドボックスにペイロードを送信する POST 用に設定された、取得呼び出し内で使用されます

1. 2 番目のサンドボックスには、データ取り込みのストリーミングエンドポイントが必要です。また、AEP のデータ準備機能を使用して、[!UICONTROL イベント転送]ペイロードの XDM への取り込みとマッピングに役立てることも検討できます。AEP ドキュメント [UI を使用した HTTP API ストリーミング接続の作成](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=ja)を参照してください。
