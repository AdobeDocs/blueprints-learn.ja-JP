---
title: 購買グループベースのマーケティングおよびジャーニー管理
description: リードを購買グループに選別するアカウントレベルのジャーニーを開発して、B2B マーケティングの効果を向上させる方法を学びましょう。
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 2bf57f67-80c8-4368-98d2-05706427772d
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 1%

---

# 購買グループベースのマーケティングとジャーニー管理

このガイドでは、購買グループベースのマーケティングとジャーニー管理のユースケースパターンについて説明します。このパターンでは、[!DNL Adobe Journey Optimizer B2B Edition]と[!DNL Real-Time CDP B2B Edition]を使用して、購買グループ管理を使用したアカウントレベルのジャーニーオーケストレーションを実装します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

個人レベルのジャーニーパターンとは異なり、このパターンはアカウントレベルで動作し、個々のリードをソリューションの関心に関連する購入グループに選定し、購入グループレベルでエンゲージメントをスコアリングし、パイプラインステージを通じてアカウントを販売準備に導くマルチステップのアカウントジャーニーを調整します。

## ユースケースパターン

**購買グループベースのマーケティングとジャーニー管理**

リードを購買グループに選別するアカウントレベルのジャーニーを作成して、B2B マーケティングの効果を向上させます。

**実行プラン：** アカウント ID >購買グループの定義> リードの選定> アカウントジャーニーの実行> エンゲージメントスコアリング > レポート

## ユースケースの概要

B2B企業は、基本的な課題に直面しています。購入に関する意思決定が一人で行われることはほとんどありません。 複雑なB2Bの購入には、意思決定者、インフルエンサー、チャンピオン、予算決定者、技術評価者など、複数の関係者が関与し、総称して「購買グループ」を形成します。 従来のリードベースのマーケティングでは、各個人を個別に扱うため、アカウント内の役割の適切な組み合わせがエンゲージされ、購入の準備ができているかどうかを示す重要なシグナルを見落としていました。

購買グループベースのマーケティングおよびジャーニー管理では、個々のリードのオーケストレーション単位をアカウントや購買グループに移行することで、この問題に対処します。 このパターンにより、B2B マーケターは、ソリューションの関心（販売される製品またはサービス）を定義し、購買の決定に必要な役割を指定する購買グループテンプレートを作成し、その役割に対するリードの選定、購買グループレベルでのエンゲージメントのスコアリング、購買グループの完全性と準備状況シグナルに対応するアカウントジャーニーをオーケストレーションできます。

望ましい成果は、パイプラインの品質と速度の向上です。マーケティング部門は、アカウント内で適切な人物がエンゲージし、購買グループが十分に完了した場合にのみアカウントを営業部門に引き渡し、無駄な営業活動を削減し、取引の進行を加速させます。

## 主なビジネス目標

このユースケースパターンは、次のビジネス目標をサポートしています。

### リードのクオリフィケーションとコンバージョンを向上

スコアリング、育成、パーソナライズされたフォローアップにより、リードの品質を向上させ、パイプラインの進行を加速させることができます。

**KPI:** リードのコンバージョン、見込み顧客/リードのコンバージョン、効率性

[リードのクオリフィケーションとコンバージョンの改善について詳しく見る](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

### リードジェネレーションの促進

フォーム、イベント、コンテンツ、マルチチャネルエンゲージメントを通じて、セールスパイプラインの質の高いリードをより多く生み出します。

**KPI:**&#x200B;見込み顧客、リード単価、リードコンバージョン

[リードジェネレーションの強化について詳しく見る](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)

### 売上と売上を増加

最適化されたデジタルチャネル、キャンペーン、カスタマージャーニーを通じて、売上の増加を促進。

**KPI:**&#x200B;売上増加、パイプラインベロシティ、成約率

[売上と売上の増加について詳しく見る](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

## 戦術的なユースケース

次に、このパターンを適用できる特定のシナリオを示します。

- **ソリューション固有の購買グループの選定** – 必要なペルソナ（Economic Buyer、Technical Evaluator、Champion、End User）を指定する役割テンプレートを使用して、各製品ライン（「Enterprise CRM」、「Data Platform」、「Security Suite」など）の購買グループを定義し、CRMおよびマーケティングオートメーションシステムのリードをそれらの役割に対して選定します。
- **パイプラインアクセラレーション用のアカウントジャーニー** – 購買グループ内のエンゲージメントの低い役割にターゲットを絞ったナーチャリングメールを送信し、エンゲージメントのしきい値に達したときにセールスアラートをトリガーし、アカウントをセールス対応ステージに移行するマルチステップのアカウントジャーニーを編成します。
- **購買グループの完全性キャンペーン** – 購買グループに欠けている役割があるアカウントを特定（例：エコノミックバイヤーが特定されていない）し、アカウント内で適切なペルソナにエンゲージするためのターゲットを絞った獲得キャンペーンを開始します。
- **クロスセルのアカウントジャーニー** – 最初の取引がクローズした後、新しい購買グループを作成して補完的なソリューションの関心を惹きつけ、拡張された購買委員会を育成するアカウントジャーニーを調整します。
- **滞留取引に対する再エンゲージメント** – 購買グループのエンゲージメントスコアが低下しているアカウントを検出し、新鮮なコンテンツ、経営陣へのアウトリーチ、イベントへの招待を含むトリガーの再エンゲージメントジャーニーを検出します。
- **CRM インサイトを介した営業部門とマーケティング部門の連携** – 購買グループのステータス、エンゲージメントデータ、アカウントジャーニーの進捗状況を[!DNL Salesforce]または[!DNL Dynamics 365]内で直接確認できるため、営業担当者はマーケティングに適格なアカウントをリアルタイムで把握できます。
- **イベント主導の購買グループ更新** — リードがウェビナーに参加したり、ホワイトペーパーをダウンロードしたり、価格ページにアクセスしたり、デモをリクエストしたりすると、購買グループのメンバーシップとエンゲージメントスコアを自動的に更新します。
- **複数の地域をまたいだアカウント調整** – 地域ごとに異なる連絡先が異なる役割を持つグローバルアカウント全体で購買グループを管理し、地域間のエンゲージメントスコアリングを統合します。

## 主要業績評価指標

次のKPIは、このユースケースパターンの有効性を測定するのに役立ちます。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| 購買グループの完全性 | すべての必要な役割が入力された購買グループの割合 | [!DNL AJO B2B] Analytics ダッシュボード：購買グループごとの役割のカバー範囲を追跡 |
| 購買グループのエンゲージメントスコア | 購買グループの全メンバーのエンゲージメントスコアを集計 | [!DNL AJO B2B]件のエンゲージメントスコアリング：個人レベルのスコアが購買グループにロールアップされました |
| MQA （マーケティングクオリファイドアカウント）率 | マーケティング適格基準に達したアカウントの割合 | アカウントジャーニーの出口基準：営業対応ステージに移行するアカウント |
| パイプライン速度 | 購買グループの作成からセールスに適格な機会までの平均時間 | CRM統合：[!DNL AJO B2B]からCRM パイプラインへのステージ移行を追跡します |
| リードから購買グループへの適格化率 | 購買グループの役割に適格と回答したリードの割合 | [!DNL AJO B2B]購買グループ管理：適格購買グループ率と非適格リード率 |
| セールスアラート応答率 | セールスフォローアップ活動につながるセールスアラートの割合 | CRM セールスインサイト：アラートからアクティビティへのコンバージョンを追跡 |
| アカウントジャーニー完了率 | 目的のジャーニーパスを完了したアカウントの割合 | [!DNL AJO B2B] Analytics ダッシュボード：ジャーニー完了指標 |
| メールエンゲージメント率（B2B） | B2B ナーチャリングメールの開封率とクリック率 | [!DNL AJO B2B] レポート：メール配信とエンゲージメント指標 |

## アプリケーション

このユースケースパターンでは、次のAdobe アプリケーションを使用します。

- **[!DNL Journey Optimizer B2B Edition]（[!DNL AJO B2B]）** – アカウントレベルのジャーニーを編成し、役割テンプレートとソリューションの関心を使用して購買グループを管理し、人物および購買グループレベルでエンゲージメントをスコア化し、B2B メールコンテンツを作成し、SMS メッセージを送信し、セールスアラートを設定し、B2B分析ダッシュボードを提供します。
- **[!DNL Real-Time CDP B2B Edition]（[!DNL RT-CDP B2B]）** — クロスソース B2B データからアカウント プロファイルを統合し、個人とアカウントの関係を解決し、アカウントレベルのオーディエンスを評価し、B2B固有の宛先（[!DNL Marketo Engage]、[!DNL LinkedIn]、CRM）を設定し、B2B データ全体にデータ ガバナンスを適用します。

## 関連ドキュメント

次のリソースでは、このガイドで参照されているアプリケーションと機能に関する追加の詳細を提供します。

### [!DNL AJO B2B Edition]

- [AJO B2B edition ドキュメントホーム](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/guide-overview)
- [購買グループの概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)
- [ソリューションへの関心](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [役割テンプレート](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates)
- [購買グループの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create)
- [購買グループステージ](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [アカウントジャーニーの概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)
- [アカウントジャーニーノード](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes)
- [セールスアラートメール](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sales-alert-email)
- [CRM セールスインサイト](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/crm-sales-insights)

### B2B メールとコンテンツ

- [B2B メールオーサリング](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/email-authoring)
- [AJO B2BでのSMS オーサリング](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sms-authoring)
- [メール作成用AI アシスタントによって作成されたものです](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/ai-assistant-emails)

### B2B分析とダッシュボード

- [購買グループダッシュボード](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/dashboards/buying-groups-dashboard)
- [エンゲージメントダッシュボード](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/dashboards/engagement-dashboard)
- [インテリジェントダッシュボード](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/dashboards/intelligent-dashboard)
- [CJA B2B editionの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### [!DNL RT-CDP B2B Edition]

- [RT-CDP B2B editionの概要](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)
- [Real-Time CDPのB2B スキーマ](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/schemas/b2b)
- [アカウントオーディエンス](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/types/account-audiences)
- [Marketo Engage ソースコネクタ](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)

### データ基盤

- [XDM システムの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/home)
- [ID サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/home)
- [ソースの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/home)
- [セグメント サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/home)

### チャネル設定

- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [SMS チャネルの設定](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### データガバナンスとプライバシー

- [データガバナンスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/home)
- [高度なデータライフサイクル管理](https://experienceleague.adobe.com/ja/docs/experience-platform/data-lifecycle/home)

### 宛先

- [宛先の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/home)
- [宛先カタログ](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/overview)
- [LinkedIn Matched Audiencesの宛先](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/social/linkedin)

### ガードレール

- [リアルタイムの顧客プロファイルのガードレール](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/guardrails)
- [セグメント化のガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- [取り込みのガードレール](https://experienceleague.adobe.com/ja/docs/experience-platform/ingestion/guardrails)
- [Journey Optimizerのガードレール](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/guardrails)

### チュートリアルと基本を学ぶ

- [AJO B2B edition入門](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/guide-overview)
- [RT-CDP B2B edition チュートリアル](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-tutorial)
