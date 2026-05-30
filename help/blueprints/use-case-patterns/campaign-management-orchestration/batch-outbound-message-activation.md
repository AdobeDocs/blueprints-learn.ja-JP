---
title: バッチ送信メッセージの有効化
description: 1回のバッチ実行でオーディエンスを評価し、スケジュールされたアウトバウンドメッセージを配信する方法を説明します。
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 192853ce-02ab-46e6-9092-3db5354bc19c
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 4%

---

# バッチアウトバウンドメッセージのアクティベーション

このガイドでは、[!DNL Adobe Journey Optimizer] （AJO）と[!DNL Adobe Real-Time Customer Data Platform] （RT-CDP）を使用して、スケジュールされたアウトバウンドメッセージを定義されたオーディエンスセグメントに配信する、バッチアウトバウンドメッセージのアクティベーションのユースケースパターンについて説明します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

バッチアウトバウンドメッセージのアクティベーションは、一対多のアウトバウンドメッセージの基本的なキャンペーンパターンです。 オーディエンスの定義からメッセージの配信、パフォーマンス分析に至るまで、ライフサイクル全体をカバーしています。

## ユースケースパターン

**バッチアウトバウンドメッセージのアクティベーション**

オーディエンスを評価し、スケジュールされたアウトバウンドメッセージ（電子メール、SMS、プッシュ通知）を、あらゆる適格プロファイルに一度に配信します。

**実行計画：** オーディエンス評価/ メッセージ作成/ キャンペーン実行/ レポート

## ユースケースの概要

企業は、多くの場合、特定の時点やシステムイベントへの反応として、既知のオーディエンスセグメントに単一のメッセージを配信する必要があります。 このパターンは、[!DNL RT-CDP]のオーディエンス評価と[!DNL Journey Optimizer]のメッセージのオーサリングおよびキャンペーン実行を組み合わせることで、この要件に対応します。

メッセージを受け取るユーザーを定義し、パーソナライズされたメッセージのコンテンツを制作し、オーディエンスとメッセージをキャンペーンやジャーニーにバインドし、スケジュールに従って、オーディエンスの選定を介して、またはシステムトリガーを介して送信します。 その結果、配信、エンゲージメント、コンバージョンに関する指標に関する詳細なレポートを活用して、メッセージを配信できます。

このパターンは、単一のメッセージを既知のオーディエンスに1回の実行で配信することで、ビジネス目標を前進させることができるたびに適用されます。 リアルタイムの行動イベントに対応するイベントトリガーメッセージや、プロファイルを複数の顧客接点に時系列で誘導するマルチステップのオーケストレーションされたジャーニーとは異なります。 バッチアクティベーションは、最もシンプルなキャンペーンパターンであり、アウトバウンドメッセージのユースケースの最も一般的な出発点です。

## 主なビジネス目標

このセクションでは、バッチアウトバウンドメッセージのアクティベーションがサポートする主要なビジネス目標を特定します。

### メールとキャンペーンのエンゲージメントを増やす

**説明：**&#x200B;最適化されたコンテンツとターゲティングにより、開封率、クリックスルー率、キャンペーン全体の反応を向上させます。

**KPI:**&#x200B;開封率、エンゲージメント、コンバージョン率

### 売上と売上の増加

**説明：**&#x200B;最適化されたデジタルチャネル、キャンペーン、カスタマージャーニーを通じて、売上の増加を促進します。

**KPI:** コンバージョン率、増分収益、平均注文額

**関連するビジネス目標：** [売上と売上の増加](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

### キャンペーン実行の合理化

**説明：** テンプレート、自動化、標準化されたプロセスを通じて、キャンペーンの構築時間を短縮し、マルチチャネルキャンペーンの配信を簡素化します。

**KPI:**&#x200B;市場投入までのスピード、効率性、時間内の完了%

## 戦術的なユースケース

次のシナリオは、バッチアウトバウンドメッセージのアクティベーションの一般的なアプリケーションを示しています。

- **セールのお知らせまたはプロモーションメールの送信** – 予定日に、対象となる顧客のセグメントにプロモーションオファーを配信します
- **製品発売のプッシュ通知** — プッシュ通知を使用して、新製品の在庫状況を興味を持っている顧客に通知します
- **ニュースレターまたはダイジェストの電子メール** – 購読者オーディエンスにコンテンツを定期的に提供します
- **イベント登録招待** – 適格な見込み客をウェビナー、会議、対面イベントに招待します
- **サブスクリプションの更新に関するリマインダーメール** – 更新日に近づいているお客様にアクションを実行するように通知します
- **ロイヤルティプログラムのマイルストーン通知** — ロイヤルティ階層またはポイントしきい値に達したメンバーに感謝します
- **特定のcall-to-action電子メール** – 購入の完了、環境設定の更新、プログラムへの登録など、ターゲットを絞ったアクションを実行します
- **フラッシュセールまたは期間限定オファーのSMS キャンペーン** — オプトインしたオーディエンスに対して、SMSを介して緊急の期限付きプロモーションを送信します

## 主要業績評価指標

次の表は、キャンペーンの効果を測定するために使用されるKPIを定義しています。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| 配信率 | 受信者に正常に配信されたメッセージの割合 | 配信済み/送信済み×100 |
| 開封率 | 受信者が開封した配信メッセージの割合 | ユニーク開封数/配信数×100 |
| CTR （クリックスルー率） | リンクがクリックされた配信メッセージの割合 | ユニーククリック数/配信数×100 |
| CTOR （クリック率） | リンクがクリックされた開封メッセージの割合 | ユニーククリック数/ユニーク開封数×100 |
| コンバージョン率 | 目的のアクションを完了した受信者の割合 | コンバージョン数/配信数×100 |
| 登録解除率 | メッセージを受信した後に登録解除した受信者の割合 | 登録解除/配信数×100 |
| バウンス率 | 配信できなかったメッセージの割合 | バウンス / 送信済みx 100 |
| メール送信あたりの売上高 | キャンペーンに起因する売上を、送信されたメッセージで割った割合 | 総収益/送信済み |

## アプリケーション

このパターンを実装するには、次のアプリケーションを使用します。

- **[!DNL Adobe Journey Optimizer]（AJO）** — メッセージのオーサリング、チャネル設定、キャンペーンの実行、ジャーニーオーケストレーション、コンテンツの実験、頻度ルール、レポート
- **[!DNL Adobe Real-Time Customer Data Platform]（RT-CDP）** — オーディエンスの評価、同意、およびガバナンスの適用
- **[!DNL Adobe Experience Platform]（AEP）** — プロファイルストア、ID サービス、スキーマ、データセット、データ収集

## 関連ドキュメント

このセクションでは、トピック別に整理された[!DNL Experience League] ドキュメントへの包括的なリンクを提供します。

### キャンペーン

- [キャンペーンの基本を学ぶ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [キャンペーンの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [API トリガーによるキャンペーン](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)

### ジャーニー

- [ジャーニーの基本を学ぶ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [オーディエンスジャーニーを読む](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)

### チャネル設定

- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [サブドメインをデリゲート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP プールの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [IP ウォームアッププラン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [メールサーフェス設定](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [SMS チャネルの設定](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [プッシュ通知チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [抑制リストの管理](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### メッセージのオーサリングとパーソナライゼーション

- [メールの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/create-email)
- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [メールDesignerコンテンツコンポーネントの使用](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [メールコンテンツのインポートまたはコーディング](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/code-content)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalizationの構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [ヘルパー関数](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)

### コンテンツ管理

- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [コンテンツフラグメントの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [コンテンツのプレビューとテスト](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [メール校正を送信](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/preview-test/proofs)
- [メールのレンダリング](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/email-rendering)

### コンテンツの検証

- [コンテンツ実験を始める](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [コンテンツ実験を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [コンテンツ実験レポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [統計計算](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### 頻度と競合管理

- [頻度ルール](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [ビジネスルールの概要](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [競合と優先順位管理を開始する](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [優先スコア](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [潜在的な競合の特定](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [ジャーニーの上限と調停](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### オーディエンスとセグメンテーション

- [セグメント サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/segment-builder)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [エッジセグメント化](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/methods/edge-segmentation)
- [オーディエンス構成](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language リファレンス](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/pql/overview)

### レポート

- [キャンペーンのライブレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [キャンペーングローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [ジャーニーライブレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [AJO + CJA統合ガイド](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### データガバナンスと同意

- [データガバナンスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/home)
- [データ使用状況ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview)
- [同意と環境設定のフィールドグループ](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/field-groups/profile/consents)
- [Journey Optimizerでの同意](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### データモデリングとID

- [XDM システムの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/home)
- [スキーマ構成の基本](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/schema/composition)
- [ID サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/home)
- [結合ポリシーの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/merge-policies/overview)

### ガードレール

- [Journey Optimizerのガードレール](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/guardrails)
- [リアルタイムの顧客プロファイルのガードレール](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/guardrails)
- [取り込みのガードレール](https://experienceleague.adobe.com/ja/docs/experience-platform/ingestion/guardrails)

### チュートリアルと基本を学ぶ

- [Journey Optimizerの導入方法](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/get-started)
- [最初のキャンペーンを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [最初のジャーニーを作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/orchestrate-journeys/journey)
