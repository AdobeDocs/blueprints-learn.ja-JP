---
title: B2B Customer Journey Analyticsの設計図
description: アカウントベースのレポートとジャーニー分析のために、Customer Journey AnalyticsにB2B アカウント、商談、購買グループのデータを含めます。
solution: Customer Journey Analytics
exl-id: d55ed43d-aabf-4722-9ae9-a2aef99f19e0
source-git-commit: 8284380fb9202991f3da7d755225da2e38a50cac
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 7%

---

# B2B Customer Journey Analyticsの設計図

>[!TIP]
>このブループリントは、[ ユースケースパターン ](/help/blueprints/use-case-patterns/b2b/account-analytics.md)としてB2B Activation &amp; Marketingで利用することもできます。

Customer Journey Analytics B2B editionなら、B2B企業のアカウントベースのレポートと分析が可能になります。 人を中心としたB2C分析とは異なり、この設計図では&#x200B;**アカウント**&#x200B;をデータモデルの中心に置き、複数の関係者、購買グループ、セールスサイクルをまたいで複雑なB2B購入ジャーニーを分析できるようにします。 [!DNL Customer Journey Analytics]を使用して、行動データをB2B ディメンション（アカウント、機会、キャンペーン、マーケティングリスト）と統合し、ジャーニーベースのインサイトとオーディエンスの作成を実現します。

## アプリケーション

* Adobe [!DNL Customer Journey Analytics] （B2B edition）
* Adobe Experience Platform（B2Bおよびイベントデータ向け）

## ユースケース

* **アカウントマーケティングの最適化** — アカウント内の購買グループ、パイプラインの進行、アップセル/クロスセルの機会について、キャンペーン、チャネル、コンテンツをまたいでマーケティング効果を分析します。
* **主要アカウントを拡大** – 主要アカウント内の購買グループ全体で価値の高い顧客接点を特定し、マーケティングおよびセールスのアクションを伝え、アカウントレベルで顧客生涯価値を計算します。
* **製品価値を構築** – 製品リリースと使用がアカウントレベルとユーザーレベルで顧客満足度に与える影響を測定し、機能を最適化して開発に役立てることができます。
* **個人ベースのB2B分析** — アカウントと商談のコンテキストを、個々のユーザーの行動と組み合わせて、リードスコアリング、エンゲージメント、ジャーニー分析を行います。

## 前提条件

* [!DNL Customer Journey Analytics] B2B edition使用権限。
* Adobe Experience PlatformのB2B データと行動データ：[CJA接続](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html)で利用可能なB2B データセット（アカウント、商談、人物、キャンペーン、マーケティングリスト、B2B アクティビティ）とイベントデータ（web、モバイル、その他のチャネル）。
* CJA](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/b2b.html)の[B2B名前付け：B2B固有のデータビュー設定（アカウント ID、商談ID、および関連ディメンション）が接続に設定されています。

## アーキテクチャ

![B2B アカウントと商談データをジャーニー分析に統合したCustomer Journey Analytics アーキテクチャ ](assets/CJA.svg){zoomable="yes"}

Experience Platform（B2Bおよびイベントデータセット）からCJA接続を介して[!DNL Customer Journey Analytics]にデータフローが実行されます。 B2Bのディメンションはデータビューで公開されるため、アカウント、商談、人物のレベルで分析とオーディエンスを構築できます。

## ガードレール

* B2B edition製品の制限と使用権限については、[Customer Journey Analytics B2B製品の説明](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics-b2b.html)を参照してください。
* Analytics PlatformとCJAの技術的な制限については、[Analytics Platformのガードレール ](https://experienceleague.adobe.com/en/docs/analytics-platform/using/technotes/guardrails)を参照してください。
* CJA データの取り込みと接続の制限については、[Customer Journey Analytics データ取り込みのガードレール ](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html#what-is-the-expected-latency-for-analytics-data-on-platform%3F)を参照してください。
* CJA オーディエンスをReal-time Customer Data Platformに公開する場合は、[Customer Journey Analytics オーディエンス共有ガードレール ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)を参照してください。
* エンドツーエンドの遅延とプラットフォームのガードレールについては、[ デプロイメントガードレール ドキュメント ](../experience-platform/guardrails.md)を参照してください。

## 実装手順

1. **B2B データとイベントデータをExperience Platform**&#x200B;に取り込む – [ ソース ](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ja)を使用して、アカウント、商談、人物、キャンペーン、アクティビティのデータに加えて、行動イベントを取り込みます（例：[!DNL Marketo Engage]、CRM、その他のB2B コネクタ）。
2. **CJA接続を作成** — [関連するExperience Platform データセット ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html) （B2Bおよびイベント）をCustomer Journey Analytics接続に追加します。
3. **データビューでB2Bを設定** — [B2Bの命名と主要ディメンション ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/b2b.html) （アカウント ID、商談IDなど）を有効にします。 接続のデータビューに表示されます。
4. **アカウントベースの分析とオーディエンスの構築** — [CJA B2B ユースケースとレポート ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/b2b.html?lang=ja)を使用して、アカウントレベルおよび商談レベルでレポート、内訳、オーディエンスを作成します。オプションで[Real-time CDPにオーディエンスを公開してアクティベーションします。](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ja)

## 関連ドキュメント

### Customer Journey Analytics B2B edition

* [Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition.html)
* [B2B ユースケース](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/b2b.html?lang=ja)
* [B2B editionのユースケースの概要](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/b2b/b2b-edition/use-cases-overview.html)
* [個人ベースのB2B プロジェクトの例](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/b2b/example.html)

### 接続とデータビュー

* [接続の作成](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html)
* [B2B データビューの設定](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/b2b.html)

### オーディエンスとガードレール

* [CJA オーディエンスをReal-Time CDPに公開する](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ja)
* [Experience Platformとアプリケーションガードレール](../experience-platform/guardrails.md)
