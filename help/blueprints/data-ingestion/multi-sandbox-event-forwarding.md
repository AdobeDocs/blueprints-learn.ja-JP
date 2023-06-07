---
title: マルチサンドボックスイベント転送のデータ収集
description: Experience PlatformWeb および Mobile SDK で収集されたデータを、単一のイベントを収集し、複数のExperience Platformサンドボックスに転送するように設定する方法について説明します。
solution: Data Collection
kt: 7202
source-git-commit: e9a9abeaa722bb2f9a232f4e861b1b5eae86edd1
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 4%

---


# マルチサンドボックスイベント転送のデータ収集

このブループリントは、Experience Platformの Web および Mobile SDK で収集されたデータを、単一のイベントを収集し、複数の AEP サンドボックスに転送するように設定する方法を示します。 このブループリントは、を使用するマルチサンドボックスデータコレクションに固有です。 [!UICONTROL イベント転送] この目標を達成するために

イベントを [!UICONTROL イベント転送] 機能を使用すると、他のサンドボックスの要件を満たす、収集された元のデータに対して、追加、フィルタリングまたは操作をおこなうことができます。

[!UICONTROL イベント転送] は、 [!UICONTROL データ要素], [!UICONTROL ルール]、および [!UICONTROL 拡張機能] データ要件に応じて必要です。 受信イベントの場合、 [!UICONTROL イベント転送] プロパティは、転送の前に、必要に応じてデータを収集し、管理できます。

宛先サンドボックスには、Adobeが使用する HTTP ストリーミングエンドポイントが設定されている必要があります [!UICONTROL クラウドコネクタ] 拡張子。

## ユースケース

* グローバルデータレポート — 複数のサンドボックスを使用して操作環境を分離し、クロスサンドボックスレポートのためにデータ収集を 1 つのサンドボックスに統合する必要がある場合。 経由での Experience Edge イベントのルーティング [!UICONTROL イベント転送] レポートサンドボックスに追加すると、各サンドボックス操作環境は、リアルタイムで収集されたデータをレポートサンドボックスに送信できます。

* サンドボックスの操作環境ごとに異なるデータルールに基づいて、サンドボックス全体のデータ収集を管理します。

## アプリケーション

* [!DNL Experience Platform] データ収集
* [!UICONTROL イベント転送]
* AEP [!UICONTROL 拡張]
* [!UICONTROL Cloud Connector 拡張機能]

## 注意点

を使用 [!UICONTROL イベント転送] データを複数のサンドボックスに送信するアプローチとして、ソリューションアーキテクチャで考慮する必要がある考慮事項があります。

### HIPAA データがありません

[!UICONTROL イベント転送] は HIPAA Ready とは見なされず、HIPAA データが収集される HIPAA の使用例では使用しないでください。 ただし、 [!UICONTROL イベント転送] は HIPAA 対応と見なされ、お客様の裁量にのみ従います。 その間、 [!UICONTROL イベント転送] タグプロパティは、 [!UICONTROL イベント転送] システムでは、収集されたデータペイロード全体が [!UICONTROL イベント転送] 処理するシステム。 このプロセスが [!UICONTROL イベント転送] HIPAA の使用例に関する情報を含む ) ペイロード全体が [!UICONTROL イベント転送] システムの場合は、HIPAA 値も含まれます。 ただし、 [!UICONTROL イベント転送] ルールは、宛先に送信する前に、HIPAA 対応のインフラストラクチャ以外に HIPAA 対応のインフラストラクチャに送信されるデータをフィルタリングします。 ただし、ペイロードデータは保存されず、単にパススルーになります。

### 異なるデータストリームとストリーミングエンドポイント

データが [!UICONTROL Platform Edge Network]を使用する場合 [!UICONTROL イベント転送] 別の AEP サンドボックスに対しては、元のコレクションを作成するデータストリームと同じデータストリームまたはストリーミングエンドポイントを使用しないでください。 これは、AEP インスタンスに悪影響を与え、DoS の状況が発生する可能性があります。

### 推定トラフィック量

トラフィック量は、各使用例での確認に必要です。 ボリュームが多いとスロットル状況が発生し、これが発生すると顧客に通知されるので、これは重要です。

## アーキテクチャ

![マルチサンドボックス [!UICONTROL イベント転送]](assets/multi-sandbox-data-collection.png)

1. イベントデータを収集し、 [!UICONTROL Platform Edge Network] は、 [!UICONTROL イベント転送]. お客様は、Adobeタグをクライアント側または [!UICONTROL Platform Edge Network Server API] （サーバー間データ収集用） この [!UICONTROL Platform Edge Network API] は、サーバー間収集機能を提供します。 ただし、実装には別のプログラミングモデルが必要です。 参照： [Edge Network Server API の概要](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

1. 収集されたペイロードは、タグ実装から [!UICONTROL Platform Edge Network] から [!UICONTROL イベント転送] 独自に処理された [!UICONTROL データ要素], [!UICONTROL ルール] および [!UICONTROL アクション]. の違いについて詳しくは、 [タグと [!UICONTROL イベント転送]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en#differences-from-tags).

1. An [!UICONTROL イベント転送] プロパティが [!UICONTROL Platform Edge Network]. デプロイ済みのタグ実装またはサーバー間コレクションによって、イベントデータが Platform Edge ネットワークに送信されたかどうか。 作成者は、2 番目のサンドボックスに転送する前にイベントデータをエンリッチメントするために使用するデータ要素、ルール、アクションを定義します。 カスタムコードの使用を検討する [!DNL JavaScript] データ要素を使用して、サンドボックス取り込み用のデータを構造化するのに役立てます。 Platform のデータ準備機能と組み合わせて、データ構造を管理するためのいくつかのオプションがあります。

1. 現在、Adobe [!UICONTROL Cloud Connector 拡張機能] は、 [!UICONTROL イベント転送] プロパティ。 ルールがイベントデータを処理またはエンリッチメントすると、Cloud Connector は、2 番目のサンドボックスにペイロードを送信するPOST用に設定されたフェッチ呼び出し内で使用されます

1. 2 番目のサンドボックスには、データ取り込みのストリーミングエンドポイントが必要です。 また、AEP でのデータ準備機能を検討して、の取り込みとマッピングに役立てることもできます。 [!UICONTROL イベント転送] XDM へのペイロード。 AEP ドキュメントの作成を参照してください。 [UI を使用した HTTP API ストリーミング接続](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=ja)
