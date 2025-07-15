---
title: B2B オーディエンスおよびプロファイルのアクティベーションブループリント
description: Real-time Customer Data Platform を使用して、アカウントベースのオーディエンスと、プロファイル中心のカスタマーエクスペリエンスを提供します。
solution: Real-Time Customer Data Platform
kt: 9311
exl-id: 5215d077-b0a9-4417-ae9b-f4961d4a73fa
source-git-commit: 70816df06ec2dff5c3a4a94a8be701cb25e6f783
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 52%

---

# B2B オーディエンスおよびプロファイルのアクティベーションブループリント

個々の顧客に関連付けられたアカウント、オポチュニティおよびリード情報を使用して、アクションにつながる B2B プロファイルを作成し、チャネルをまたいだパーソナライゼーションとターゲティングを改善します。

## ユースケース

* アカウント、商談、リードを含む B2B データに対して、複数のチャネルをまたいでターゲティングとパーソナライゼーションをおこなうための顧客のオーディエンスを作成します。
* ターゲティングとパーソナライゼーションのために、Experience Platform の宛先に対してオーディエンスをアクティブ化します。
* アカウントのオーディエンス（会社のリストなど）を作成し、ターゲティングやセールスアウトリーチのためにクラウドストレージの宛先への入力または書き出しとして会社のリストを受け入れる LinkedIn などの宛先を介して、それらの会社をターゲットにします。

## アプリケーション

* Real-time Customer Data Platform B2B エディション

## 統合パターン

* B2B データソース（Marketo、Salesforceなど）/Real-time Customer Data Platform B2B edition/宛先
* 様々な B2B データソースを使用して、アカウント、リード、オポチュニティおよび人物のデータを Real-time Customer Data Platform のB2B editionにマッピングできます。

## アーキテクチャ

![B2B アクティベーションブループリントのリファレンスアーキテクチャ ](assets/b2b-activation.png)

## ガードレール

* Marketo Engage 関連のガードレールおよび実装手順は、Marketo Engage がソースまたは宛先として使用されている場合にのみ該当します。

* データモデル、サイズ、セグメント化のその他の詳細とガードレールについては、[ デプロイメントガードレールのドキュメント ](../experience-platform/deployment/guardrails.md) を参照してください。


### 複数のインスタンスと IMS 組織のサポート：

以下に、Experience Platform および Marketo Engage のインスタンスのマッピングにおいてサポートされるパターンの概要を示します。

#### Experience Platform に対するデータソースとしての Marketo：

* 1 つの Marketo Engage インスタンスに対する複数の Experience Platform インスタンスがサポートされます。
* 多数の Marketo Engage インスタンスに対する 1 つの Experience Platform インスタンスは、サポートされていません。
* 1 つの Experience Platform インスタンスに対する 1 つの Marketo Engage インスタンスおよび複数のサンドボックスがサポートされます。

#### Experience Platform の宛先としての Marketo：

* 多数の Marketo Engage インスタンスに対する Experience Platform がサポートされます
* 1 つの Marketo Engage インスタンスに対する多数の Experience Platform インスタンスがサポートされます

#### Experience Platform のプロファイルとセグメント化のガードレール：

* プロファイルとセグメント化のガードレールについては、Experience Platform の[プロファイルとセグメント化のガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)を参照してください
* アカウント、リード、商談を含む B2B セグメントでは、複数エンティティの関係を使用するので、セグメント評価がバッチになります。ストリーミングのセグメント化は、ユーザーとイベントに限定されたセグメントに対してサポートされます。
* ストリーミング b2b セグメントのユースケースをサポートするために、バッチ b2b セグメントをストリーミングセグメントまたはエッジセグメントへの入力として含めます。 バッチセグメントのメンバーシップは、最新の毎日のバッチセグメント化の評価結果に基づいています。

#### Experience Platform - Marketo Engage ソースコネクタ：

* 履歴バックフィルの完了には、データの量に応じて、最大 7 日かかる場合があります。
* Marketoからの継続的なデータ更新と変更は、ストリーミング API を介してExperience Platformに送信されます。この API は、プロファイルに対して最大 10 分程度の潜伏時間がかかることがあり、ボリュームに応じて、データレイクに対して最大 60 分かかることがあります。

#### Experience Platform - Marketo 宛先コネクタ：

* Real-time Customer Data Platform からMarketo Engageへのストリーミングセグメント共有は、セグメント評価から最大 15 分かかる場合があります。 アクティブ化の前にセグメントに既に存在していたプロファイルを初めてバックフィルするには、最大 24 時間かかる場合があります。
* バッチのセグメント化は、Experience Platform のセグメント化スケジュールに基づいて、1 日に 1 回共有されます。複数エンティティの関係を使用する B2B セグメント。例えば、アカウントおよび商談オブジェクトのデータを使用するセグメントは、常にバッチモードで実行されます。

#### Marketo Engage ガードレール：

* Real-time Customer Data Platform オーディエンスが Marketo Engage の連絡先およびリードと一致するには、連絡先とリードが Marketo Engage に直接取り込まれ、定義されている必要があります。
* RTCDP Marketoの宛先では、セグメントに参加しているがMarketoには存在しない顧客のために、オプションでMarketoで新しいリードを作成できます。

#### 宛先ガードレール

* 宛先に関する具体的なガイダンスについては、宛先のドキュメントを参照してください。[宛先ガードレール](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=ja)


## 実装手順

Real-time Customer Data Platform B2B エディションの実装と設定の方法に関するガイダンスについては、Real-time Customer Data Platform キュメントの B2B エディションを参照してください。[Real-time Customer Data Platform B2B エディション](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=ja)

実装には、2 つのパターンが存在する可能性があります。Marketo Engage から B2B データとプロファイルを取り込む機能と、他の CRM データソースから B2B データを取り込む機能の両方です。

## 実装に関する考慮事項

ブループリントの主要な考慮事項と設定に関するガイダンス

* Marketoを使用した場合と使用しない場合の CRM 統合：
Marketo Engageをソースとして使用し、Marketo Engageが CRM に接続されている場合、CRM データは自動的に同じ接続を経由するので、Marketoを経由しない CRM データオブジェクトが他にない限り、CRM を Platform に直接接続する必要がなくなります。 追加のテーブルを取り込む必要がある場合は、Experience Platform ソースコネクタを使用します。実装でMarketo Engageをソースとして使用しない場合は、CRM ソース Experience Platform コネクタを使用して CRM ソースを Platform に直接接続します。
* Marketo Engage Destination Connector for Platform は、オーディエンスをMarketo Engageにプッシュしてアクティブ化し、一致するメールアドレスと ECID に基づいてオーディエンスメンバーを共有します。 連絡先が存在しない場合は、新しいリードを作成するオプションがあります。 新しいリードを作成する際に、Real-time Customer Data Platform の最大 50 個のプロファイル属性（非配列またはマップ属性）をMarketoの人物フィールドにマッピングできます。

## 関連ドキュメント

* [Real-time Customer Data Platform B2B エディション](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=ja)
* [Real-time Customer Data Platform B2B editionの概要 ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial)
* [Real-time Customer Data Platform B2B editionのガードレール ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails)
* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Marketo Engage](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=ja)
* [Adobe Experience Platform - Marketo ソースコネクタ](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=ja)
* [Adobe Experience Platform - Marketo 宛先コネクタ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=ja)
