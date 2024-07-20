---
title: 複数サンドボックスイベント転送のデータ収集
description: Experience Platform Web SDK および Mobile SDK で収集されたデータを、単一のイベントを収集して複数の Experience Platform サンドボックスに転送するように設定する方法について説明します。
solution: Data Collection
kt: 7202
exl-id: ecc94fc8-9fad-4b88-a153-3d0fc00d8d58
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 55%

---

# 複数サンドボックスイベント転送のデータ収集

このブループリントは、[!DNL Experience Platform] Web SDK および Mobile SDK で収集されるデータを、1 つのイベントを収集して複数の AEP サンドボックスに転送するように設定する方法を示しています。 このブループリントは、[!UICONTROL イベント転送]を使用してこの目標を達成する複数サンドボックスデータ収集に特化しています。

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

[!UICONTROL  イベント転送 ] は HIPAA 対応とは見なされないので、HIPAA データが収集される HIPAA のユースケースでは使用しないでください。

ただし、[!UICONTROL  イベント転送 ] に使用されるインフラストラクチャは HIPAA に対応していると見なされ、お客様の判断においてのみ使用されます。 [!UICONTROL イベント転送]タグのプロパティは[!UICONTROL イベント転送]システムに存在しますが、収集されたデータペイロード全体が[!UICONTROL イベント転送]システムに送信されて処理されます。このプロセスでは、HIPAA のユースケースに関する [!UICONTROL  イベント転送 ] が行われます。 [!UICONTROL  イベント転送 ] システムに送信されたペイロード全体を使用すると、このプロセスには HIPAA 値が含まれます。 [!UICONTROL  イベント転送 ] ルールでは、そのデータを宛先に送信する前にフィルタリングしますが、その HIPAA データは、HIPAA に対応していないインフラストラクチャに送信されます。 ただし、ペイロードデータは保存されず、単なるパススルーです。

### 異なるデータストリームとストリーミングエンドポイント

[!UICONTROL  イベント転送 ] を使用して別の AEP サンドボックスに送信する場合、データは [!DNL Platform Edge Network] からデータストリームを通過するので、元のコレクションを作成するデータストリームと同じデータストリームまたはストリーミングエンドポイントを使用しないことが要件です。 AEP インスタンスに悪影響を与え、DoS の状況が発生する可能性があります。

### 推定トラフィック量

トラフィック量は、各ユースケースでの確認に必要です。トラフィック量が多いとスロットルが発生する可能性があるので、この処理は重要です。発生した場合はお客様に通知されます。

## アーキテクチャ

![複数サンドボックス[!UICONTROL イベント転送]](assets/multi-sandbox-data-collection.png)

1. [!UICONTROL  イベント転送 ] を使用するには、イベントデータを収集して [!DNL Platform Edge Network] に送信する必要があります。 Adobeタグは、クライアントサイドの場合はクライアントサイドで、[!DNL Platform Edge Network Server API] ーバー間のデータ収集の場合はサーバー間のデータ収集に使用できます。

   [!DNL Platform Edge Network API] は、サーバー間の収集機能を提供できます。 ただし、これには、別のプログラミングモデルを実装する必要があります。 [Edge Network Server API の概要](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)を参照してください。

1. 収集されたペイロードは、タグ実装から [!DNL Platform Edge Network] に [!UICONTROL  イベント転送 ] サービスに送信され、独自の [!UICONTROL  データ要素 ]、[!UICONTROL  ルール ]、[!UICONTROL  アクション ] によって処理されます。 違いについて詳しくは、[ タグと [!UICONTROL  イベント転送 ]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ja#differences-from-tags) を参照してください。

1. また、イベントデータがデプロイ済みのタグ実装によってサーバーに送信されたか、サーバー間コレクションによって [!DNL Platform Edge Network] に送信されたかに関わらず、[!DNL Platform Edge Network] から収集されたイベントデータを受信するには、[!UICONTROL  イベント転送 ] プロパティも必要です。

   作成者は、2 番目のサンドボックスに転送する前にイベントデータのエンリッチメントに使用する、データ要素、ルール、アクションを定義します。カスタムコードの [!DNL JavaScript] データ要素を使用して、サンドボックス取り込み用のデータを構造化するのに役立てることを検討してください。Platform のデータ準備機能と組み合わせて、データ構造を管理するオプションがいくつかあります。

1. 現状、[!UICONTROL イベント転送]プロパティ内で Adobe [!UICONTROL Cloud Connector 拡張機能]を使用する必要があります。ルールがイベントデータを処理またはエンリッチメントした後、サンドボックスに設定された取得呼び出し内で [!UICONTROL Cloud Connector] が使用され、POSTが 2 番目のサンドボックスに送信されます。

1. 2 つ目のサンドボックスには、データ取り込み用のストリーミングエンドポイントが必要です。 また、AEP で [!UICONTROL  データ準備 ] 機能を検討して、[!UICONTROL  イベント転送 ] ペイロードの XDM への取り込みとマッピングに役立てることもできます。 AEP ドキュメント [UI を使用した HTTP API ストリーミング接続の作成](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=ja)を参照してください。
