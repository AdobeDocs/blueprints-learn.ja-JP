---
title: B2B オーディエンスとプロファイルのアクティベーション
description: Real-Time Customer Data Platform B2B editionなら、アカウントベースおよびピープルベースのオーディエンスを提供し、チャネルや配信先をまたいで活用できます。
solution: Real-Time Customer Data Platform
source-git-commit: 7f0b624616480cf563142c08eb0598d1dd55d551
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 5%
---

# B2B オーディエンスとプロファイルのアクティベーション

**Real-Time Customer Data Platform B2B edition**&#x200B;を使用して、アカウント、商談、人物のデータを統合されたB2B プロファイルにまとめ、LinkedIn、Marketo Engage、クラウドストレージなどの配信先で、人物オーディエンスとアカウントオーディエンスの両方をアクティブ化します。 このブループリントでは、B2B スキーマを設計し、複数のエンティティ オーディエンスを作成して、複数のチャネルと宛先をまたいでアクティベートし、**Journey Optimizer B2B edition**&#x200B;や&#x200B;**Customer Journey Analytics B2B edition**&#x200B;などのアプリケーションでオーケストレーションや分析を行うために書き出す方法について説明します。

## ユースケース

- アカウント、機会、リードなどのB2B データにもとづいて、チャネルをまたいでターゲティングやパーソナライゼーションに関与する人物のオーディエンスを構築できます。
- **セグメントのセグメント** アプローチを使用して、アカウントレベルおよび商談レベルの属性と個人レベルの行動を組み合わせたマルチエンティティオーディエンスを作成します（例：「過去3日間に価格ページを訪問し、業界Yのアカウントのステージ Xの機会における意思決定者」）。
- Experience Platformやクラウドストレージの宛先（Marketo Engage、LinkedIn Matched Audiences、Google Customer Match、DV360、The Trade Desk、Amazon Ads、Bombora、Demandbaseなど）に対して、ターゲティング、パーソナライゼーション、セールスアウトリーチ、分析のために、個人および企業のオーディエンスをアクティベートします。

## アプリケーション

- Real-Time Customer Data Platform B2B edition
- （オプション） **Customer Journey Analytics B2B edition**
- （オプション） **Journey Optimizer B2B edition**

## 統合パターン

このブループリントの一般的なB2B統合パターンは次のとおりです。

- **B2BのエンゲージメントとCRM ソース → RTCDP B2B →の宛先**

  B2B エンゲージメントおよびCRM システム（Marketo Engage、Salesforce、Microsoft Dynamicsなど）は、標準のB2B スキーマを使用して、リード/コンタクト、アカウント、商談を&#x200B;**Real-Time CDP B2B edition**&#x200B;に送信します。 そこから、人物やアカウントのオーディエンスが、次のような宛先にアクティベートされます。

  - Marketo Engage
  - LinkedIn/LinkedIn Matched Audiences
  - Google カスタマーマッチとDV360
  - The Trade Desk
  - Amazon Ads
  - Trade Desk CRM、Criteo、Bingなどの広告プラットフォーム
  - ダウンストリームで使用するAmazon S3、ADLS、Snowflakeなどのクラウドストレージの宛先

- **B2Bのインテントおよびイベントソース → RTCDP B2B →オーディエンス→宛先**

  B2Bの意図およびイベントソース：Bombora Intent、Demandbase Intent、PathFactory、RainFocusなどのストリームの意図およびエンゲージメントイベントをRTCDP B2Bに送信します。 これらのイベントは標準的なB2B スキーマにマッピングされ、広告やマーケティングの配信先で活用できる人物やアカウントのオーディエンスを構築するために使用されます。

様々なB2B データソースを使用して、標準の&#x200B;**B2B スキーマと関係**&#x200B;を使用して、アカウント、リード、商談、人物のデータをReal-Time Customer Data PlatformのB2B editionにマッピングできます。

## アーキテクチャ

<img src="assets/b2b-audience-profile-activation.png" alt="B2B オーディエンスおよびプロファイルアクティベーションの設計図のためのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a"  width="100%" />

## ガードレール

B2B オーディエンスとプロファイルを設計する際には、次のガードレールと適格性に関するドキュメントを参照してください。

- [Real-Time Customer Data Platform B2B editionのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails?lang=en)
- [Real-Time CDP B2B editionのセグメント化ユースケース](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/segmentation/b2b)
- [プロファイルとセグメント化のガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [ストリーミングセグメント化の適格基準の更新](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/eligibility-criteria-update)

### 複数のインスタンスとIMS組織のサポート

以下に、Experience Platform および Marketo Engage のインスタンスのマッピングにおいてサポートされるパターンの概要を示します。

#### Marketo as a data source to Experience Platform

- 1つのExperience Platform インスタンスに対する複数のMarketo Engage インスタンスがサポートされています。
- 多数の Marketo Engage インスタンスに対する 1 つの Experience Platform インスタンスは、サポートされていません。
- 1 つの Experience Platform インスタンスに対する 1 つの Marketo Engage インスタンスおよび複数のサンドボックスがサポートされます。

#### Experience Platformへの目的地としてのMarketo

- 多くのMarketo Engage インスタンスへのExperience Platformがサポートされています。
- 1つのMarketo Engage インスタンスに対する多くのExperience Platform インスタンスがサポートされています。

#### Experience Platformのプロファイルとセグメンテーションガードレール

Experience Platform プロファイルとセグメント化のガードレールについては、[ プロファイルとセグメント化のガードレール ](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)を参照してください。

アカウント、リード、商談などのB2B エンティティを含むセグメントは、複数のエンティティの関係に依存し、**バッチ**&#x200B;で評価されます。 対照的に、**ストリーミングセグメンテーション**&#x200B;は、B2B エンティティを組み込まない人物およびイベントに限定されたオーディエンスに対してサポートされます。 ほぼリアルタイムのB2B アクティベーションのシナリオについては、バッチ評価されたB2B オーディエンスを、ストリーミングオーディエンスやエッジオーディエンスの入力として使用することを検討してください。

#### Experience Platform - Marketo Engage Source Connector

- ドキュメント [こちら](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)を参照してください。

#### Experience Platform - Marketo Destination Connector

- ドキュメント [こちら](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage-connection)を参照してください。

#### 宛先ガードレール

- 各宛先に関する具体的なガイダンスについては、宛先ドキュメントを参照してください：[宛先ガードレール ](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)。
- Facebook、Google Customer Match &amp; DV360、Microsoft Bing、The Trade Desk、Amazon Ads、Bombora、Demandbaseなどの広告配信先では、スキーマおよびID戦略（メール、モバイル広告ID、アドレスフィールド、アカウント ID）で選択した識別子が、マッピング機能およびそれらの配信先でサポートされているIDと一致していることを確認します。

## 実装手順

Real-Time Customer Data PlatformのB2B editionの実装と設定方法に関するガイダンスについては、Real-Time CDP B2B editionのドキュメント「[Real-Time Customer Data PlatformのB2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)」を参照してください。

一般的な実装パターンは、次のふたつです。

- B2B データとプロファイルを、Marketo Engage（および接続されたCRM）からRTCDP B2B editionに取り込みます。
- 適切なソースコネクタを使用して、CRMなどのB2B システムから、B2B データをRTCDP B2B editionに直接取り込むことができます。

RTCDP B2B アーキテクチャのアップグレードの一環として、以前に使用されていたパターンの一部がB2B エンティティで非推奨（廃止予定）になりました。 詳細については、詳細なドキュメント [こちら](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-architecture-upgrade)を参照してください。

## 実装に関する考慮事項

ブループリントの主要な考慮事項と設定に関するガイダンス

- **MarketoとのCRM統合**

  - 実装でMarketo Engageをソースとして使用し、Marketo EngageがCRMに接続されている場合、Marketoに同期されたCRM データ（リード/コンタクト、アカウント、商談など）は、Marketo ソースコネクタを介してRTCDP B2B editionに流れます。
  - Marketoを介して渡されないCRM テーブルまたは属性（カスタムオブジェクトや追加フィールドなど）がある場合は、CRM ソースコネクタを使用してCRM ソースをExperience Platformに直接接続し、それらのテーブルを標準のB2B スキーマおよび関係にマッピングします。
  - CRMとMarketoの統合を設計することで、RTCDP B2BにおけるB2B エンティティの表現の重複や競合を回避し、あらゆるB2B エンティティが標準スキーマに準拠できるようにします。

## 関連ドキュメント

- [Real-Time Customer Data PlatformのB2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
- [Real-Time Customer Data Platform B2B editionの基本を学ぶ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial?lang=en)
- [Real-Time Customer Data Platform B2B editionのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails?lang=en)
- [Real-Time Customer Data Platform B2B editionのスキーマ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Real-Time CDP B2B editionへのアーキテクチャのアップグレード](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-architecture-upgrade)
- [Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform)
- [Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home)
- [Adobe Experience Platform - Marketo Source Connector](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Adobe Experience Platform - Marketo Destination Connector](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list)
- [宛先ガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
