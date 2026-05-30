---
title: B2B Audience Activation
description: web、電子メール、広告のチャネルをまたいでアカウントベースのB2B オーディエンスを活用する方法について解説します。
solution: Real-Time Customer Data Platform
exl-id: 2b979159-37aa-41d4-a6b4-1105538f6546
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 2%

---

# B2B オーディエンスのアクティベーション

このガイドでは、[!DNL Adobe Real-Time Customer Data Platform] （[!DNL RT-CDP]）B2B editionを使用して、web、メール、広告、CRM チャネルをまたいでアカウントレベルのオーディエンスを構築、評価、アクティブ化するB2B オーディエンスのアクティベーションのユースケース パターンについて説明します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

このパターンは、アカウントプロファイルの統合からオーディエンスの評価とアクティベーション、そして[!DNL Marketo Engage]、[!DNL LinkedIn]、CRM システムなどのB2B固有の宛先までのライフサイクル全体をカバーしています。

## ユースケースパターン

**B2B オーディエンスのアクティブ化**

web、電子メール、広告のチャネルをまたいで、アカウントベースのB2B オーディエンスを活用できます。

**実行プラン：** Account Profile Enrichment > Account Audience Evaluation > Destination Configuration > Audience Activation > Monitoring

## ユースケースの概要

B2B マーケティング部門は、個人レベルではなく、アカウントレベルでオーディエンスをターゲティングし、活性化する必要があります。 ターゲティングの単位が単一の消費者プロファイルであるB2C オーディエンスのアクティベーションとは異なり、B2B オーディエンスのアクティベーションには、人物と所属するアカウントの関係を把握し、アカウントレベルの属性と人物レベルのエンゲージメントシグナルを組み合わせてオーディエンスメンバーシップを評価し、アカウントベースのターゲティングをサポートする配信先にオーディエンスを配信する必要があります。

[!DNL RT-CDP] B2B editionは、アカウント、オポチュニティ、キャンペーンに特化したXDM クラスと、個人とアカウントの関係をマッピングするB2B ID解決を含む標準[!DNL Real-Time Customer Data Platform]を拡張します。 これによりマーケターは、アカウントに関連する人々の企業特性データ（業界、収益、従業員数）、技術特性データ（テクノロジースタック、製品の使用状況）、行動データ（web訪問、メールエンゲージメント、イベントへの参加）を組み合わせたアカウントオーディエンスを構築することができます。

アクティブ化されたアカウントオーディエンスは、需要創出funnelのユースケースを強化します。[!DNL LinkedIn]のfunnel上部の認知キャンペーン、ディスプレイ広告、[!DNL Marketo Engage]のfunnel中央のナーチャリングプログラム、CRM統合によるfunnel下部のセールスイネーブルメントです。 アカウント抑制オーディエンスは、既存顧客、クローズドまたはアクティブな販売サイクルにあるアカウントを除外することで、支出の無駄を防ぎます。

>[!NOTE]
>ユースケースで、アカウントレベルではなく個人レベル（B2C）でオーディエンスをアクティブ化する場合は、[宛先へのオーディエンスアクティベーション ](../audience-building-activation/audience-activation-to-destinations.md)を参照してください。 このパターンでは、標準のRT-CDP データモデルが使用され、B2B editionは必要ありません。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

### リードジェネレーションの促進

フォーム、イベント、コンテンツ、マルチチャネルエンゲージメントを通じて、セールスパイプラインの質の高いリードをより多く生み出します。

**KPI:**&#x200B;見込み顧客、リード単価、リードコンバージョン

[リードジェネレーションの強化について詳しく見る](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)

### リードのクオリフィケーションとコンバージョンを向上

スコアリング、育成、パーソナライズされたフォローアップにより、リードの品質を向上させ、パイプラインの進行を加速させることができます。

**KPI:** リードのコンバージョン、見込み顧客/リードのコンバージョン、効率性

[リードのクオリフィケーションとコンバージョンの改善について詳しく見る](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

### 新規顧客の獲得

ターゲットを絞った獲得キャンペーン、類似オーディエンス、有料メディアの最適化により、顧客基盤を拡大できます。

**KPI:**&#x200B;新規顧客、顧客獲得コスト、見込み顧客/リードコンバージョン

[新規顧客の獲得についてさらに詳しく](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### マーケティングの支出とROIの最適化

ターゲティング、アトリビューション、オーディエンスの抑制、予算配分の改善を通じて、マーケティングのROIを向上できます。

**KPI:** コスト削減、顧客獲得コスト、増分収益

[マーケティング費用とROIの最適化について詳しく見る](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## 戦術的なユースケース

次のシナリオは、このパターンを実際にどのように適用できるかを示しています。

- **アカウントベースの広告[!DNL LinkedIn]** — [!DNL RT-CDP] B2B editionからアクティブ化されたアカウントリストを使用して、理想的な顧客プロファイル（ICP）とスポンサーコンテンツおよび[!DNL LinkedIn]のInMail キャンペーンを一致させるターゲットアカウント
- **[!DNL Marketo Engage]ナーチャリングプログラムのターゲティング** — アカウントレベルのクオリフィケーション基準に基づいて、関連するリードと連絡先をターゲットナーチャリングストリームに登録するために、[!DNL Marketo Engage]にアカウントオーディエンスをアクティブ化します
- **CRM アカウントリストの同期** – 営業チームの可視化、担当地域の割り当て、アウトバウンドの見込み顧客ワークフローのために、適格アカウントリストを[!DNL Salesforce]または[!DNL Microsoft Dynamics]にプッシュします
- **有料メディアのアカウント抑制** – 有料獲得キャンペーンから既存の顧客、契約成立したアカウント、またはアクティブな販売サイクルのアカウントを抑制して、無駄な支出を削減します
- **インテントベースのアカウントターゲティング** — サードパーティのインテントシグナルとアカウントレベルでのファーストパーティのエンゲージメントデータを組み合わせて、市場内アカウントのオーディエンスを特定し、アクティブ化します
- **製品の既存アカウントへのクロスセル** – ある製品ラインを使用してアカウントのオーディエンスを構築するが、別の製品ラインを使用しない場合は、クロスセルキャンペーン用にメールおよび広告チャネルに対してアクティブ化する
- **イベントおよびウェビナーのターゲティング** – 広告およびメールチャネルにアカウントオーディエンスをアクティベートして、ターゲットアカウントからのイベント登録を促進します
- **競合他社への乗り換えキャンペーン** – 広告およびメールチャネルを通じて有効化された、カスタマイズされたメッセージを含む競合他社製品を使用してアカウントをターゲットにする
- **階層化されたアカウントエンゲージメント** – 集約された個人レベルのアクティビティに基づいてアカウントをエンゲージメント層（高、中、低）にセグメント化し、各層で差別化されたキャンペーンをアクティブ化します
- **パートナー共同マーケティングオーディエンス** — アカウントオーディエンスセグメントをチャネルパートナーまたはクラウドストレージの宛先を通じた共同マーケティングプログラムと共有します

## 主要業績評価指標

次のKPIは、このユースケースパターンの成功を測定するのに役立ちます。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| アカウントリーチ | アクティベーションチャネルをまたいでリーチしたターゲットアカウントの数 | 宛先ごとにアクティブ化されたユニークアカウントの追跡 |
| アカウントエンゲージメント率 | エンゲージメントシグナルを示すアクティブなアカウントの割合 | アカウントに集約された個人レベルのエンゲージメントを測定 |
| パイプラインへの影響 | アカウントベースのアクティベーション施策による収益パイプライン | アクティブなアカウントオーディエンスから作成された商談の追跡 |
| エンゲージメントアカウントあたりのコスト | マーケティング費用を、エンゲージメントを示しているアカウント数で割った値 | 広告とメールチャネルのコストを計算 |
| リードコンバージョン率 | アクティベートされたアカウントから商談にコンバージョンするリードの割合 | アクティブなオーディエンスに対するリードから商談へのコンバージョンを追跡 |
| オーディエンス抑制の削減 | 有料キャンペーンから対象外のアカウントを除外することでコストを削減 | 抑制オーディエンスからの支出削減を測定する |
| アカウントのカバー範囲 | アクティブなオーディエンスがカバーするTAM （Total Addressable Market）の割合 | アクティブ化されたアカウントとICP全体のユニバースを比較 |

## アプリケーション

このユースケースパターンを実装するには、次のアプリケーションを使用します。

- **[!DNL Real-Time CDP]B2B edition** — アカウントプロファイルの統合、B2B ID解決、アカウントオーディエンスの評価、B2B固有の宛先設定、アカウントオーディエンスのアクティベーションのためのコアプラットフォーム
- **[!DNL Adobe Experience Platform]（AEP）** — B2B XDM データモデリング、CRMおよびマーケティングオートメーションソースからのデータ取り込み、ID サービス、ガバナンスのための基盤インフラストラクチャ
- **[!DNL Marketo Engage]** – アクティブなアカウントオーディエンスによって提供される、リードナーチャリングプログラム、スコアリング、キャンペーン実行のプライマリB2B マーケティングオートメーションの宛先

## 関連ドキュメント

次のリソースでは、このユースケースパターンで使用される機能に関する追加のコンテキストと詳細なガイダンスを提供します。

**[!DNL RT-CDP]B2B edition**

- [Real-Time CDP B2B editionの概要](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b)
- [Real-Time CDPのB2B スキーマ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [アカウントオーディエンス](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [RT-CDP B2B edition製品の説明](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

**オーディエンスの評価とセグメント化**

- [セグメント サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [オーディエンス構成](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [セグメント化のガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

**宛先とアクティブ化**

- [宛先の概要](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [宛先カタログ](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Marketo Engageの宛先](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [LinkedIn Matched Audiencesの宛先](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)
- [Salesforce CRMの宛先](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Microsoft Dynamics 365の宛先](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/microsoft-dynamics-365)
- [Amazon S3の宛先](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)
- [ストリーミング配信先でオーディエンスを活用](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [バッチ配信先でオーディエンスを活用](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [アクティベーションガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

**データソースとコネクタ**

- [ソースの概要](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Marketo Engage コネクタ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Salesforce コネクタ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/crm/salesforce)

**データモデリングとID**

- [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [プロファイルの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

**データガバナンスとプライバシー**

- [データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [データ使用状況ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview)
- [同意と環境設定](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**監視と監視**

- [アラートの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [宛先データフローの監視](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)
- [ソースデータフローの監視](https://experienceleague.adobe.com/en/docs/experience-platform/sources/api-tutorials/monitor)
- [ライセンス使用状況ダッシュボード](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**レポートと分析**

- [CJAの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [接続の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [データビューの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)

**チュートリアルとガイド**

- [Real-Time CDP B2B editionの導入方法](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro)
- [B2B ソースのスキーマの作成](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [サンドボックスツール](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/overview)
