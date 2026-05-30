---
title: Audience Collaboration
description: Segment Matchを使用して、サンドボックスや組織間でオーディエンスセグメントを共有し、一致させる方法を説明します。
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: 7014849c-5e32-4ec3-a531-c0e8ce896f44
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 3%

---

# Audience Collaboration

このガイドでは、[!DNL Real-Time CDP]と[!DNL Adobe Experience Platform]の[!DNL Segment Match]を使用して、プライバシーが保護された方法でサンドボックスまたは組織間でオーディエンスセグメントを共有および一致させる、オーディエンスコラボレーションのユースケースパターンについて説明します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

[!DNL Segment Match]では、基礎となるPIIを公開せずにセグメントメンバーシップ情報を共有することで、2つ以上の[!DNL Experience Platform]組織（または組織内のサンドボックス）がオーディエンスデータで共同作業を行うことができます。 参加者は、重複を推定し、オーディエンスを共有し、一致したプロファイルを下流の宛先にアクティベートできます。

## ユースケースパターン

このユースケースは、Audience Collaboration パターンに従います。

[!DNL Segment Match]を使用して、サンドボックスまたは組織間でオーディエンスセグメントを共有し、一致させます。

**実行プラン：** セグメント選択/設定の一致/重複の見積もり/オーディエンスの共有/アクティベーション

## ユースケースの概要

企業は、厳格なプライバシー管理を維持しながら、パートナー企業、子会社、事業部門をまたいで、オーディエンスデータを連携する必要に迫られています。 Audience Collaborationは、ハッシュ化されたプライバシー保護された識別子を使用して、2つ以上の[!DNL Experience Platform]組織（またはサンドボックス）がオーディエンスメンバーシップ情報を交換できるようにする[!DNL Real-Time CDP]内の機能である[!DNL Segment Match]を通じて、安全なセグメント共有を有効にすることで、このニーズに対応します。

通常、ビジネスシナリオには、価値のあるオーディエンスセグメントを構築し、それをパートナー組織（受信者）と共有して、共同でターゲティング、抑制、強化する必要がある組織（送信者）が含まれます。 共有する前に、両者はオーディエンスの重複を推定して価値を評価できます。 共有が完了すると、受信組織は、一致したオーディエンスを独自の宛先を通じてアクティブ化できます。

このパターンは、外部の広告やマーケティングの宛先ではなく、組織やサンドボックス間で運用されるため、標準的なオーディエンスのアクティベーションとは異なります。 また、データクリーンルームやサードパーティのコラボレーションプラットフォームとも異なります。これは、[!DNL Experience Platform]ID インフラストラクチャを使用して、Adobe エコシステム内でネイティブに動作するからです。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

### 新規顧客の獲得

ターゲットを絞った獲得キャンペーン、類似オーディエンス、有料メディアの最適化により、顧客基盤を拡大できます。 オーディエンスのコラボレーションにより、セグメントをパートナーオーディエンスに照合し、価値の高い重複を特定して、共同アクティベーションを通じて新規顧客にリーチすることで、新しい見込み客プールを発見することができます。

- **KPI:**&#x200B;新規顧客、顧客獲得コスト、見込み顧客/リードコンバージョン
- [新規顧客の獲得](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### 顧客獲得コストの削減

ターゲティング効率を改善し、獲得キャンペーンから既存顧客を除外し、メディア支出を最適化します。 組織や事業部門をまたいで抑制セグメントを共有することで、既にコンバージョンした顧客に費やす無駄を省き、真に新しい見込み客に予算を集中させることができます。

- **KPI:**&#x200B;顧客獲得コスト、リード単価、効率性
- [顧客獲得コストの削減](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)

### マーケティングの支出とROIの最適化

ターゲティング、アトリビューション、オーディエンスの抑制、予算配分の改善を通じて、マーケティングのROIを向上できます。 [!DNL Segment Match]を使用すると、組織をまたいだオーディエンスの抑制と共同ターゲティングが可能になり、重複を減らし、精度が向上します。

- **KPI:** コスト削減、顧客獲得コスト、増分収益
- [マーケティングの支出とROIの最適化](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## 戦術的なユースケース

- **パブリッシャーと広告主のオーディエンスマッチング** – 企業は、価値の高い顧客セグメントをメディアパブリッシャーと共有して、重複を推定し、パーソナライズされた広告でマッチングされたユーザーをターゲティングすることで、PIIを公開することなくキャンペーンの関連性を向上させます。
- **持ち株会社内のクロスブランド抑制** – 親の組織の下の複数のブランドが顧客セグメントを共有し、姉妹ブランドの既存顧客を獲得キャンペーンから除外して、無駄な広告費を削減します。
- **小売メディアネットワークのオーディエンスの強化** — retailerは、CPG ブランドパートナーと購入ベースのセグメントを共有し、retailerのメディアネットワークで実績のある購入者をより高いコンバージョン率でターゲティングできるようにします。
- **共同マーケティングパートナーのオーディエンスの発見** – 競合しない2つのブランドが、共同キャンペーンを開始する前にパートナーシップの可能性を評価するためにオーディエンスの重複を評価し、重複の見積もりを使用してオーディエンスの整合性を検証します。
- **データ協同組合セグメント共有** - データ協同組合の組織は、プライバシーのコンプライアンスとデータガバナンス管理を維持しながら、ターゲティングリーチを拡大するために、ハッシュ化されたオーディエンスセグメントを共有します。
- **マルチサンドボックスオーディエンスフェデレーション**：グローバル企業が地域のサンドボックスをまたいでオーディエンスセグメントを共有し、地域のデータレジデンシー要件を尊重しながら、市場全体で一貫した顧客ターゲティングを可能にします。
- **ロイヤルティプログラム クロスパートナーのアクティベーション** – ロイヤルティ連合は、参加している加盟店とロイヤルティ階層セグメントを共有し、各パートナーが共有している顧客基盤に対して階層別のプロモーションを提供できるようにします。
- **測定とアトリビューションのコラボレーション** – 広告主がメディアパートナーとコンバージョンセグメントを共有することで、パートナーは公開されたユーザーとコンバーターを照合してキャンペーンの効果を測定できます。

## 主要業績評価指標

次のKPIは、オーディエンスコラボレーションの導入の成功を測定するのに役立ちます。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| オーディエンス重複率 | 送信者と受信者の間で一致する共有セグメント内のプロファイルの割合 | [!DNL Segment Match]重複見積もりレポート |
| 一致するオーディエンスサイズ | 正常に一致し、アクティブ化に使用できるプロファイルの数 | [!DNL Segment Match]共有ステータスとオーディエンス母集団数 |
| 一致するオーディエンスからの新規顧客獲得 | 一致するセグメントをターゲットにしたキャンペーンを通じて獲得した新規顧客 | 一致したオーディエンスを使用したキャンペーンのコンバージョン追跡 |
| 顧客獲得コストの削減 | 一致するオーディエンスを使用する場合の顧客獲得単価の削減と、広範なターゲティング | 一致したオーディエンスと一致していないオーディエンスのパフォーマンスを比較するキャンペーンコスト分析 |
| 抑制の削減 | 獲得施策で既知の顧客を除外することで、メディア費用を節約 | 抑制メディア費用の前後の比較 |
| キャンペーンのパフォーマンス向上 | 一致したオーディエンスを使用したキャンペーンのコンバージョン率、クリック率、エンゲージメントの向上 | A/B テストと一致したオーディエンス施策と対照の比較 |
| Collaborationまでの時間 | セグメント共有の開始からアクティベーションの準備までの経過時間 | [!DNL Segment Match] ワークフローのタイムスタンプ |

## アプリケーション

このユースケースパターンでは、次のアプリケーションを使用します。

- **[!DNL Real-Time CDP]** — プライバシー保護されたオーディエンスの共有、セグメント作成のためのオーディエンス評価、一致したオーディエンスの下流での使用のための宛先アクティベーションのための[!DNL Segment Match]機能を提供します。
- **[!DNL Adobe Experience Platform]** — [!DNL Segment Match]が依存するID解決、プロファイル統合、データガバナンス、同意の適用など、基盤となるデータ基盤を提供します。

## 関連ドキュメント

次のリソースでは、このユースケースパターンで使用される機能に関する追加の詳細を示します。

### [!DNL Segment Match]

- [セグメントマッチの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)
- [セグメントマッチのトラブルシューティング](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/troubleshooting)

### セグメンテーションとオーディエンス

- [セグメント サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [オーディエンス構成の概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language リファレンス](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [エッジセグメント化](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### IDとプロファイル

- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID名前空間の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/namespaces)
- [結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [リアルタイム顧客プロファイルの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### データガバナンスと同意

- [データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [データ使用状況ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview)
- [ポリシーの適用](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview)
- [同意と環境設定](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [同意と環境設定のフィールドグループ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)

### 配信先とアクティベーション

- [宛先の概要](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [宛先カタログ](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [宛先のデータフローの監視](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)

### データモデリングとスキーマ

- [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [スキーマ構成の基本](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

### 管理とアクセス制御

- [アクセス制御の概要](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home)
- [サンドボックスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/sandbox/home)

### 監視と監視

- [アラートの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Observability Insightsの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)

### ガードレール

- [リアルタイムの顧客プロファイルのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [セグメント化のガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- [アクティベーションガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

### チュートリアル

- [スキーマを作成](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/union-schema)
- [プロファイルのデータセットを有効にする](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/enable-for-profile)
