---
title: 複数ステップの調整されたジャーニー
description: 待機時間、条件、複数のメッセージアクションを伴う分岐、マルチタッチジャーニーを通じてプロファイルを導く方法を説明します。
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 5667b188-1b20-4a85-aebb-74efd5f771a1
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1798'
ht-degree: 5%

---

# マルチステップのオーケストレーションジャーニー

このガイドでは、[!DNL Adobe Journey Optimizer] （AJO）と[!DNL Real-Time Customer Data Platform] （RT-CDP）を使用して、複数のメッセージを経時的に配信する分岐マルチタッチ カスタマージャーニーを調整する、マルチステップのオーケストレーションされたジャーニーのユースケースパターンについて説明します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

## ユースケースパターン

**複数ステップの調整されたジャーニー**

待機、条件、複数のメッセージアクションを経時的に使用する分岐マルチタッチジャーニーを通じてプロファイルを導きます。

**実行プラン：** オーディエンスの評価/ジャーニー実行（マルチノード）/条件分岐/メッセージ配信（xN）/離脱条件/レポート

## ユースケースの概要

マルチステップのオーケストレーションされたジャーニーは、単一のメッセージでは顧客が望む結果を得るのに不十分なビジネスシナリオに対処します。 このジャーニーでは、1回限りの送信ではなく、プロファイル属性、行動シグナル、イベントデータにもとづいてパスを適応させる分岐ロジックを使用して、電子メール、SMS メッセージ、プッシュ通知、アプリ内メッセージなどの一連の顧客接点を数日から数週間にわたって誘導します。

これらのジャーニーは、AJOの最も複雑なキャンペーンパターンです。 オーディエンスベースまたはイベントベースのエントリを、アクションノード（メッセージ）、条件ノード（分岐ロジック）、待機ノード（時間遅延）、および終了条件（コンバージョンイベントまたはタイムアウト）のキャンバスと組み合わせます。 プロファイルはジャーニーを独自のペースで進み、各ステップでコンテキストに即したコンテンツを受け取ります。

このパターンでは、単純なパターンである、単一送信キャンペーンのバッチアウトバウンドメッセージのアクティベーションと、単一イベントの応答に対するイベントトリガーメッセージを使用します。 このパターンは、ユースケースにおいて、複数のインタラクションを通じてプロファイルを育成する必要がある場合に使用します。

>[!NOTE]
>ジャーニーで最適なオファー、コンテンツ、チャネルを個別の意思決定ポイントで動的に選択する必要がある場合は、[意思決定を伴うクロスチャネルジャーニー](cross-channel-journey-with-decisioning.md)を参照してください。 このパターンは、AJO Decisioningとの統合によってこれを拡張します。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

### 顧客維持率の向上

価値主導の体験と継続的な関係育成を通じて、既存顧客との関係を維持し、更新する。

**KPI:** リテンション、顧客生涯価値、エンゲージメント

[顧客維持率の向上について詳しく見る](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)

### 顧客オンボーディングの改善

合理化され、パーソナライズされたウェルカムエクスペリエンスとアクティベーションジャーニーにより、新規顧客の価値創出までの時間を短縮できます。

**KPI:**&#x200B;のエンゲージメント、リテンション、コンバージョン率

[関連トピックス](/help/blueprints/business-objectives/customer-experience/improve-customer-onboarding.md)

### 休眠顧客のリエンゲージメント

行動シグナルにもとづいたリエンゲージメント施策を実施し、非アクティブな顧客や休眠顧客を取り戻すことができます。

**KPI:**&#x200B;のエンゲージメント、リテンション、コンバージョン率

[顧客維持率の向上について詳しく見る](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)

### 放棄されたカートとジャーニーを回復する

タイムリーでパーソナライズされたフォローアップにより、購入、申し込み、登録のフローの途中で離脱したユーザーをリエンゲージできます。

**KPI:** コンバージョン率、増収率、エンゲージメント

[放棄されたカートとジャーニーの回復について詳しく見る](/help/blueprints/business-objectives/customer-experience/recover-abandoned-carts-journeys.md)

## 戦術的なユースケース

次のシナリオは、マルチステップのオーケストレーションされたジャーニーパターンの一般的なアプリケーションを示しています。

- **顧客オンボーディングシリーズ** – ようこそ電子メール、機能教育、登録後の最初の14日間のアクティベーションプロンプト
- **再エンゲージメント ドリップキャンペーン** – リマインダーメール、インセンティブオファー、3週間にわたる休眠顧客への最終通知
- **ロイヤルティマイルストーンジャーニー** – 階層アップグレード通知、続いて限定オファー、メンバーシップの契約応当日の更新リマインダー
- **ウィンバック シーケンス** — 「お見逃ししています」電子メール、電子メールによる割引オファー、解約した購入者に対する最終的なSMS リマインダー
- **製品の導入ジャーニー** – 試用版の歓迎、使用のヒント、試用期間の進行に伴うアップグレードプロンプト
- **サブスクリプション更新シーケンス** — 30日間の通知、7日間のリマインダー、および今後のサブスクリプション更新の有効期限メッセージ
- **購入後のナーチャリング** – お礼の電子メール、使い方ガイド、クロスセルのレコメンデーション、購入後30日間にわたるレビューリクエスト

## 主要業績評価指標

次のKPIを使用して、マルチステップのオーケストレーションされたジャーニー実装の効果を測定します。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| ジャーニー完了率 | ジャーニー全体を完了し、早期終了することなく離脱したプロファイルの割合 | ジャーニーレポート：終了（完了） / 入力済 |
| ステップのコンバージョン率 | 次のステップへと進むプロファイルの割合 | ジャーニーレポートのノードごとの指標 |
| チャネルエンゲージメント率 | 各顧客接点での開封率、クリック率、応答率 | メッセージごとの配信とエンゲージメント指標 |
| 出口基準コンバージョン率 | ジャーニータイムアウト前に離脱イベント（購入、サインアップなど）をトリガーにしたプロファイルの割合 | 出口基準ヒット数/合計入力 |
| コンバージョンまでの時間 | ジャーニー開始から出口基準イベントまでの平均期間 | ジャーニー分析：エントリタイムスタンプからコンバージョンイベントタイムスタンプ |
| ジャーニー脱落率 | 各ステップでエンゲージを停止したプロファイルの割合（フォールアウト分析） | ジャーニーステップをまたいだCJAフォールアウトビジュアライゼーション |
| リテンション/リエンゲージメント率 | アクティブステータスに戻るターゲットプロファイルの割合 | CJAによるジャーニー後の行動分析 |

## アプリケーション

このユースケースパターンを実装するには、次のアプリケーションを使用します。

- **[!DNL Adobe Journey Optimizer]（AJO）** — ジャーニー オーケストレーション エンジン、メッセージ オーサリング、チャネル設定、コンテンツの実験、頻度と競合の管理、レポート
- **[!DNL Adobe Real-Time Customer Data Platform]（RT-CDP）** — ジャーニーエントリのオーディエンスのオーディエンス評価と定義、パーソナライゼーションおよび条件分岐のプロファイルデータ
- **[!DNL Adobe Experience Platform]（AEP）** — プロファイルストア、ID サービス、イベントデータ取り込み、基礎データインフラストラクチャ

## 関連ドキュメント

以下のリソースでは、この実装で使用される機能に関する追加の詳細を提供します。

### ジャーニー

- [ジャーニーの基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [ジャーニーの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [ジャーニーのプロパティ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [ジャーニーを公開](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)
- [ジャーニーをテスト](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)

### ジャーニー活動

- [オーディエンスアクティビティの読み取り](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [一般イベント](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [オーディエンスの選定イベント](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [条件アクティビティ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [「待機」アクティビティ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [ジャーニーへのメッセージの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [「終了」アクティビティ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/end-activity)
- [カスタムアクションの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions)

### 入出口管理

- [ジャーニー入力管理](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [終了条件](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)

### チャネル設定

- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [チャネルサーフェスの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [サブドメインをデリゲート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP プールの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [IP ウォームアッププラン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [SMS チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [プッシュ通知チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### メッセージのオーサリングとパーソナライゼーション

- [メールの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [メールDesignerコンテンツコンポーネントの使用](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalizationの構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [ヘルパー関数](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [コンテンツフラグメントの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [コンテンツのプレビューとテスト](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### コンテンツの検証

- [コンテンツ実験を始める](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [コンテンツ実験を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [コンテンツ実験レポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [統計計算](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### 頻度、競合、優先度

- [頻度ルール](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [ビジネスルールの概要](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [競合と優先順位管理を開始する](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [優先スコア](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [ジャーニーの上限と調停](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [潜在的な競合の特定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### オーディエンスとセグメンテーション

- [セグメント サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Profile Query Language リファレンス](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/api/streaming-segmentation)
- [エッジセグメント化](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/api/edge-segmentation)

### レポートと分析

- [ジャーニーライブレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [AJO + CJA統合ガイド](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [CJAの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)

### 同意とガバナンス

- [Journey Optimizerでの同意](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [抑制リストの管理](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### データ基盤

- [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [プロファイルの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [計算属性の概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
