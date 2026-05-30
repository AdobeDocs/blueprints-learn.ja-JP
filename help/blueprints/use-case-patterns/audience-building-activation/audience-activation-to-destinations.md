---
title: 配信先でのオーディエンスの活用
description: Adobe Real-Time CDPを使用して、ターゲティングまたは抑制のためにオーディエンスセグメントを評価し、外部の宛先に公開する方法を説明します。
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: b0b9d937-45d2-48f9-ac4c-3611c6e35f58
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 4%

---

# 配信先でのオーディエンスの活用

このガイドでは、Adobe [!DNL Real-Time Customer Data Platform] （RT-CDP）のオーディエンスセグメントを評価し、ターゲティング、抑制、類似モデリング、分析の強化のために、アドプラットフォーム、クラウドストレージ、CRM システム、データパートナーに公開する宛先へのオーディエンスアクティベーションのユースケースパターンについて説明します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

このパターンは、オーディエンスのアクティベーションのライフサイクル全体をカバーしています。オーディエンスセグメントの定義と評価から、宛先接続の設定とオーディエンスの公開、アクティベーションの健全性の監視、ガバナンスコンプライアンスの適用に至るまで、あらゆるものをカバーしています。

## ユースケースパターン

**Audience Activationから宛先** — ターゲティングまたは抑制のために、オーディエンスセグメントを評価して外部の宛先に公開します。

**実行計画：** オーディエンス評価/宛先設定/ Audience Activation > モニタリング

## ユースケースの概要

企業は、有料メディアキャンペーンの実施、CRM レコードの拡充、パートナーとのデータ共有、下流プロセスでの分析の実行などを目的として、オーディエンスデータを外部システムに配信する必要があります。 Audience Activation to Destinationsは、RT-CDPの基本的なアクティベーションパターンです。ターゲットオーディエンスに適格なプロファイルを評価し、1つ以上の外部宛先に接続し、プロファイル属性を宛先固有のフィールドにマッピングし、ダウンストリームでの使用のためにオーディエンスを公開します。

このパターンは、オーディエンスデータを適切な形式の外部システムに的確なタイミングで取得することが目標である場合に適用されます。 メッセージの配信、オンサイトでのパーソナライゼーション、分析は含まれていません。 これは、RT-CDP実装の最も一般的な出発点であり、他のパターンがその上に構成するビルディングブロックとして機能します。

典型的な関係者には、有料メディアを管理するデジタルマーケティングチーム、データチームによるデータウェアハウスの強化、キャンペーンのコンタクトリストの準備、アウトバウンドデータフローのガバナンスコンプライアンスを確保するプライバシーチームなどがあります。

>[!NOTE]
>組織で[!DNL Real-Time CDP] B2B editionを使用し、アカウントベースの宛先に対してアクティブ化している場合は、[B2B オーディエンスのアクティブ化](../b2b/account-audience-activation.md)を参照してください。 このパターンは、同じアクティベーションの仕組みを共有していますが、B2B企業の対面データモデルを使用しており、B2B edition ライセンスが必要です。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

### 新規顧客の獲得

ターゲットを絞った獲得キャンペーン、類似オーディエンス、有料メディアの最適化により、顧客基盤を拡大できます。

**KPI:**&#x200B;新規顧客、顧客獲得コスト、見込み顧客/リードコンバージョン

[新規顧客の獲得についてさらに詳しく](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### 顧客獲得コストの削減

ターゲティング効率を改善し、獲得キャンペーンから既存顧客を除外し、メディア支出を最適化します。

**KPI:**&#x200B;顧客獲得コスト、リード単価、効率性

[顧客獲得コストの削減について詳しく見る](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)

### マーケティングの支出とROIの最適化

ターゲティング、アトリビューション、オーディエンスの抑制、予算配分の改善を通じて、マーケティングのROIを向上できます。

**KPI:** コスト削減、顧客獲得コスト、増分収益

[関連トピックス](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## 戦術的なユースケース

- **広告プラットフォームオーディエンスターゲティング** — キャンペーンのターゲティング用に有料メディアプラットフォームに適格セグメントをプッシュします
- **既存顧客に対する有料メディアの抑制** – 広告プラットフォームでの獲得キャンペーンから既知の顧客を除外して、無駄な支出を排除します
- **類似シードオーディエンス** – 類似オーディエンスを拡張するためのシードオーディエンスとして、価値の高い顧客セグメントをFacebook、Google Ads、The Trade Deskにプッシュします
- セールス支援のための&#x200B;**CRM同期** – 購買意欲の高いオーディエンスや価値の高いオーディエンスをアクティベートして、セールス部門がアウトリーチを優先できるようにします
- **データパートナーのオーディエンス共有** – 協力ターゲティングまたは測定のために、データパートナーと適格なオーディエンスセグメントを共有します
- **データウェアハウスのエンリッチメント用のクラウドストレージの書き出し** — オーディエンスメンバーシップとプロファイル属性をAmazon S3、Azure Blob、Google Cloud StorageまたはSFTPに書き出して、ダウンストリーム分析に使用します
- **リターゲティングオーディエンスのアクティベーション** — リターゲティングプラットフォームにコンバージョンしなかったサイト訪問者をアクティベート
- **連絡先リストをメールサービスプロバイダーに同期** – 調整されたアウトリーチのために、オーディエンスメンバーシップをサードパーティのメールプラットフォームにプッシュします

## 主要業績評価指標

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| 顧客獲得コスト（CAC） | アクティベートされたオーディエンスを通じて新規顧客を獲得するコスト | 総メディア費用/アクティベートされたオーディエンスに起因する新規顧客 |
| Audience Match Rate | 宛先で正常に一致したアクティブ化されたプロファイルの割合 | 宛先で一致したプロファイル / RT-CDPから書き出されたプロファイル |
| 抑制の削減 | 既存顧客を獲得キャンペーンから除外することで、メディア費用を回避 | 推定CPM x抑制オーディエンスサイズ |
| アクティベーションの配信率 | 宛先に正常に配信されたプロファイルの割合 | 配信されたプロファイル / ソースオーディエンス内のプロファイル |
| アクティベーションにかかる時間 | オーディエンス定義から宛先での初回配信までの経過時間 | セグメントの作成から最初に確認したデータフローの実行まで測定したい |
| オーディエンス母集団の精度 | 配信先での予想オーディエンスサイズと実際のオーディエンスサイズの調整 | 配信先のオーディエンスサイズ/RT-CDPのオーディエンスサイズ |

## アプリケーション

- **Adobe [!DNL Real-Time Customer Data Platform] （RT-CDP）** — オーディエンスの評価、宛先管理、オーディエンスのアクティブ化、同意およびガバナンスの適用
- **Adobe [!DNL Experience Platform] （AEP）** — プロファイルストア、ID サービス、セグメンテーションエンジン、データガバナンス

## アーキテクチャ

次のリファレンスアーキテクチャでは、Real-Time CDPから、クラウドストレージ、ストリーミングエンドポイント、SaaS アプリケーションなどのエンタープライズ宛先に、オーディエンスとプロファイルデータがどのように流れるのかを示しています。

![ エンタープライズ宛先に対するオーディエンスとプロファイルのアクティブ化のための参照アーキテクチャ ](/help/blueprints/audience-activation/assets/known_activation.png)

## 関連ドキュメント

**宛先**

- [宛先の概要](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [宛先カタログ](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [ストリーミング配信先でオーディエンスを活用](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [バッチプロファイル書き出し宛先へのオーディエンスのアクティベート](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [バッチ配信先でオンデマンドでオーディエンスを活用](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/api/ad-hoc-activation-api)
- [宛先のガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
- [Destination SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/overview)

**オーディエンスとセグメント化**

- [セグメント サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Profile Query Language リファレンス](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [エッジセグメント化](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [オーディエンス構成の概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [セグメント化のガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

**IDとプロファイル**

- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID名前空間の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/namespaces)
- [ID グラフのリンクルール](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [プロファイルの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

**データモデリングとスキーマ**

- [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [スキーマ構成の基本](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

**データガバナンス**

- [データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [データ使用状況ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview)
- [データガバナンスポリシー](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/policies/overview)
- [ポリシーの適用](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview)
- [同意と環境設定](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**監視と監視**

- [宛先のデータフローの監視](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)
- [アラートの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Observability Insightsの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
- [ライセンス使用状況ダッシュボード](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**計算属性**

- [計算属性の概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [計算属性UI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)

**データの収集とソース**

- [ソースの概要](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Web SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [データストリームの設定](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)

**管理**

- [サンドボックスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/sandbox/home)
- [アクセス制御の概要](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home)
- [属性ベースのアクセス制御](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/abac/overview)

**ガードレール**

- [リアルタイムの顧客プロファイルのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [ID サービスのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
- [アクティベーションガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
- [取り込みのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
