---
title: イベントトリガーメッセージ
description: 行動イベントやシステムイベントに応じて、コンテキストに即したリアルタイムメッセージを配信する方法を説明します。
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 75137990-9848-40c0-abf3-adbd21d2de52
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1955'
ht-degree: 5%

---

# イベントトリガーメッセージ

このガイドでは、[!DNL Adobe Journey Optimizer] （AJO）、[!DNL Real-Time Customer Data Platform] （RT-CDP）、[!DNL Adobe Experience Platform] （AEP）を使用して、行動イベントまたはシステムイベントに応じてコンテキストに即したリアルタイムのメッセージを配信する、イベントトリガー型メッセージのユースケースパターンについて説明します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

このパターンは、イベントの取り込みから、メッセージ配信、パフォーマンスレポート作成に至るまで、ライフサイクル全体をカバーしています。

## ユースケースパターン

この節では、イベントトリガーメッセージを駆動するコアパターンと実行プランについて説明します。

**イベントトリガーメッセージ**

リアルタイムの行動イベントやシステムイベントをリッスンし、トリガープロファイルにコンテクストに即したメッセージを配信します。

**実行プラン：** イベント取り込み/ジャーニーエントリ/条件評価/メッセージ配信/レポート

## ユースケースの概要

イベントトリガーメッセージは、リアルタイムの行動イベントやシステムイベントに応じて、コンテクストに即したメッセージを配信します。 バッチ方式のアウトバウンドメッセージのアクティベーションでは、事前に評価されたオーディエンスにスケジュールどおりに送信しますが、このパターンでは、カート放棄、閲覧セッション、フォーム送信、システムステータスの変更など、条件が適用されるイベントをリッスンして、条件を評価してメッセージを配信するジャーニーにすぐにトリガープロファイルを入力します。

このパターンは、AEPへのリアルタイムのイベントストリーミング（Web SDK、モバイルSDK、サーバーサイド API経由）、AJOの単一イベントエントリを含むジャーニー、送信するかどうか、何を送信するかを決定する条件評価ロジックに依存しています。 メッセージは通常、トリガーイベントから数分以内に送信されるため、このパターンは、時間的制約があり、コンテキストに関連性の高いコミュニケーションに最適です。

企業はこのパターンを利用して、顧客の行動にリアルタイムで対応できるため、スケジュール型のバッチコミュニケーションと比較して、関連性が高まり、エンゲージメントとコンバージョン率が向上します。 一般的なシナリオには、カート放棄からの復旧、購入後のフォローアップ、登録後のウェルカムメッセージ、支払い失敗や価格低下のアラートなどの時間的制約を受ける通知などがあります。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

**[放棄されたカートとジャーニーを復元](../../business-objectives/customer-experience/recover-abandoned-carts-journeys.md)**

タイムリーでパーソナライズされたフォローアップにより、購入、申し込み、登録のフローの途中で離脱したユーザーをリエンゲージできます。

| KPI |
| --- |
| コンバージョン率、売上増加、エンゲージメント |

**[コンバージョン率を向上](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

購入、サインアップ、フォーム送信など、望ましいアクションを実行した訪問者と見込み顧客の割合を向上させます。

| KPI |
| --- |
| Cpl、Cpl、Cpl （リード単価） |

**[パーソナライズされた顧客体験の提供](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

個人の好み、行動、ライフサイクルのステージに合わせて、コンテンツ、オファー、メッセージを調整。

| KPI |
| --- |
| エンゲージメント、コンバージョン率、顧客満足度（CSAT） |

**[顧客オンボーディングの改善](../../business-objectives/customer-experience/improve-customer-onboarding.md)**

合理化され、パーソナライズされたウェルカムエクスペリエンスとアクティベーションジャーニーにより、新規顧客の価値創出までの時間を短縮できます。

| KPI |
| --- |
| エンゲージメント、リテンション、コンバージョン率 |

## 戦術的なユースケース

次のシナリオは、イベントトリガーメッセージを様々なビジネスコンテキストに適用する方法を示しています。

- **カート放棄メールまたはSMS** – 顧客がカートに商品を追加したものの、定義された時間枠内に購入を完了しなかった場合にリマインダーメッセージを送信する
- **放棄のフォローアップを参照** – 製品またはコンテンツを閲覧したものの、コンバージョンのアクションを起こさなかった訪問者をリエンゲージします
- **購入後のお礼またはクロスセル** – 購入イベントの直後に、確認とクロスセルのレコメンデーションを配信します
- **体験版の有効期限に関するリマインダー** – 更新またはコンバージョンメッセージを使用して、無料体験版の終了を迫っているユーザーに通知します
- **登録後のウェルカムメッセージ** – 新しいユーザーがアカウントを登録または作成すると、すぐにオンボーディングメッセージを送信します
- **フォーム送信確認** — コンテキスト確認を使用して、フォーム送信（問い合わせリクエスト、アプリケーション、登録）を確認します
- **支払い失敗の通知** – 定期的な支払いが失敗したときに顧客に通知し、支払い情報を更新するよう促します
- **App uninstall win-back push notification** — ユーザーがモバイルアプリケーションをアンインストールすると、win-back メッセージがトリガーされる
- **予約または予約の確認** – 予約、予約、または予約がスケジュールされた後、すぐに確認を送信します
- **ウィッシュリストに登録された商品の値下げアラート** – ウィッシュリストに登録されている商品の値下げを顧客に通知します

## 主要業績評価指標

次のKPIは、イベントをトリガーとしたメッセージ実装の効果を測定するのに役立ちます。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| コンバージョン率 | トリガーされたメッセージ受信者のうち、望ましいアクション（購入、サインアップ、更新）を完了した割合 | 配信されたコンバージョン数/メッセージ数* 100 |
| 売上増加 | イベントをトリガーとしたメッセージに起因する売上が、配信不可コントロールグループに比べて増加 | トリガーされた送信からの収益 – コントロールグループのベースライン |
| 開封率 | 受信者が開封した配信メッセージの割合 | 開封数/配信数×100 |
| CTR （クリックスルー率） | 少なくとも1回のクリックが発生した配信メッセージの割合 | クリック数/配信数×100 |
| コンバージョンまでの時間 | メッセージ配信とコンバージョンイベントまでの平均経過時間 | 平均（コンバージョンタイムスタンプ – 配信タイムスタンプ） |
| ジャーニー完了率 | ジャーニーにエントリし、メッセージ配信ステップに到達したプロファイルの割合（条件または終了によってドロップされない） | 配信に達したプロファイル / ジャーニーに入るプロファイル * 100 |
| メッセージ抑制率 | 頻度の上限、同意、条件の評価が原因で抑制された、適格プロファイルの割合 | 抑制されたプロファイル / 対象プロファイルの合計* 100 |
| バウンス率 | ハードバウンスまたはソフトバウンスのために配信できなかったメッセージの割合 | バウンス/送信済み* 100 |

## アプリケーション

このユースケースパターンでは、次のAdobe アプリケーションを使用します。

- **[!DNL Adobe Journey Optimizer]（AJO）** – 単一イベント入力、条件評価、待機手順、メッセージのオーサリング、チャネル設定、頻度ガバナンス、配信レポートを使用したジャーニーオーケストレーション
- **[!DNL Adobe Real-Time Customer Data Platform]（RT-CDP）** — ジャーニー内の条件ベースのフィルタリング、同意とガバナンスの適用、プロファイルの強化のオーディエンス評価
- **[!DNL Adobe Experience Platform]（AEP）** — Web SDK、モバイル SDK、またはサーバーサイド APIを介したリアルタイムのイベント取り込み、データモデリング、ID解決、Edge Network

## 関連ドキュメント

以下のリソースでは、この実装で使用される機能に関する追加の詳細を提供します。

### ジャーニー連携

- [ジャーニーの基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [ジャーニーの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [ジャーニーのプロパティ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [一般イベント](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [オーディエンスの選定イベント](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [条件アクティビティ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [「待機」アクティビティ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [ジャーニーへのメッセージの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [終了条件](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [ジャーニー入力管理](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [ジャーニーをテスト](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [ジャーニーを公開](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### チャネル設定

- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [サブドメインをデリゲート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP プールの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [IP ウォームアッププラン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [メールサーフェス設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [SMS チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [プッシュ通知チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [抑制リストの管理](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### メッセージのオーサリングとパーソナライゼーション

- [メールの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalizationの構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [ヘルパー関数](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [コンテンツフラグメントの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [コンテンツのプレビューとテスト](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [SMS メッセージの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [プッシュ通知のデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)

### 頻度とビジネスルール

- [頻度ルール](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [ビジネスルールの概要](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [キャップ API](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/channel-surfaces/capping)

### 対立と優先順位管理

- [競合と優先順位管理を開始する](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [潜在的な競合の特定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [優先スコア](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [ジャーニーの上限と調停](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### レポートとパフォーマンス

- [ジャーニーライブレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [AJO + CJA統合ガイド](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### データの収集と取り込み

- [Web SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [モバイル SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Edge Network Server APIの概要](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [データストリームの設定](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [ストリーミング取り込みの概要](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview)

### データモデリングとスキーマ

- [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [スキーマ構成の基本](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

### IDとプロファイル

- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID名前空間の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/namespaces)
- [ID グラフのリンクルール](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [プロファイルの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### セグメンテーションとオーディエンス

- [セグメント サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)

### データガバナンスと同意

- [データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [データ使用状況ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview)
- [同意と環境設定のフィールドグループ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
- [Journey Optimizerでの同意](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### 計算属性

- [計算属性の概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [計算属性UI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)

### 監視と監視

- [アラートの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Observability Insightsの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)

### ガードレール

- [Journey Optimizerのガードレール](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [リアルタイムの顧客プロファイルのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [取り込みのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### チュートリアルとガイド

- [ジャーニーのチュートリアルの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [Web SDKのインストール](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
