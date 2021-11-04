---
title: B2B アクティベーション
description: Real-time Customer Data Platformを使用して、アカウントベースのオーディエンスとプロファイル中心の顧客エクスペリエンスを提供し​ます。
solution: Experience Platform, Real-time Customer Data Platform
kt: 9311
exl-id: null
source-git-commit: d811d82418d477372caa9e5b0b67af197275d459
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 4%

---

# B2B オーディエンスとプロファイルのアクティベーション

個々の顧客に関連付けられたアカウント、オポチュニティおよびリード情報を使用して、アクションにつながる b2b プロファイルを作成し、チャネルをまたいだパーソナライゼーションとターゲティングを改善します。

## ユースケース

* アカウント、商談、リードを含む B2B データに対して、複数のチャネルをまたいでターゲティングとパーソナライゼーションをおこなうための顧客のオーディエンスを作成します。
* ターゲティングとパーソナライゼーションのために、Experience Platformの宛先に対するオーディエンスをアクティブ化します。

## アプリケーション

* Real-time Customer Data Platform B2B エディション

## 統合パターン

* B2B データソース (Marketo、Salesforce など ) -> Real-time Customer Data Platform B2B Edition -> Destinations 様々な B2B データソースを使用して、アカウント、リード、オポチュニティおよび人のデータをReal-time Customer Data Platformの B2B Edition にマッピングできます。

## アーキテクチャ

<img src="assets/b2b-activation.svg" alt="B2B アクティベーションブループリントの参照アーキテクチャ" style="border:1px solid #4a4a4a" />
<br>

## ガードレール

Marketo Engage関連のガードレールおよび実装手順は、Marketo Engageがソースまたは宛先として使用されている場合にのみ関連します。

### 複数のインスタンスと IMS 組織のサポート：

次に、マッピングインスタンスとMarketo EngageインスタンスでサポートされるExperience Platformの概要を示します。

#### Marketo as a data source toExperience Platform:

* 1 つのMarketo Engageインスタンスに対する複数のExperience Platformインスタンスがサポートされます。
* 多数のMarketo Engageインスタンスに対する複数のExperience Platformインスタンスは、をサポートしていません。
* 1 つのMarketo Engageインスタンスから多くのExperience Platformインスタンスへの変換はサポートされていません。
* 1 つのMarketo Engageインスタンスから 1 つのExperience Platformインスタンスへ、複数のサンドボックスへとがサポートされます。

#### MarketoをExperience Platformの宛先にする：

* 多数のMarketo EngageインスタンスへのExperience Platformがサポートされます
* 1 つのExperience Platformインスタンスに対する多数のMarketo Engageインスタンスがサポートされます

#### Experience Platformプロファイルとセグメント化ガードレール：

* Experience Platformのプロファイルとセグメント化のガードレールを参照してください — [プロファイルとセグメント化のガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* アカウント、リード、商談を含む B2B セグメントでは、複数エンティティの関係を使用するので、セグメント評価がバッチになります。 ストリーミングセグメント化は、ユーザーとイベントに限定されたセグメントでサポートされます。

#### Experience Platform-Marketo Engageソースコネクタ：

* 履歴バックフィルの完了には、データの量に応じて、最大 7 日かかる場合があります。
* Marketoからの継続的なデータ更新や変更は、ストリーミング API を介してExperience Platformに送信されます。ストリーミング API は、プロファイルに対して最大 5 分、ボリュームに応じてデータレイクに対して約 15 分待ちます。

#### Experience Platform- Marketo宛先コネクタ：

* Real-time Customer Data PlatformからMarketo Engageへのストリーミングセグメントの共有には、最大 5 分かかる場合があります。
* バッチセグメント化は、Experience Platformセグメント化スケジュールに基づいて、1 日に 1 回共有されます。 アカウント、リード、商談を含む B2B セグメントでは、複数エンティティの関係を使用するので、セグメントがバッチになります。

#### Marketo Engageガードレール：

* Real-time Customer Data PlatformオーディエンスがMarketo Engageの連絡先およびリードと一致するには、連絡先とリードがMarketo Engageで直接取り込まれ、定義されている必要があります。

#### 宛先ガードレール

* 宛先に関する具体的なガイダンスについては、宛先のドキュメントを参照してください。 [宛先のガイドライン](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)


## 実装手順

Real-time Customer Data Platformの B2B エディションの実装と設定の方法に関するガイダンスについては、Real-time Customer Data Platformドキュメントの B2B エディションを参照してください。 [B2B エディションオブReal-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=en)

実装には、2 つのパターンが存在する可能性があります。 Marketo Engageから B2B データとプロファイルを取り込む機能と、他の CRM データソースから B2B データを取り込む機能の両方です。

## 実装に関する考慮事項

ブループリントの主要な考慮事項と設定に関するガイダンス

* Marketoとの CRM 統合となし：実装でMarketo Engageをソースとして使用し、Marketo Engageが CRM に接続される場合は、Experience PlatformでMarketoソースコネクタを使用して CRM データをExperience Platformに取り込みます。 追加のテーブルを取り込む必要がある場合は、Experience Platformソースコネクタを使用します。 実装でMarketo Engageをソースとして使用しない場合は、CRM ソースExperience Platformコネクタを使用して CRM ソースを AEP に直接接続します。
* Real-time Customer Data Platformの B2B エディションのみからのリードの開始と育成は、お勧めしません。 この使用例では、リード育成ツール (Marketo Engageなど ) の使用をお勧めします。
* AEP 用のMarketo Engage宛先コネクタは、アクティブ化のためにオーディエンスをMarketo Engageにプッシュし、電子メールアドレスと ECID のみをプッシュします。 連絡先が存在しない場合、新規リードは作成されません。そのため、プロファイルとリードのデータをMarketo Engageに取り込む必要があります。

## 関連ドキュメント

* [B2B エディションオブReal-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=en)
* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Marketo Engage](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=en)
* [Adobe Experience Platform - Marketo Source Connector](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=ja)
* [Adobe Experience Platform - Marketo Destination Connector](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en)