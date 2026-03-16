---
title: B2B 分析
description: クロスチャネルカスタマージャーニー分析に B2B アカウントレベルの情報を含める方法を説明します。
solution: Customer Journey Analytics, Real-Time Customer Data Platform
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '7528'
ht-degree: 1%

---


# B2B 分析

このガイドでは、[!DNL Customer Journey Analytics] （[!DNL CJA]）B2B editionと [!DNL Real-Time Customer Data Platform] （[!DNL RT-CDP]）B2B editionを使用した B2B アカウントレベルの分析のための包括的な実装リファレンスを提供します。 これは、B2B アカウントレベルの情報をクロスチャネルのカスタマージャーニー分析に組み込む必要があるソリューションアーキテクト、マーケティング技術者、実装エンジニア向けに設計されています。

フラットなアカウント構造から複雑なグローバルアカウント階層まで、アカウント中心の分析に関するすべての実行可能なアプローチをカバーし、各オプションをいつ選択するかについてのガイダンスを提供します。 このプランは、B2B データ接続、アカウントデータビュー設定、ワークスペース分析、ダッシュボードの公開に対応しています。

B2B Analytics は、アカウントベースの接続、B2B 固有のコンテナ（アカウント、グローバルアカウント、オポチュニティ、購入グループ）、アカウントレベルのレポートにより、標準の [!DNL CJA] 機能を拡張します。 この機能を使用すると、組織は、アカウントレベルでのマーケティングおよびセールスエンゲージメントの分析、オポチュニティの進行状況の追跡、購入グループの完全性の測定、拡張された B2B セールスサイクル全体でのマーケティングタッチポイントに対する売上高の関連付けを行うことができます。

## ユースケースの概要

B2B 組織は、分析に関する基本的な課題に直面しています。顧客は個人の人物ではなく、複数の関係者、購入グループ、機会で構成されるアカウントです。 標準的なユーザーベースの分析では、「最もエンゲージメントが高いアカウント」、「購入グループの完成度」、「商談の進行を促進するマーケティングタッチポイントはどれか」などの質問に答えることはできません。

B2B Analytics は、[!DNL CJA] B2B editionを活用して、ユーザーレベルの行動データをアカウント、オポチュニティ、購入グループディメンションと組み合わせるアカウント中心の分析ビューを作成することでこれを解決します。[!DNL RT-CDP] B2B editionは、Analytics レイヤーをフィードする基盤となるアカウントプロファイルの統合と B2B ID 解決を提供します。 これらのソリューションを組み合わせることで、アカウントレベルでのクロスチャネルジャーニー分析を構築し、マーケティングエンゲージメントとパイプラインの進捗を関連付け、マーケティングチームとセールスチームの両方に実用的なインサイトを提供することができます。

ターゲットオーディエンスには、B2B マーケティング運用チーム、需要創出リーダー、収益運用アナリスト、アカウントレベルのエンゲージメントとパイプラインの正常性を可視化する必要のあるセールスリーダーシップが含まれます。

## 主なビジネス目標

このユースケースパターンでは、以下のビジネス目標がサポートされています。

### 分析とレポートの改善

統合ダッシュボードとセルフサービスツールを通じて、レポート機能を強化し、より迅速で実用的なマーケティングインサイトを得ます。 B2B Analytics を使用すると、組織は、複数のソースからのアカウントレベルのエンゲージメントデータを単一の分析環境に統合し、マーケティングプログラムがパイプラインと収益に与える影響をクロスチャネルで可視化できます。

**KPI:** 効率、生産性

[分析とレポートの改善に関する詳細情報](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)

### データに基づく意思決定の有効化

セルフサービス分析、リアルタイムの顧客インサイト、戦略の指針となる AI を活用した予測で、チームを強化します。 アカウントレベルの分析では、アカウントの優先順位づけ、エンゲージメント戦略の最適化、パイプラインのオポチュニティとの連携に必要なデータを、マーケティングチームとセールスチームに提供します。

**KPI:** 効率、生産性

[詳しくは、データに基づく意思決定の有効化を参照してください](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)

### リードの選定とコンバージョンの向上

スコアリング、育成、パーソナライズされたフォローアップにより、リードの品質を高め、パイプラインの進行を加速させます。 CJA B2B editionは、B2B セールスサイクル専用に設計された 13 か月のアカウントルックバックウィンドウを拡張し、アカウントジャーニー全体で正確なマルチタッチアトリビューションを可能にします。

**KPI:** 効率、増分収益

[リードの選定とコンバージョンの向上に関する詳細情報](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

## 戦術的な使用例

次のシナリオは、このパターンを実際にどのように適用できるかを示しています。

- **アカウントエンゲージメントスコアリング分析** - Web、メール、イベントおよびコンテンツインタラクションにわたる集計エンゲージメント別にアカウントを測定およびランク付けし、販売のフォローアップに関するハイインテントなアカウントを特定します
- **購入グループの完全性トラッキング**：複数のアカウントの購入グループ構成を分析して、ロールカバレッジのギャップを特定し、不完全な購入グループのリード獲得を優先します
- **商談パイプラインの相関関係** - マーケティングエンゲージメントデータを商談ステージの進行状況と関連付けて、パイプラインの進歩を促すキャンペーンとタッチポイントを把握します
- **マルチタッチ B2B アトリビューション** - 13 か月のルックバックウィンドウを持つアトリビューションモデルを適用して、ファーストタッチからクローズドウォンまでの完全な B2B 購入ジャーニー全体でマーケティングタッチポイントをクレジットします
- **アカウントジャーニーマッピング** – 初期認識から商談の作成およびクローズまで、クロスチャネルアカウントジャーニーを視覚化し、共通のパスと摩擦ポイントを特定します
- **パイプラインに対するキャンペーンの影響** – 特定のキャンペーンがアカウントパイプラインの作成、オポチュニティの進展、収益の生成にどのように影響するかを測定します
- **購入グループエンゲージメントの進行状況** – 購入グループエンゲージメントスコアが時間の経過と共にどのように変化するかを追跡し、エンゲージメントのしきい値とオポチュニティの成果を関連付けます
- **アカウントベースのコンテンツのパフォーマンス** – 特定のアカウントセグメント、業界、購入グループの役割と共鳴するコンテンツアセットとトピックを分析します
- **販売とマーケティングの連携ダッシュボード** - マーケティングチームと販売チームの両方に、アカウントエンゲージメント、パイプラインの正常性、収益属性を統一されたビューで提供する共有ダッシュボードを作成します
- **アクティブ化のためのアカウントセグメント化** - アカウントレベルの分析に基づいて B2B セグメントを作成し（例えば、「機会を増やさずに高度に関与したアカウント」）、ダウンストリームのアクティベーション用に公開します

## 主要業績評価指標

次の KPI は、このユースケースパターンの成功を測定するのに役立ちます。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| アカウントエンゲージメントスコア | アカウント内のすべての連絡先にわたるエンゲージメント指標の集計 | アカウントレベルでの web 訪問、電子メールインタラクション、イベント出席、コンテンツダウンロードを組み合わせた計算指標 |
| 購買グループの完全性 | 購買グループ内で入力される必須ロールの割合 | 購買グループごとの必要な役割の合計に対する、入力済の役割の比率。経時的に追跡されます |
| マーケティングの影響を受けたパイプライン | マーケティングアクティビティによってタッチされたパイプラインの収益 | 関連するアカウント連絡先が属性ウィンドウ内でマーケティングタッチポイントを持つ商談値 |
| アカウントから商談へのコンバージョン率 | 適格なオポチュニティを生み出すエンゲージメント済みアカウントの割合 | 指定した期間のエンゲージメント済みアカウント総数でオポチュニティを割ったアカウント |
| 平均契約サイクル長 | 最初のマーケティングタッチから受注案件までの時間 | 最初の属性タッチポイントから商談クローズ日までの平均期間 |
| マーケティングアトリビューション収益 | マーケティングタッチポイントに起因する収益 | アトリビューションモデルごとに配分された、マーケティングタッチを含む受注案件からの売上高 |
| アカウントのリーチと浸透 | ターゲットアカウントごとにエンゲージした連絡先の数 | 既知の連絡先総数に対する、アカウントごとのマーケティングインタラクションのユニーク連絡先 |
| 購入ロールによるコンテンツエンゲージメント | 購入グループの役割ごとにセグメント化されたエンゲージメント指標 | ページビュー、ダウンロードおよび滞在時間を、購買グループ内のペルソナ/役割ごとに分類 |

## ユースケースパターン

**B2B 分析**

クロスチャネルカスタマージャーニー分析に B2B アカウントレベルの情報を含めます。

**関数チェーン：** B2B データ接続/ アカウントデータビューの設定/ Workspace Analysis / ダッシュボードの公開

## アプリケーション

次のアプリケーションを使用して、このユースケースパターンを実装します。

- **[!DNL Customer Journey Analytics]B2B edition** – 拡張ルックバックウィンドウで、アカウントベースの接続、B2B 固有のデータビューコンテナ、アカウントレベルのワークスペース分析、購入グループ分析、商談分析、B2B セグメント化、B2B アトリビューションを提供します
- **[!DNL Real-Time CDP]B2B edition** - アカウントプロファイルの統合、B2B ID の解決、B2B スキーマクラス（アカウント、オポチュニティ、購入グループ）、B2B エンゲージメントデータを取り込むための [!DNL Marketo Engage] 統合など、B2B データの基盤を提供します

## 基本関数

このユースケースパターンでは、次の基本機能が配置されている必要があります。 各関数のステータスは、通常、必須、事前設定済みと想定、適用不可のいずれかを示します。

| 基本関数 | ステータス | 設定する必要があること | Experience League リファレンス |
| --- | --- | --- | --- |
| 管理とガバナンス | 必須 | [!DNL CJA] B2B editionと [!DNL RT-CDP] B2B editionの使用権限で設定されたサンドボックス。 [!DNL CJA] および B2B データモデルへのアクセス権を持つデータエンジニア、アナリストおよびマーケティング運用ユーザーにプロビジョニングされた役割。 | [&#x200B; サンドボックスの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/sandbox/home) |
| データモデリングと準備 | 必須 | B2B クラス（XDM Business Account、XDM Business Opportunity、XDM Business Account Person Relation、XDM Business Opportunity Person Relation、XDM Business Marketing List Members）を使用して設定された B2B XDM スキーマ。 アカウント属性、商談ステージ、および購買グループの役割のフィールドグループを定義する必要があります。 データセットが作成され、プロファイルに対して有効になりました。 | [XDM システムの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/home)、[B2B edition スキーマ &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/schemas/b2b) |
| データソースとコレクション | 必須 | （通常は [!DNL Marketo Engage] ソースコネクタまたは CRM ソースコネクタを介して）接続され [!DNL Salesforce]B2B データソース。 アカウントレコード、商談レコード、ユーザーとアカウントの関係、行動エンゲージメントイベントは、AEP データセットに送られる必要があります。[!DNL Web SDK] または [!DNL Marketo] 統合は、アカウントの関連付けを使用して行動イベントをキャプチャする必要があります。 | [&#x200B; ソースの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/home)、[Marketo Engage コネクタ &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| ID とプロファイル設定 | 必須 | ユーザーとアカウントの関係を解決するように設定された B2B ID 解決。 アカウント ID、人物 ID （[!DNL Marketo] リード ID または CRM 連絡先 ID）、クロスデバイス ID （ECID、メール）をリンクする必要があります。 ID グラフは、B2B データモデルに固有の、多対多の人物とアカウントのマッピングをサポートする必要があります。 | [ID サービスの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/home)、[B2B ID 解決 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/schemas/b2b) |
| オーディエンスの定義とセグメント化 | 所定の位置に想定 | B2B セグメントをアクティベーション用に [!DNL CJA] からAEPに公開する場合は、アカウントレベルのオーディエンス定義を使用できます。 分析専用のユースケースの場合、これは厳密な前提条件ではありませんが、セグメントベースの分析にお勧めします。 | [&#x200B; セグメント化サービスの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/home) |

## サポート関数

次の機能は、このユースケースのパターンを拡張しますが、コア実行には必要ありません。

| サポート機能 | ステータス | これが重要な理由 | Experience League リファレンス |
| --- | --- | --- | --- |
| 計算/派生属性の作成 | 推奨 | アカウントプロファイルに対して計算された属性（合計エンゲージメントスコア、前回のアクティビティからの日数、商談数など）により、アカウントレベルの分析に [!DNL CJA] で使用できる分析ディメンションが強化されます。 | [&#x200B; 計算済み属性の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/computed-attributes/overview) |
| データ・ライフサイクル管理 | 推奨 | B2B データセット、特に [!DNL Marketo Engage] の行動イベントデータは、急速に増加する可能性があります。 データセット有効期限ポリシーは、ストレージを管理し、データ保持要件に確実に準拠するのに役立ちます。 | [&#x200B; 高度なデータ・ライフサイクル管理 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/data-lifecycle/home) |
| データ使用のラベル付けと適用 | 推奨 | B2B データには、多くの場合、機密ビジネス情報（契約値、競合上のインテリジェンス）が含まれています。 データ使用ラベルとガバナンスポリシーにより、分析ワークフローとアクティベーションワークフロー全体でこのデータが適切に使用されるようになります。 | [&#x200B; データガバナンスの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/home) |
| 監視と監視 | 推奨 | B2B ソースコネクタ（[!DNL Marketo]、[!DNL Salesforce]）には、取り込みの正常性を監視する必要があります。 [!DNL CJA] の接続ヘルス監視により、分析のデータの鮮度が保証されます。 取り込みエラーのアラートルールにより、ダッシュボードが古くなるのを防ぎます。 | [Observability Insights の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/observability/home) |
| レポートと分析 | Included | このパターンは、それ自体が分析パターンです。 この機能は、コア機能チェーンがレポート機能と分析機能を提供するので、本質的に含まれています。 | [CJAの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-overview/cja-overview) |

## アプリケーション関数

このプランは、アプリケーション機能カタログから次の機能を実行します。 関数は、番号付きステップではなく、実装フェーズにマッピングされます。

### [!DNL Customer Journey Analytics] B2B edition

| 関数 | 実装フェーズ | 説明 |
| --- | --- | --- |
| アカウントベースの接続 | フェーズ 1: B2B データ接続 | 組織レベルの分析用のプライマリ識別子として、アカウントまたはグローバルアカウントを使用して接続を設定します |
| B2B データビュー設定 | フェーズ 2：アカウントデータビューの設定 | 標準の人物、セッション、イベントのコンテナと共に、B2B 固有のコンテナ（アカウント、グローバルアカウント、オポチュニティ、購入グループ）を使用してデータビューを定義します |
| アカウントレベルのWorkspace分析 | フェーズ 3:Workspaceの分析 | アカウントレベルのディメンション、指標および B2B コンテナを使用したフリーフォーム分析の作成による組織レベルのジャーニーインサイトの獲得 |
| 購買グループ分析 | フェーズ 3:Workspaceの分析 | 購入決定プロセスを通じて購入グループの構成、エンゲージメント、進行状況を分析します |
| 商談分析 | フェーズ 3:Workspaceの分析 | セールス・funnelの各段階を通じてオポチュニティの進行状況を履歴管理し、マーケティング・エンゲージメント・データと関連づけます。 |
| B2B セグメント化 | フェーズ 3:Workspaceの分析 | フィルターされたアカウントレベルの分析のための B2B コンテナを使用したセグメントの作成 |
| B2B アトリビューション | フェーズ 3:Workspaceの分析 | B2B セールスサイクル分析の 13 か月間の拡張アカウントルックバックウィンドウを使用したアトリビューションモデルの適用 |
| 計算指標の作成 | フェーズ 3:Workspaceの分析 | アカウントのエンゲージメント率、購入グループの完全性、パイプラインの影響など、B2B KPI の計算指標を定義します |
| ダッシュボードとスコアカードの公開 | フェーズ 4：ダッシュボードの公開 | マーケティングおよびセールスリーダーシップ用のダッシュボードとモバイルスコアカードの作成と共有 |
| オーディエンスの公開 | フェーズ 4：ダッシュボードの公開 | ダウンストリームのアクティベーション用に、[!DNL CJA] 定義されたアカウントベースのオーディエンスをAEPに公開します |

### [!DNL Customer Journey Analytics] – 標準関数

| 関数 | 実装フェーズ | 説明 |
| --- | --- | --- |
| データ接続 | フェーズ 1: B2B データ接続 | クロスチャネル分析のために、AEP B2B データセットを [!DNL CJA] 接続に連結 |
| データビュー設定 | フェーズ 2：アカウントデータビューの設定 | B2B データビュー内での標準ディメンション、指標、アトリビューションおよび永続性の設定 |
| Workspaceの分析 | フェーズ 3:Workspaceの分析 | テーブル、フォールアウト、フロー、コホートおよびアトリビューションビジュアライゼーションを使用したフリーフォーム分析の作成 |
| ガイド付き分析 | フェーズ 3:Workspaceの分析 | アカウントレベルでのfunnel、トレンド、リテンションの分析にガイド付きワークフローを使用 |

### [!DNL Real-Time CDP] B2B edition

| 関数 | 実装フェーズ | 説明 |
| --- | --- | --- |
| アカウントプロファイルの統合 | 前提条件（F2/F4） | 専用の XDM B2B スキーマクラスを使用して、クロスソース B2B データを統合アカウントプロファイルに統合する |
| B2B Id 解決 | 前提条件（F4） | 複数レベルのアカウント階層と多対多のマッピングをサポートする、ユーザーとアカウントの関係の解決 |
| [!DNL Marketo Engage] Integration | 前提条件（F3） | ネイティブ B2B ソースコネクタを使用して、[!DNL Marketo Engage] から行動エンゲージメントデータおよびアカウント/リードレコードを取り込む |

## 前提条件

実装を開始する前に、次の項目を行う必要があります。

- B2B edition ライセンス [!DNL CJA] アクティブで、組織用にプロビジョニングされています
- B2B スキーマ [!DNL RT-CDP] アカウントプロファイルが設定された状態で、B2B edition ライセンスがアクティブになっている
- B2B XDM スキーマは、次のように定義されます（アカウント、オポチュニティ、アカウント人物関係、オポチュニティ人物関係、マーケティングリストメンバー）
- [!DNL Marketo Engage] および/または CRM ソースコネクタが設定され、データをアクティブに取り込んでいます
- アカウントの関連付けを使用して、アカウントレベルの行動イベントデータ（web 訪問、メールインタラクション、フォーム送信）がAEPに送られます
- 人物とアカウントの関係は ID グラフで確立されます
- 重要な分析のために、少なくとも 30 日間の B2B エンゲージメントデータの履歴を利用できます
- 関係者は、グループの役割の定義とソリューションの関心のマッピングを購入することに合意しています
- [!DNL CJA] ユーザーアカウントは、B2B edition機能に適した製品プロファイルでプロビジョニングされます
- ターゲット KPI とレポート要件は、マーケティングおよびセールスリーダーシップによって定義されています

## 実装オプション

次の節では、このユースケースパターンを実装する様々なアプローチについて説明します。

### オプション A：アカウント中心の分析

**最適な対象：** アカウントのレンズを通じてすべてのエンゲージメントデータとパイプラインデータを分析する組織。 このアプローチでは、勘定コンテナをメイン分析単位として使用し、購入ジャーニーを通じて勘定がどのように進行するかのトップダウンビューを提供します。

**仕組み：**

アカウントをプライマリ識別子として使用する [!DNL CJA] B2B 接続を設定します。 すべての行動イベント、機会および購買グループのデータは、アカウントレベルにロールアップされます。 データビューでは、アカウントを最上位レベルのコンテナとして使用し、ユーザー、セッションおよびイベントをネストしています。 これにより、「価格ページにアクセスしたアカウントの数と、30 日以内に作成されたオポチュニティの数」などの分析が可能になります。

アカウント中心の分析は、アカウントが購入単位である B2B 組織に最も自然なビューを提供します。 業界、会社サイズ、アカウント層、アカウント所有者などのディメンションを使用して、エンゲージメントパターンとパイプライン指標を分類できます。 アトリビューションは、長い B2B セールスサイクルに対応する 13 か月のルックバックウィンドウで、アカウントレベルで適用されます。

**主な考慮事項：**

- ID グラフにクリーンなアカウントと人物のマッピングが必要
- すべてのユーザーレベルのイベントは、アカウントに起因する必要があります
- アカウントに関連付けることができない匿名 Web トラフィックは、アカウントレベルの分析には表示されません

**メリット：**

- 購入ジャーニー全体の真のアカウントレベルのビューを提供
- B2B 収益の生成方法に一致するアカウントベースのアトリビューションを有効にします
- アカウント内にネストされたコンテナとして購買グループおよび商談分析をサポートします。
- Analytics をアカウントベースドマーケティング（ABM）戦略と連携させる

**制限事項：**

- 堅牢なユーザーからアカウントへの ID 解決が必要
- 匿名または一致しないエンゲージメントデータは分析から除外されます
- ユーザー中心の分析よりも設定が複雑

**Experience League:**

- [CJA B2B editionの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [B2B edition スキーマ](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/schemas/b2b)

### オプション B：グローバルなアカウント中心型分析

**最適な対象：** 複雑なアカウント階層を持つ企業組織で、親会社に複数の子会社アカウントがある場合。 このアプローチでは、グローバル・アカウントをプライマリ識別子として使用し、すべての連結元アカウント・アクティビティを親組織レベルに積み上げます。

**仕組み：**

プライマリ識別子としてアカウントではなくグローバルアカウントを使用して [!DNL CJA] B2B 接続を設定します。 これにより、親組織の下にあるすべての子会社アカウントからエンゲージメントデータが集計されます。 例えば、「Acme Corp」に地域子会社「Acme EMEA」と「Acme APAC」がある場合、グローバルアカウント接続は、3 つのエンティティすべてからのエンゲージメントを 1 つの分析ビューに統合します。

データビューには、最上位コンテナとしてグローバルアカウントが含まれ、アカウント、ユーザー、セッションおよびイベントがネストされたコンテナとして含まれています。 これにより、同じワークスペースプロジェクト内のグローバルおよび子会社の両方のアカウントレベルで分析が可能になります。 アトリビューションのルックバックウィンドウは、グローバルアカウントレベルで適用され、企業階層全体にわたるすべてのタッチポイントをキャプチャします。

**主な考慮事項：**

- B2B データモデルで定義された親子関係を持つアカウント階層データが必要です
- グローバルアカウント ID は、すべてのアカウントレコードにわたって生成され、正確である必要があります
- 子会社アカウントは、親に正しくマッピングする必要があります

**メリット：**

- 複雑なエンタープライズ・アカウント構造にわたって統合された可視性を提供
- 単一の企業顧客が複数のアカウント・レコードを持つ場合に、分析の断片化を防止します。
- 単一のグローバル・アカウント内の地域子会社を比較することが可能
- エンタープライズレベルのパイプラインと収益レポートをサポート

**制限事項：**

- 正確なアカウント階層データが必要であり、多くの組織では維持に苦労しています
- グローバルなレベルでのみ見ると、子会社レベルのパターンが不明瞭になる場合がある
- 階層関係を確立および維持するための追加のデータモデリング作業

**Experience League:**

- [CJA B2B editionの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### オプション C：ハイブリッドユーザー+ アカウント分析

**最適な対象：** ユーザーベースの分析からアカウントベースの分析に移行している組織、またはユーザーレベルとアカウントレベルの両方の表示が必要な組織。 このアプローチでは、同じ接続から 2 つのデータビュー（1 つはユーザー中心、もう 1 つはアカウント中心）を作成します。

**仕組み：**

すべての B2B データセット（イベント、アカウント、オポチュニティ、購入グループ、ユーザーとアカウントの関係）を含む単一の [!DNL CJA] B2B 接続を設定します。 次に、2 つのデータビューを作成します。1 つはプライマリコンテナとしてユーザーを使用するビュー（標準 [!DNL CJA] と同様）、もう 1 つはプライマリコンテナとしてアカウントを使用するビューです。 アナリストは、尋ねられる質問に応じて、データビューを切り替えることができます。

ユーザー中心データビューは、従来の個人レベルのジャーニー分析（「商談になるリードのコンバージョンパスは何か？」）を提供し、アカウント中心データビューは、組織レベルの分析（「エンゲージメントからパイプラインへのコンバージョン率が最も高いアカウントはどれか？」）を提供します。 両方のビューで同じ基礎データを使用し、一貫性を確保します。

**主な考慮事項：**

- ディメンションと指標の設定が異なる可能性がある 2 つのデータビューが必要です
- アナリストは、各表示を使用するタイミングに関するトレーニングが必要です
- 計算指標は、データビューごとに個別に作成する必要がある場合があります

**メリット：**

- 人物レベルとアカウントレベルの両方でデータを柔軟に分析できる
- ユーザーレベルの分析に慣れたチームにとって、より簡単な導入パス
- ユーザーレベルの指標とアカウントレベルの指標を比較できます
- リードベースとアカウントベースのマーケティング戦略の両方をサポート

**制限事項：**

- 2 つのデータビューを維持し、同期を維持
- 使用するビューに関してアナリストが混乱する可能性
- 計算指標とフィルターは、複数のビューをまたいで複製する必要がある場合があります

**Experience League:**

- [データビューの作成または編集](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [データビューの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/data-views)

### オプションの比較

| 条件 | オプション A：アカウント中心 | オプション B：グローバルなアカウント中心 | オプション C：ハイブリッド人物+ アカウント |
| --- | --- | --- | --- |
| に最適 | フラット勘定構造を持つ標準 B2B | 親子階層を持つエンタープライズ | 組織または二重のニーズの移行 |
| 複雑性 | 中 | 高 | Medium – 高 |
| データ要件 | アカウントと担当者のマッピング | アカウント階層+ マッピング | アカウントと担当者のマッピング |
| 属性の範囲 | アカウントレベル（13 か月間のルックバック） | グローバルアカウントレベル（13 か月間のルックバック） | 人物とアカウントの両方のレベル |
| 匿名データ | アカウントビューから除外 | グローバル表示から除外 | ユーザービューに含まれ、アカウントビューから除外 |
| が必要 | B2B edition[!DNL CJA]B2B edition[!DNL RT-CDP] | [!DNL RT-CDP] B2B edition、[!DNL CJA] B2B edition、階層データ | B2B edition[!DNL CJA]B2B edition[!DNL RT-CDP] |
| メンテナンス作業 | 単一のデータビュー | 単一のデータビュー | 2 つのデータビュー |

### 適切なオプションを選択

- **オプション A を選択します** 組織がフラットなアカウント構造を持つ（親子階層がない）場合、ABM 戦略は個々のアカウントレベルで動作し、アカウントレベルの分析への最も簡単なパスが必要となります。
- **ターゲット勘定科目が、地域または部門全体にわたって連結元勘定科目を持つ大企業で、企業の親レベルでの連結レポートが必要な場合は、「オプション B」を選択します**。 このオプションには、高品質のアカウント階層データが必要です。
- **オプション C を選択** 組織をリードベースからアカウントベースのマーケティングに移行する場合、アナリストはユーザーレベルのfunnel分析とアカウントレベルのエンゲージメント分析の両方が必要であるか、B2B と B2C のビジネスラインが混在している可能性があります。

## 実装フェーズ

次の各フェーズでは、推奨される実装シーケンスの概要を説明します。

### フェーズ 1: B2B データ接続

**アプリケーション機能：** [!DNL CJA] B2B：アカウントベースの接続、[!DNL CJA]：データ接続

分析用にAEP B2B データセットを [!DNL CJA] にバインドする [!DNL CJA] 接続を設定します。 この接続では、[!DNL CJA] に取り込むデータセット、プライマリ識別子のタイプ（アカウントまたはグローバルアカウント）、履歴データとストリーミングデータの取り込み方法を定義します。 接続は、後続のすべての分析の基礎です。

#### 決定：プライマリID のタイプ

接続でアカウント ID またはグローバルアカウント ID のどちらをプライマリ識別子として使用するかを決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| アカウント ID | フラットなアカウント構造（親子階層なし） | 設定を簡素化。各アカウントを個別に分析できます。 中小規模ビジネス向けの B2B で最も一般的な選択肢。 |
| グローバルアカウント ID | 下位階層を持つエンタープライズ勘定科目 | 階層データが必要です。親の下にあるすべての子会社を集計します。 エンタープライズ ABM プログラムに最適です。 |

#### 決定：データセットの選択とタイプの指定

含める B2B データセットとそれぞれの入力方法を決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| イベントデータセット（行動） | 常に含める | Web インタラクション、メールイベント、フォーム送信、コンテンツのダウンロード。 タイムスタンプフィールドが必要です。 これらはエンゲージメントシグナルです。 |
| アカウントレコードデータセット （プロファイル） | 常に含める | アカウント属性（業界、サイズ、階層、所有者など）。 勘定科目分析の次元コンテキストを提供します。 |
| 商談データセット （ルックアップ/プロファイル） | パイプライン分析に含める | 商談ステージ、値、クローズ日。 パイプラインおよび収益アトリビューションの分析に必須です。 |
| 購入グループデータセット（ルックアップ/プロファイル） | 購買グループ分析に含める | 購入グループの役割、エンゲージメントスコア、完全性。 購買グループ構成分析に必要です。 |
| 人物とアカウントの関係データセット（ルックアップ） | 常に含める | 人物をアカウントにマッピングします。 ユーザーレベルのイベントをアカウントレベルの分析に関連付ける際に重要です。 |
| キャンペーン/プログラムデータセット（ルックアップ） | アトリビューションに含める | キャンペーンメタデータ、プログラムタイプ、チャネル。 キャンペーンの影響分析を有効にします。 |

#### 決定：バックフィル範囲

接続にインポートする履歴データの量を決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| すべての既存データ | B2B のセールスサイクルは長く（6～18 か月）、完全な履歴が必要 | B2B にお勧めします。 大規模なデータセットの場合はバックフィルに数日かかる場合がありますが、完全なアトリビューションデータが提供されます。 |
| カスタムの日付範囲（過去 2～3 年） | データ品質が特定のポイントを超えると低下する | 完全性とデータ品質のバランスを取ります。 CRM データに履歴上の不整合がある場合に一般的です。 |
| バックフィルなし | テストまたは開発のみ | 新しいデータのみが流入します。 実稼動 B2B 分析には適していません。 |

#### B2B データ接続の設定

**UI ナビゲーション：** [!DNL Customer Journey Analytics]/接続/新しい接続を作成

主な設定の詳細：

- B2B データセットを含んだAEP サンドボックスを選択します。
- キャパシティ計画の毎日のイベントの平均数を設定します
- 各データセットを追加して、タイプ（イベント、ルックアップ、プロファイル）を指定します
- B2B 接続のアカウント ID またはグローバルアカウント ID を使用するように、ユーザー ID フィールドを設定します
- ほぼリアルタイムの更新が必要なデータセットのストリーミングを有効にする
- 履歴バックフィルに対して「すべての既存データをインポート」を有効にします

**オプションが分岐する場所：**

**オプション A （アカウント中心）の場合：**
プライマリ識別子をアカウント ID に設定します。 アカウントレコード、商談、購入グループおよびユーザー – アカウント関係のデータセットを追加します。 データセット間の結合のために、「アカウント ID」フィールドを使用してユーザーレベルのイベントデータセットを設定します。

**オプション B （グローバル アカウント中心）の場合：**
プライマリ識別子をグローバルアカウント ID に設定します。 アカウント階層データに「グローバルアカウント ID」フィールドが含まれていることを確認します。 適切なロールアップを行うには、すべてのデータセットにグローバルアカウント ID が含まれているか、この ID に結合可能である必要があります。

**オプション C （ハイブリッド）の場合：**
すべての B2B データセットで 1 つの接続を作成します。 アカウント ID をプライマリ識別子として使用します。 ユーザー中心のビューは、同じ接続で別のデータビュー設定を使用することにより、フェーズ 2 で作成されます。

**Experience League ドキュメント：**

- [接続の概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-connections/overview)
- [接続の作成または編集](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-connections/create-connection)
- [接続の管理](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-connections/manage-connections)
- [CJA B2B editionの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### フェーズ 2：アカウントデータビューの設定

**アプリケーション関数：** [!DNL CJA] B2B: B2B データビュー設定、[!DNL CJA]: データビュー設定

分析での接続データの表示方法を定義するデータビューを設定します。 B2B 分析の場合、これには、B2B 固有のコンテナ（アカウント、商談、購入グループ）の設定、B2B スキーマフィールドのディメンションと指標へのマッピング、B2B に適したルックバックウィンドウを使用したアトリビューションモデルの設定、B2B ビジネスロジックの派生フィールドの作成が含まれます。

#### 決定：コンテナ設定

有効にする B2B コンテナと名前の付け方を決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| アカウント +人物+ セッション + イベント | グループまたはオポチュニティ分析を購入しない標準 B2B | 最も単純な B2B コンテナ階層。 アカウントは最上位のコンテナです。 |
| アカウント +商談+人物+ セッション + イベント | パイプラインと売上高の分析が必要です | 商談をコンテナレベルとして追加し、商談を範囲とする分析を有効にします。 |
| アカウント +購入グループ +商談+人物+ セッション + イベント | 購買グループ構成を含む完全な B2B 分析 | 最も包括的。 B2B データモデルのすべてのレベルで分析を有効にします。 |
| グローバルアカウント + アカウント +人物+ セッション + イベント | グローバル アカウント階層分析 | グローバル勘定科目を、勘定科目の最上位レベルのコンテナとして追加します。 |

#### 決定：B2B 指標のアトリビューションモデル

コンバージョン指標のデフォルトにするアトリビューションモデルを決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| 線形アトリビューション（13 か月間のルックバック） | B2B ジャーニーのすべてのタッチポイントに対するクレジットと等しい | マーケティングアクティビティの完全な組み合わせを理解するのに最適です。 B2B の推奨される開始点。 |
| U字型属性（13 か月間のルックバック） | ファーストタッチとラストタッチに重点を置き、クレジットタッチからミドルタッチに対応 | リード作成と商談コンバージョンモーメントをハイライト表示します。 需要生成分析で共通です。 |
| タイムディケイ（13 か月間のルックバック） | より新しいタッチポイントは、より多くのクレジットを受け取る必要があります | エンゲージメントの最新性がセールス準備の重要なシグナルである場合に最適です。 |
| ラストタッチ | コンバージョン前の最終タッチポイントの簡単なレポート | 理解しやすいが、早期マーケティングは過小評価している。 運用レポートをすばやく作成する場合にのみ使用します。 |

#### 決定：B2B のセッション定義

B2B エンゲージメントのためのセッションの定義方法を決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| タイムアウト 30 分（デフォルト） | 標準の web 分析セッション動作 | Web エンゲージメント分析の標準。 長いコンテンツ消費セッションをフラグメント化できる場合があります。 |
| タイムアウトの延長（60～120 分） | B2B ユーザーは、より長い研究セッションに参加します | B2B の購入者は、多くの場合、技術的なコンテンツ、価格、ドキュメントの確認に長い時間を費やしています。 |
| イベントベースの新しいセッション | 特定のイベントは、常に新しいセッションを開始する必要があります | キャンペーンのクリックスルーまたはデモリクエストが常に新しい分析セッションを開始する必要がある場合に使用します。 |

#### アカウントデータビューの設定

**UI ナビゲーション：** [!DNL Customer Journey Analytics]/データビュー/新しいデータビューを作成

主な設定の詳細：

- フェーズ 1 で作成した接続を選択します。
- 組織に適したタイムゾーンとカレンダータイプの設定
- コンテナ名を B2B 関連の用語（アカウント/エンゲージメント/タッチポイントなど）に変更
- B2B スキーマフィールドのディメンションへのマッピング：アカウント名、アカウント ID、業界、会社のサイズ、アカウント層、アカウント所有者、商談のステージ、商談値、購入グループの役割、ソリューションの関心
- エンゲージメント指標のマッピング：イベント（回数）、人物、セッション、ページビュー、フォーム送信、メール開封数、メールのクリック数
- 主要なディメンションの永続性を設定する（例：アカウント業界はアカウントレベルで永続化される）
- コンバージョン指標のデフォルトとして 13 か月間のルックバックを使用し、アトリビューションを線形に設定します
- マーケティングチャネル分類、エンゲージメントスコアリング層および商談ステージ分類の派生フィールドを作成します

**オプションが分岐する場所：**

**オプション A （アカウント中心）の場合：**
アカウントをトップレベルコンテナとして持つ単一のデータビューを設定します。 パイプラインと購入グループの分析が必要な場合、商談と購入グループのコンテナを含めます。

**オプション B （グローバル アカウント中心）の場合：**
グローバルアカウントを最上位コンテナとして設定します。 勘定科目をサブコンテナとして含めて、グローバル分析と連結元分析の両方を使用可能にします。

**オプション C （ハイブリッド）の場合：**
同じ接続から 2 つのデータビューを作成します。 データビュー 1 では、プライマリコンテナとして Person を使用します（標準 [!DNL CJA] 動作）。 データビュー 2 では、B2B コンテナのプライマリコンテナとしてアカウントを使用します。 該当する場合は、両方のビューに同一の指標をマッピングします。

**Experience League ドキュメント：**

- [データビューの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/data-views)
- [データビューの作成または編集](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [コンポーネント設定の概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [永続性設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [アトリビューション設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [派生フィールド](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [セッション設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/session-settings)

### フェーズ 3:Workspaceの分析

**アプリケーション関数：** [!DNL CJA] B2B：アカウントレベルのWorkspace分析、購入グループ分析、商談分析、B2B セグメンテーション、B2B アトリビューション、[!DNL CJA]:Workspace分析、計算指標の作成、ガイド付き分析

KPI で定義された分析インサイトを提供する Workspace プロジェクトを作成します。 このフェーズには、B2B のディメンションと指標を使用したフリーフォームテーブルの作成、B2B KPI の計算指標の作成、B2B 固有のビジュアライゼーション（アカウントレベルのフロー、オポチュニティのfunnel、購入グループのエンゲージメント）の設定、B2B コンテナを使用したフィルター/セグメントの作成、B2B アトリビューションモデルの適用が含まれます。

#### 決定：Analysis Workspace の構造

ワークスペースプロジェクトの編成方法を決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| 複数のパネルを使用した単一の包括的なプロジェクト | 小規模なチームですが、すべての関係者が同じレポートを表示しています | メンテナンスが容易です。 パネルを使用して、トピック（エンゲージメント、パイプライン、アトリビューション）を分割します。 プロジェクトあたり最大 40 個のパネル。 |
| オーディエンス別の複数のフォーカスされたプロジェクト | 関係者ごとに必要な意見は異なります | マーケティングはエンゲージメント/アトリビューションを取得します。 営業は、パイプライン/アカウントのヘルスを取得します。 操作はデータ品質を取得します。 メンテナンスの増加とターゲットの絞り込みの改善 |
| ガイド付き分析を使用したテンプレートベースのプロジェクト | エキスパートユーザー以外のユーザー向けのセルフサービス分析 | funnelおよびトレンドビューについては、ガイド付き分析を使用します。 繰り返し可能な分析用のテンプレートとして保存する。 幅広いユーザーに導入するのに最適です。 |

#### 決定：B2B 計算指標

B2B KPI に必要な計算指標を決定します。

| 指標 | 数式 | 作成するタイミング |
| --- | --- | --- |
| アカウントのエンゲージメント率 | （アカウントイベント合計/アカウント合計） | 常に – コア B2B 指標 |
| 購買グループの完了率 | （入力済みの役割/必須役割） * 100 | 購入グループ分析が範囲内の場合 |
| アカウントからオポチュニティへのコンバージョン | 商談/エンゲージメント済みアカウントを持つアカウント | パイプライン分析が必要な場合 |
| パイプラインの影響 % | 影響パイプライン値/パイプライン値合計 | マーケティングアトリビューションが必要な場合 |
| コンタクト先ごとの平均エンゲージメント | アカウントあたりのイベント / ユニーク人物 | アカウント貫通分析が必要な場合 |
| 役割別のコンテンツエンゲージメント | 購入グループの役割でフィルター処理されたイベント | B2B のコンテンツの最適化が必要な場合 |

#### 決定：B2B フィルター/セグメント範囲

どのコンテナレベルのフィルターを作成するかを決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| アカウントレベルのフィルター | アカウントの一致条件を対象とした分析（エンタープライズ口座、特定の業界など） | 対象アカウントのすべてのイベントが含まれます。 B2B で最も一般的です。 |
| 商談レベルのフィルター | 特定のオポチュニティのタイプまたはステージを範囲とする分析 | 条件を満たす商談に関連するすべてのイベントが含まれます。 |
| グループレベルのフィルターの購入 | 特定の購入グループの状態を対象範囲とする分析 | 対象となる購入グループの人物からのイベントが含まれます。 |
| ユーザーレベルのフィルター | 条件（特定の役割、タイトルなど）に一致する個人を範囲とする分析 | 標準のフィルター動作。 B2B コンテキスト内の個々のエンゲージメントを分析する際に使用します。 |

#### ワークスペース分析の作成

**UI ナビゲーション：** [!DNL Customer Journey Analytics]/Workspace/プロジェクト/プロジェクトを作成

主な設定の詳細：

- フェーズ 2 で作成した B2B データビューを選択します。
- アカウントレベルのディメンション（アカウント名、業界、層）をエンゲージメント指標で分類したフリーフォームテーブルの作成
- ステージを通した商談の進行状況を示す商談funnelのビジュアライゼーションを作成します
- 役割のフィルレートと役割ごとのエンゲージメントを示す購入グループ構成テーブルを作成します
- 13 か月のルックバックでアトリビューションモデル（線形、U字形、タイムディケイ）を比較する B2B アトリビューションパネルの設定
- 購入ジャーニーの共通パスを示すアカウントフロービジュアライゼーションの作成
- アカウントの保持と再エンゲージメントの推移を分析するコホートテーブルの作成
- B2B フィルターをアカウント層、業界、エンゲージメントレベル別のセグメント分析に適用します
- 重要なイベント（キャンペーンの開始、製品リリース、価格の変更）に対する注釈を作成する

**Experience League ドキュメント：**

- [Workspaceの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/home)
- [プロジェクトの作成](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [フリーフォームテーブル](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [アトリビューションパネル](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [フロービジュアライゼーション](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [フォールアウトビジュアライゼーション](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [コホートテーブル](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [フィルターの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [計算指標の概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [計算指標の作成](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [注釈：概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/annotations/overview)
- [ガイド付き分析：概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/guided-analysis/overview)
- [分類ディメンション](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

### フェーズ 4：ダッシュボードの公開

**アプリケーション機能：** [!DNL CJA]：ダッシュボードおよびスコアカードの公開、[!DNL CJA]：オーディエンスの公開

B2B 分析のインサイトを関係者に提供する、共有可能なダッシュボードとモバイルスコアカードを作成します。 このフェーズでは、B2B オーディエンスのアクティベーションなど、ダウンストリームのユースケースでのアクティベーション用に、[!DNL CJA] 定義された B2B オーディエンスをAEPに公開する方法についても説明します。

#### 決定：ダッシュボード配信方法

B2B 分析のインサイトを関係者に提供する方法を決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| Workspace プロジェクト（デスクトップ） | インタラクティブな探索を必要とするアナリストやマーケティング業務 | 完全なインタラクティビティ、ドリルダウン、フィルターの切り替え。 [!DNL CJA] アクセスが必要です。 |
| モバイルスコアカード | 一目で KPI を確認できるエグゼクティブおよびセールスリーダー | トレンドラインを使用した概要数値。 ダッシュボードアプリ [!DNL Adobe Analytics] らアクセスできます。 限定的なインタラクティビティ。 |
| スケジュールされたPDF/CSV 書き出し | 定期的な更新を必要とする、[!DNL CJA] アクセス権を持たない関係者 | スケジュールに従った自動配信。 インタラクティブ機能はありません。 毎週/毎月のエグゼクティブサマリーに最適です。 |
| 上記のすべて | 多様な関係者のニーズを持つ大規模組織 | 最大リーチ。 メンテナンス作業の増加。 成熟した B2B 分析プログラムに推奨されます。 |

#### 決定：[!DNL CJA] からのオーディエンスの公開

アクティベーションのために B2B セグメントをAEPに再び公開する必要があるかどうかを判断します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| アカウントベースのオーディエンスの公開 | Analytics インサイトは、ターゲティングと抑制に関する情報を提供する必要があります | [!DNL RT-CDP] を介して [!DNL CJA] 定義されたセグメント（「オポチュニティのない高度に関与したアカウント」など）をアクティブ化できます。 更新サイクル：4 時間から毎週。 |
| 公開しない | Analytics はレポート専用で、アクティベーション用ではありません | よりシンプルな設定。 アクティベーションは [!DNL RT-CDP] で別途処理されます。 |

#### ダッシュボードとオーディエンスの公開

**UI ナビゲーション：** [!DNL Customer Journey Analytics]/プロジェクト/共有（Workspaceの場合）、プロジェクト/作成/モバイルスコアカード（スコアカードの場合）、コンポーネント/オーディエンス/公開（オーディエンス公開用）

主な設定の詳細：

- 主要な B2B KPI （エンゲージメント済みアカウントの合計、パイプライン値、購入グループの完全性）の概要番号を含むエグゼクティブダッシュボードを作成します
- トレンド指標の比較期間（前月比、前四半期比）を設定
- アカウントエンゲージメント、パイプラインの正常性、アトリビューション指標のタイルを使用してモバイルスコアカードを作成します
- エグゼクティブ用のフィルターを追加して、地域、業界、アカウント層別に表示を切り替えることができます
- 週次エグゼクティブレポート用のスケジュールされたプロジェクト配信の設定
- オーディエンスの公開の場合：B2B フィルターを選択し、ID 名前空間（アカウント ID）を設定して、更新サイクルを設定します

**Experience League ドキュメント：**

- [モバイルスコアカードの作成](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [プロジェクトの共有](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [プロジェクトのスケジュール](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [スコアカードの設定とキュレーション](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analytics ダッシュボード – エグゼクティブガイド](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [オーディエンスの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [オーディエンスの作成と公開](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/audiences/publish)

## 実装に関する考慮事項

以下の節では、実装時に念頭に置くべきガードレール、一般的な落とし穴、ベストプラクティス、トレードオフの決定について説明します。

### ガードレールと制限

- [!DNL CJA] 接続には、1 つのAEP サンドボックス （[CJA ガードレール）からのデータセットのみを含めることができ &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-admin/guardrails) す。
- 1 つのデータビューにつき最大 5,000 のディメンションと 5,000 の指標
- 1 つのデータビューにつき最大 100 個の派生フィールド
- B2B アトリビューションは、アカウントレベルの分析のために、最大 13 か月のルックバックウィンドウをサポートします
- すべてのサンドボックスで、[!DNL CJA] 顧客あたり最大 75 個の公開済みオーディエンス
- オーディエンス公開の最小更新サイクルは 4 時間ごと
- AEPから [!DNL CJA] へのストリーミングの待ち時間は通常、90 分以内です
- フリーフォームテーブルでは、最大 10 個のディメンション分類をサポートしています
- モバイルスコアカードは、スコアカードあたり最大 16 個のタイルをサポートします
- Workspace プロジェクトは、プロジェクトあたり最大 40 個のパネルをサポートします
- 大きな B2B データセット（数十億件のレコード）のバックフィルは、完了するまで数日かかる場合があります

### よくある落とし穴

- **ユーザーとアカウントのマッピングが不完全：** ユーザーレベルのイベントをアカウントに関連付けることができない場合、アカウントレベルの分析には表示されません。 直接またはユーザー/アカウント関係ルックアップデータセットを通じて、すべてのイベントデータセットにアカウント ID に結合できるフィールドが含まれていることを確認します。 分析を構築する前に、アカウントの関連付けが欠落しているイベントの割合を監査します。
- **データセットタイプの指定が正しくありません：** B2B ルックアップデータセット（オポチュニティ、購入グループ、ユーザーとアカウントの関係）は、[!DNL CJA] 接続でルックアップまたはプロファイルタイプとして正しく指定される必要があります。 ルックアップデータセットをイベントデータセットと誤って入力すると、各レコード [!DNL CJA] タイムスタンプ付きイベントとして扱おうとするので、誤った結果が生じます。
- **B2B にはアトリビューションウィンドウが短すぎます：** デフォルトの 30 日間のアトリビューションウィンドウを使用すると、通常 6～18 か月にまたがる B2B ジャーニーの早期ステージタッチポイントが失われます。 B2B アトリビューション指標の 13 か月間のルックバックウィンドウを常に設定します。
- **アカウントレベルとユーザーレベルの指標の誤った混在：** アカウントレベルの分析で「ユーザー」をカウントすると、誤解を招く可能性があります。 計算指標が適切なコンテナレベルで定義されていることを確認します。 「アカウントエンゲージメント率」では、人物ではなく、アカウントごとに分割されたアカウントレベルのイベントを使用する必要があります。
- **古い購入グループデータ：** 購入グループの構成とロールの割り当ては、時間の経過と共に変化します。 購入グループデータセットが定期的に更新されない場合、完了度指標は不正確になります。 ソースシステム（[!DNL Marketo Engage] または [!DNL AJO] B2B edition）が購買グループデータをアクティブに同期していることを確認します。
- **1 つのワークスペースプロジェクトのオーバーロード：** B2B Analytics は、エンゲージメント、パイプライン、アトリビューションおよび購入グループをカバーしています。 すべてを 1 つのプロジェクトに配置しようとすると、読み込みが遅くなり、ナビゲーションが混乱します。 複数のフォーカスされたプロジェクトまたは明確にラベル付けされたパネルを使用します。

### ベストプラクティス

- 後でオプション B （グローバルアカウント）を使用する予定がある場合でも、オプション A （アカウント中心）から開始します。 アカウント中心の分析はよりシンプルで、階層を複雑にする前にデータモデルを検証します。
- アカウントの関連付け、孤立したアカウントの数、購入グループの完了度指標を含むイベントの割合を追跡する、専用の「B2B データ品質」ワークスペースプロジェクトを作成します。 この毎週を実行して、データの問題を早期に把握します。
- 派生フィールドを使用して、アカウントレベルのイベント数に基づいてエンゲージメントスコアリング層（高/Medium/低）を作成します。 これにより、分析が簡素化され、技術者以外の関係者がダッシュボードを操作しやすくなります。
- B2B アトリビューションを設定する場合は、まず線形アトリビューションをベースラインとして使用し、次に U字型モデルとタイムディケイモデルと比較します。 多くの場合、モデル間の違いによって、マーケティングミックスが認知アクティビティとコンバージョンアクティビティのどちらに重み付けされているかが明らかになります。
- リーダーシップにとって最も重要な KPI をカバーする 8 つ以下のタイルを含む「B2B エグゼクティブサマリー」モバイルスコアカードを公開します。 It 部門に焦点を当てる：エグゼクティブスコアカードは、「どのように対応しているか」という回答が必要 「なぜ？」ではなく、
- 主要なイベント（製品ローンチ、主要なキャンペーンのローンチ、価格の変更、販売プロセスの変更）に注釈を付けて、データのトレンドのコンテキストを提供します。 B2B データは、多くの場合、イベントコンテキストなしでは説明できないスパイクやディップを示します。
- B2B オーディエンスを [!DNL CJA] から公開する場合は、標準のアクティベーションセグメントには日次更新を使用し、時間依存のセグメントには 4 時間の更新のみを使用します。 頻繁な更新は、処理リソースを消費します。

### トレードオフの決定

>[!NOTE]
>次のトレードオフ決定は、組織の特定の要件と制約に基づいて評価する必要があります。

**解析精度に対するデータ完全性**

アカウント分析にすべてのユーザーレベルのイベントを含めると（アカウントの関連付けが弱いイベントも含む）、データの完全性が向上しますが、アカウントマッピングに信頼性がない場合は、分析の精度が低下する可能性があります。

- **すべてのイベントのお気に入りを含む：** 包括的なエンゲージメント測定、より高いアカウントエンゲージメントスコア、より広い可視性
- **一致しないイベントの好みを除外：** 正確なアカウントレベルの指標、信頼できるアトリビューション、信頼性の高いパイプライン相関性
- **推奨事項：** 一致しないイベントをアカウントレベルの分析から除外し、別のユーザーレベルのデータビュー（オプション C）に含めて、全体像を把握する。 並列ワークストリームとして、アカウントの関連付けデータ品質の向上を優先します。

**B2B アトリビューションルックバックウィンドウの長さ**

ルックバックウィンドウが長くなる（13 か月）と、より多くのタッチポイントをキャプチャできますが、現在の購入決定とは関係のないマーケティングアクティビティが含まれる場合があります。

- **ルックバックの長期化（13 か月）のお気に入り：** 完全な B2B ジャーニーのキャプチャ、認知ステージのアクティビティのクレジット、長いセールスサイクルへの対応
- **ルックバックの短縮（6 か月）のお気に入り：** 最近のエンゲージメントに焦点を当て、古いタッチポイントからのノイズを減らし、現在の購入意図をより適切に反映
- **推奨事項：** 販売サイクルが長い（12 か月以上）エンタープライズアカウントには、13 か月のルックバックを使用します。 サイクルが短いミッドマーケットアカウントには 6 か月のルックバックを使用します。 比較するウィンドウごとに個別の計算指標を作成します。

**単一の包括的なデータ・ビューと複数のフォーカスされたデータ・ビューの比較**

すべての B2B コンテナとディメンションを含む 1 つのデータビューは、維持が簡単ですが、アナリストを複雑さに圧倒する可能性があります。 複数のフォーカスされたデータビュー（エンゲージメント、パイプライン、アトリビューション）は、使いやすいですが、保守が困難です。

- **単一ビューのメリット：** 一貫性、容易なメンテナンス、単一プロジェクト内でのクロスドメイン分析
- **複数ビューの使用：** アナリストのシンプルさ、読み込み時間の短縮、ユースケースごとのカスタマイズされたコンポーネントリスト
- **推奨事項：** 単一の包括的なデータビューから始めます。 アナリストから適切なディメンションと指標の見つけ方が困難であると報告された場合は、複数のビューに分割する前に、同じビュー内でキュレートされたコンポーネントグループを作成します。 ワークスペーステンプレートを使用して、アナリストが適切なコンポーネントに導きます。

## 関連ドキュメント

次のリソースでは、このユースケースパターンを実装するための追加情報を提供しています。

B2B edition **[!DNL CJA]す**。

- [CJA B2B editionの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [CJAの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-overview/cja-overview)
- [CJA ガードレール](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-admin/guardrails)

**接続**

- [接続の概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-connections/overview)
- [接続の作成または編集](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-connections/create-connection)
- [接続の管理](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-connections/manage-connections)

**データビュー**

- [データビューの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/data-views)
- [データビューの作成または編集](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [コンポーネント設定の概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [永続性設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [アトリビューション設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [形式設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [派生フィールド](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [セッション設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/session-settings)

**Workspaceと分析**

- [Workspaceの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/home)
- [プロジェクトの作成](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [フリーフォームテーブル](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [フロービジュアライゼーション](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [フォールアウトビジュアライゼーション](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [コホートテーブル](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [アトリビューションパネル](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [プロジェクトの共有](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [プロジェクトのスケジュール](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [分類ディメンション](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

**コンポーネント**

- [フィルターの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [フィルターの作成](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [計算指標の概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [計算指標の作成](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [注釈：概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/annotations/overview)
- [日付範囲](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)

**オーディエンス**

- [オーディエンスの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [オーディエンスの作成と公開](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/audiences/publish)
- [オーディエンスの管理](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/audiences/manage)

**ダッシュボードとスコアカード**

- [モバイルスコアカードの作成](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [スコアカードの設定とキュレーション](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analytics ダッシュボード – エグゼクティブガイド](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dashboards/set-up-execs)

**ガイド付き分析**

- [ガイド付き分析：概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/guided-analysis/overview)
- [Funnelビュー](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [トレンドビュー](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/guided-analysis/trends/usage)
- [保持ビュー](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/guided-analysis/retention/retention-rates)

B2B edition **[!DNL RT-CDP]す**。

- [RT-CDP B2B editionの概要](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#702702)
- [B2B edition スキーマ](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/schemas/b2b)
- [B2B ソースの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/sources/b2b)

**AEP Data Foundation**

- [XDM システムの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/home)
- [ソースの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/home)
- [Marketo Engage コネクタ](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [ID サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/home)
- [サンドボックスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/sandbox/home)

**データガバナンスとライフサイクル**

- [データガバナンスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/home)
- [高度なデータ・ライフサイクル管理](https://experienceleague.adobe.com/ja/docs/experience-platform/data-lifecycle/home)

**チュートリアルとガイド**

- [スキーマ構成の基本](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/schema/composition)
- [計算済み属性の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/computed-attributes/overview)
- [Observability Insights の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/observability/home)
