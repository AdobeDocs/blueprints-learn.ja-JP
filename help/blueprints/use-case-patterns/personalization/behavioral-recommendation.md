---
title: 行動の推奨事項
description: 選択戦略とランキングモデルを使用して、項目とコンテンツのレコメンデーションを生成する方法を説明します。
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '7626'
ht-degree: 2%

---


# 行動の推奨事項

このガイドでは、[!DNL Adobe Journey Optimizer] （AJO） Decisioning、[!DNL Real-Time Customer Data Platform] （RT-CDP）および [!DNL Adobe Experience Platform] （AEP）を使用して行動製品およびコンテンツレコメンデーションを実装する方法について説明します。 Web、モバイルアプリ、メールチャネルをまたいでパーソナライズされたレコメンデーションエクスペリエンスを提供する必要があるソリューションアーキテクト、マーケティング技術者、実装エンジニア向けに設計されています。

実行可能なすべての実装オプション、各段階での決定に関する考慮事項および [!DNL Adobe Experience League] のドキュメントへのリンクを示します。 行動レコメンデーションは、AJO Decisioning セレクション戦略とランキングモデルを組み合わせ、行動シグナル（商品表示、購入、コンテンツのインタラクション、検索クエリ）を使用して、項目レベルまたはコンテンツレベルのレコメンデーションを生成します。 明示的な実施要件ルールを使用してキュレーションされた一連のマーケティングオファーから選択する Offer Decisioning とは異なり、このパターンは、大規模なアイテムカタログ（製品、記事、ビデオ）を対象に動作し、行動アフィニティ信号と ML ベースのランキングを使用して、各訪問者に最も関連性の高いアイテムを表示します。

## ユースケースの概要

製品カタログ、コンテンツライブラリまたはメディアライブラリを持つ組織では、行動履歴とセッション内のアクティビティに基づいて、各訪問者に最も関連性の高い項目を表示する必要があります。 ホームページでの「お勧め」カルーセル、製品の詳細ページでのクロスセルウィジェット、メールキャンペーンに埋め込まれた製品レコメンデーションのいずれであっても、基盤となる課題は同じです。各訪問者の行動プロファイルをカタログの最も関連性の高い項目に一致させ、適切なチャネルでこれらのレコメンデーションを適切なタイミングで配信します。

このパターンは、[!DNL Web SDK] または [!DNL Mobile SDK] を介してリアルタイムに行動信号を取り込み、項目属性と行動コンテキストを組み合わせたAJO Decisioning 選択戦略を通じて処理し、web、アプリ内、メールのチャネルを通じて推奨される項目を配信することで、課題に対処します。 ランキングモデルは、数式ベース（カテゴリの親和性スコアで並べ替えるなど）または AI ランク（パーソナライズされたレコメンデーションモデルなど）にすることができます。 このパターンでは、フォールバック Recommendations を設定することで、行動履歴のない新規訪問者向けのコールドスタートシナリオも処理します。

このパターンのターゲットオーディエンスには、実際のユーザーの行動に基づいたパーソナライズされたレコメンデーションを通じて、エンゲージメント、コンバージョンおよび平均注文額を向上させたい e コマースマーチャンダイジングチーム、コンテンツパーソナライゼーションチーム、デジタルエクスペリエンスチームが含まれます。

## 主なビジネス目標

このユースケースパターンでは、以下のビジネス目標がサポートされています。

### [&#x200B; クロスセルとアップセルの収益を促進 &#x200B;](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)

行動および購入履歴に基づいて、既存の顧客に補完的でプレミアムな製品またはサービスを宣伝します。

| KPI | 説明 |
| --- | --- |
| アップセル/クロスセル % | 推奨される補完的またはプレミアム商品を購入するお客様の割合 |
| 増分収益 | レコメンデーション主導の購入に起因する追加収益 |
| 顧客のライフタイムバリュー | より深い製品エンゲージメントによる長期的な価値の増加 |

### [&#x200B; コンバージョン率の向上 &#x200B;](../../business-objectives/revenue-monetization/increase-conversion-rates.md)

購入、サインアップ、フォーム送信などの目的のアクションを完了する訪問者や見込み客の割合を改善します。

| KPI | 説明 |
| --- | --- |
| コンバージョン率 | レコメンデーションを行った後にコンバージョンした訪問者の割合 |
| リードコンバージョン | レコメンデーションに関与した訪問者が顧客になる割合 |
| リードあたりのコスト | オーガニックレコメンデーションエンゲージメントによる獲得コストの削減 |

### [&#x200B; パーソナライズされたカスタマーエクスペリエンスの提供 &#x200B;](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)

コンテンツ、オファーおよびメッセージングを、個々の環境設定、行動およびライフサイクルステージに合わせて調整します。

| KPI | 説明 |
| --- | --- |
| エンゲージメント | レコメンデーションサーフェスを使用したインタラクションの頻度（クリック数、表示数、買い物かごへの追加） |
| コンバージョン率 | レコメンデーションに関与した訪問者とコントロールのコンバージョン率の上昇 |
| 顧客満足度（CSAT） | 適切にパーソナライズされたエクスペリエンスによる顧客満足度の向上 |

## 戦術的な使用例

このパターンに対する一般的な戦術的な実装を次に示します。

- 製品詳細ページの製品クロスセルウィジェット（「顧客も購入」）
- 閲覧履歴に基づくホームページの「お勧め」カルーセル
- 読み取り行動に基づくメディアサイトのコンテンツ推奨事項
- 「最近表示された」を類似の項目ウィジェットと組み合わせる
- 購入後の補完製品の推奨事項
- 行動アフィニティに基づく電子メール製品のレコメンデーション
- セッション内の参照動作に基づくカテゴリ固有の推奨事項
- 行動信号に基づく検索結果の再ランキング

## 主要業績評価指標

次の KPI は、行動レコメンデーション実装の有効性を測定するのに役立ちます。

| KPI | 測定アプローチ |
| --- | --- |
| レコメンデーションクリックスルー率（CTR） | 推奨項目のクリック数をレコメンデーションインプレッション数で割った値 |
| レコメンデーションコンバージョン率 | レコメンデーションクリック数の購入または目的のアクションをレコメンデーションクリック数合計で割った値 |
| Recommendations の影響を受ける売上高 | 1 つ以上のレコメンデーションベースの製品を含んだ注文からの合計売上高 |
| 平均注文額（AOV）上昇率 | Recommendations が関与するセッションとそうでないセッションの AOV が増加 |
| 注文あたりの項目数 | Recommendation-engaged セッションの注文あたりの項目数 |
| 推奨事項の対象範囲 | パーソナライズされた（フォールバック以外の）レコメンデーションを受信した、適格なページビューまたはセッションの割合 |
| コールドスタートのフォールバック率 | 行動履歴が不十分なためにフォールバックロジックによって提供されたレコメンデーションリクエストの割合 |

## ユースケースパターン

**行動に関する推奨事項**

AJO Decisioning の選択戦略とランキングモデルを使用して、行動シグナルに基づいて項目レベルまたはコンテンツレベルのレコメンデーションを生成し、コンテキストコンテンツを提供します。

**機能チェーン：** 行動信号取り込み/判定戦略の評価/レコメンデーション配信/レポート

パターンの組み合わせに関するガイダンスについては、実装に関する考慮事項の下のパターン構成の節を参照してください。

## アプリケーション

このユースケースパターンでは、次のアプリケーションが使用されています。

- **[!DNL Adobe Journey Optimizer]（AJO） Decisioning** – 行動シグナルを評価し、各訪問者に最も関連性の高いアイテムを返す選択戦略、ランキングモデル、アイテムカタログおよび決定ポリシー
- **[!DNL Adobe Real-Time Customer Data Platform]（RT-CDP）** – 行動プロファイルデータの蓄積、レコメンデーションスコーピングのオーディエンス評価、行動アフィニティスコアリングの計算属性
- **[!DNL Adobe Experience Platform]（AEP）** - [!DNL Web SDK] および [!DNL Mobile SDK] を介した行動イベントの取り込み、[!DNL Edge Network] 処理、イベントおよびカタログデータの XDM スキーマ管理

## 基本関数

このユースケースパターンでは、次の基本機能が配置されている必要があります。 各関数のステータスは、通常、必須、事前設定済みと想定、適用不可のいずれかを示します。

| 基本関数 | ステータス | 所定の位置に配置する必要があること | Experience League リファレンス |
| --- | --- | --- | --- |
| 管理とガバナンス | 所定の位置に想定 | 意思決定権限が有効なAJO サンドボックス。 項目カタログ管理、選択戦略の設定、チャネルサーフェスの管理へのアクセス権がプロビジョニングされたユーザーの役割。 | [&#x200B; サンドボックスの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/sandbox/home)、[&#x200B; アクセス制御の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/access-control/home) |
| データモデリングと準備 | 必須 | 項目/製品識別子を使用した行動シグナル（製品表示、買い物かごへの追加、購入、コンテンツのインタラクション）をキャプチャするエクスペリエンスイベントスキーマ。 推奨品目セットの品目カタログスキーマ（製品属性、カテゴリ、画像、価格）。 ID フィールドを含むプロファイルスキーマ。 [!DNL Real-Time Customer Profile] に対してすべてのスキーマが有効になっています。 | [XDM システムの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/home)、[&#x200B; スキーマ構成の基本 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/schema/composition)、[&#x200B; データセットの作成 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/catalog/datasets/create) |
| データソースとコレクション | 必須 | [!DNL Web SDK] または [!DNL Mobile SDK] を介したリアルタイムの行動イベントストリーミングは重要です。推奨の品質は、新しい行動シグナルに依存します。 品目カタログデータを取り込む（バッチまたはストリーミング）必要があります。 AJO サービスで設定されたデータストリームは、Edge Decisioning で有効になります。 | [Web SDKの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/home)、[Mobile SDKの概要 &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)、[&#x200B; データストリームの設定 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/datastreams/configure) |
| ID とプロファイル設定 | 必須 | 行動シグナルは、行動プロファイルを作成するために、（ECID を介して既知または匿名の） ID に関連付ける必要があります。 既知の訪問者レコメンデーションの場合、認証済み ID （CRM ID、メール）を設定する必要があります。 リアルタイムのレコメンデーション配信のために、Edgeでアクティブな結合ポリシー。 | [ID サービスの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/home)、[&#x200B; 結合ポリシーの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/merge-policies/overview) |
| オーディエンスの定義とセグメント化 | 推奨 | オーディエンスは、Recommendations の範囲（例：プレミアム製品のみをプレミアムメンバーに推奨する）またはフィルタリングに使用できます。 推奨事項が単なる行動である場合は、厳密には必要ありません。 電子メールベースのレコメンデーション（オプション C）で、ターゲットオーディエンスを定義する際に必須です。 | [&#x200B; セグメント化サービスの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/home)、[&#x200B; セグメントビルダー UI ガイド &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/segment-builder) |

## サポート関数

次の機能は、このユースケースのパターンを拡張しますが、コア実行には必要ありません。

| サポート機能 | ステータス | これが重要な理由 | Experience League リファレンス |
| --- | --- | --- | --- |
| 計算/派生属性の作成 | 推奨 | カテゴリ親和性のスコア、製品インタラクションの頻度、購入の最新性、総支出などの計算済み属性によって、レコメンデーションランキングの品質が向上します。[!DNL Customer AI] 傾向スコアは、購入の可能性を予測することで、関連度をさらに高めることができます。 | [&#x200B; 計算済み属性の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/computed-attributes/overview)、[&#x200B; 顧客 AI の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/intelligent-services/customer-ai/overview) |
| データ・ライフサイクル管理 | 推奨 | 行動イベントデータには適切な有効期限ポリシーが必要です。レコメンデーションの関連性は、古いデータによって低下します。 行動イベントデータセットにデータセット有効期限ポリシーを設定すると、鮮度が保証され、ストレージが管理されます。 同意の適用により、行動データのコンプライアンスへの使用が保証されます。 | [&#x200B; データセットの有効期限 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/data-lifecycle/ui/dataset-expiration)、[&#x200B; 高度なデータライフサイクル管理の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/data-lifecycle/home) |
| データ使用のラベル付けと適用 | 推奨 | 行動データのガバナンスラベルにより、レコメンデーションに対するインタラクション履歴の準拠した使用が保証されます。 行動データに閲覧パターン、購入履歴、または健康/金融商品の興味シグナルが含まれる場合は、特に重要です。 | [&#x200B; データガバナンスの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/home)、[&#x200B; データ使用ラベルの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview) |
| 監視と監視 | 推奨 | レコメンデーション配信待ち時間、フォールバック率および項目カタログの取り込み状態を監視する必要があります。 行動イベント取り込みエラーと決定エラーに関するアラートは、レコメンデーションの品質を維持するのに役立ちます。 | [Observability Insights の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/observability/home)、[&#x200B; アラートの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/observability/alerts/overview) |
| レポートと分析 | Included | レコメンデーションパフォーマンスレポートは、機能チェーン手順 4 の一部です。[!DNL Customer Journey Analytics] サーフェスやセグメントをまたいでレコメンデーションの有効性、収益への影響、項目レベルのパフォーマンスを分析すると、最適化に関するインサイトが得られます。 | [CJAの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-overview/cja-overview)、[Analysis Workspaceの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/home) |

## アプリケーション関数

このプランは、アプリケーション機能カタログから次の機能を実行します。 関数は、番号付きステップではなく、実装フェーズにマッピングされます。

### [!DNL Journey Optimizer] （AJO）

| 関数 | 実装フェーズ | 説明 |
| --- | --- | --- |
| 決定 | 品目カタログおよび選択戦略の設定 | アイテムカタログ（決定項目）、行動ランキングモデルを使用した選択戦略、フィルタリングルールおよびフォールバックの推奨事項を設定します |
| チャネル設定 | チャネルとサーフェスの設定 | レコメンデーションがレンダリングされる web （コードベースのエクスペリエンス）、アプリ内、コンテンツカードまたはメールチャネルの配信サーフェスを設定する |
| メッセージオーサリング | コンテンツと配信の設定 | レコメンデーションレンダリングテンプレート、項目表示レイアウトおよび推奨項目のパーソナライゼーション式の設計 |
| レポートとパフォーマンスの分析 | レポートと最適化 | AJOのネイティブレポートと [!DNL Customer Journey Analytics] の統合により、レコメンデーションのクリックスルー、コンバージョン、売上高の各指標を監視します |

### [!DNL Real-Time CDP] （RT-CDP）

| 関数 | 実装フェーズ | 説明 |
| --- | --- | --- |
| オーディエンスの評価 | オーディエンスの範囲（オプション C） | レコメンデーションのスコープ設定や、E メールレコメンデーションキャンペーンのターゲット母集団の定義に使用されるオーディエンスセグメントを評価します。 |
| プロファイルエンリッチメント | 行動信号充実 | レコメンデーションランキングを向上させる計算済み属性（カテゴリ親和性スコア、インタラクション頻度）を使用したプロファイルのエンリッチメント |

## 前提条件

実装を開始する前に、次の手順を完了してください。

- AJO Decisioning がターゲットサンドボックスでプロビジョニングされ、有効になります
- [!DNL Web SDK] または [!DNL Mobile SDK] がデプロイされ、製品/コンテンツ識別子を使用して行動イベントが収集されます
- 製品またはコンテンツのカタログデータは、取り込み可能です（製品名、カテゴリ、価格、画像 URL、可用性）
- 行動イベントスキーマには、カタログ項目にリンクする項目/製品識別子が含まれます
- サービスを有効にしてデータストリーム [!DNL Adobe Journey Optimizer] 設定する（Edge Decisioning で必要）
- `isActiveOnEdge: true` との結合ポリシーが設定されています（リアルタイムの web/アプリ推奨事項に必要）
- メールのレコメンデーションの場合（オプション C）：メールチャネルサーフェスが設定され検証されます
- メールのレコメンデーションの場合（オプション C）：ターゲットオーディエンスが定義され、評価されます

## 実装オプション

次のオプションでは、行動に関する推奨事項を実装する際の様々なアプローチについて説明します。 チャネル要件と技術的な制約に最適なオプションを選択します。

### オプション A:Web のリアルタイムの推奨事項

**最適な対象：** Web ページでの製品またはコンテンツのレコメンデーション – 製品詳細ページのクロスセルウィジェット、ホームページのレコメンデーションカルーセル、カテゴリページのパーソナライズされたリスト、検索結果のパーソナライゼーション。

**仕組み：**

訪問者がサイトを閲覧すると、[!DNL Web SDK] を介して行動シグナルがリアルタイムで収集されます。 各ページビュー、商品インタラクションまたは検索クエリは、AEPにストリーミングされ、訪問者のプロファイルに関連付けられます（匿名訪問者の場合は ECID を使用し、既知の訪問者の場合は認証済み ID を使用します）。 レコメンデーションサーフェスを含むページが読み込まれると、[!DNL Web SDK] は [!DNL Edge Network] を介してAJOに意思決定評価をリクエストします。 決定エンジンは、選択戦略に照らして訪問者の行動プロファイルを評価し、ランキングロジックを適用して、不適格な項目（既に購入済み、または在庫切れ）をフィルタリングし、推奨項目を返します。

レコメンデーションは、コードベースのエクスペリエンスまたは web チャネルサーフェスを通じてページ上にレンダリングされます。 レンダリングには、カルーセル、グリッド、単一項目ウィジェットまたは recommendation テンプレートで定義されている任意のカスタムレイアウトを使用できます。 インプレッションイベントとクリックイベントは、自動的にAEPにトラッキングされ、パフォーマンスレポートが作成されます。

**主な考慮事項：**

- Edge Decisioning では、結合ポリシーをEdge上でアクティブにする必要があります
- 推奨待ち時間は応答時間 [!DNL Edge Network] 依存する（シングルスコープリクエストの場合は 500 ms 未満のSLA）
- 匿名訪問者は、セッション内の行動に基づいてレコメンデーションを受け取ります。既知の訪問者には、セッション間の行動履歴が役立ちます。
- 行動履歴のないコールドスタート訪問者には、フォールバックのレコメンデーションが表示されます

**メリット：**

- セッション内の動作に基づくリアルタイムパーソナライゼーション
- [!DNL Edge Network] を介した 2 秒未満のレコメンデーション配信
- 匿名の訪問者と既知の訪問者の両方に対応
- 自動インプレッションとクリックの追跡
- 新しいお勧めのページを再読み込みする必要はありません

**制限事項：**

- Edge プロファイルストアに、完全なプロファイル属性のサブセットが含まれる
- 多くのプロファイル属性を持つ複雑なランキングモデルでは、ハブサイドの評価が必要になる場合があります
- 行動イベン [!DNL Web SDK] トラッキングを使用したデプロイメントが必要です

**Experience League:**

- [Edge Decisioning API を使用したオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Web SDKの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/home)

### オプション B：モバイルアプリの推奨事項

**最適な対象：** アプリ内製品レコメンデーション、パーソナライズされたコンテンツフィード、通知駆動型レコメンデーション、モバイルコマースエクスペリエンス。

**仕組み：**

行動シグナルは、ユーザーがアプリとやり取りする際に、[!DNL Mobile SDK] を介して収集されます。 製品表示、コンテンツのインタラクション、検索および購入がAEPにストリーミングされます。 レコメンデーションサーフェスを含む画面が読み込まれると、[!DNL Mobile SDK] は判定評価をリクエストします。 レコメンデーションは、モバイルアプリ内のアプリ内メッセージ、コンテンツカードまたはコードベースのエクスペリエンスを通じて配信されます。

コンテンツカードは、ユーザーが都合のよいときに参照できるフィードのようなエクスペリエンスを保持するので、モバイルアプリのレコメンデーションユースケースに特に適しています。 アプリ内メッセージは、特定の行動によってトリガーされるコンテキストに応じたレコメンデーションに使用できます（例えば、買い物かごに項目を追加した後に補完的な製品を表示するなど）。

**主な考慮事項：**

- 関連 [!DNL Mobile SDK] るインタラクションの行動イベントトラッキングを使用して設定する必要があります
- コンテンツカードは永続的なレコメンデーションサーフェスを提供し、アプリ内メッセージは一時的なものになります
- オフラインでの動作のトラッキングでは、遅延イベント送信のためにSDK キュー管理が必要です
- アプリストアの更新サイクルは、レコメンデーションレンダリングの変更をデプロイする速度に影響します

**メリット：**

- アプリに統合されたスムーズなレコメンデーションレンダリングによるネイティブモバイルエクスペリエンス
- コンテンツカードは、永続的で閲覧可能なレコメンデーションフィードを提供します
- アプリ内メッセージにより、行動によってトリガーされるコンテキストに応じたレコメンデーションが可能になります
- デバイスレベルのシグナル（場所、アプリの使用パターン）を活用して関連性を高めます

**制限事項：**

- [!DNL Mobile SDK] 統合およびアプリ開発リソースが必要です
- レンダリングの変更には、アプリの更新が必要です（サーバードリブン型レイアウトのコードベースのエクスペリエンスを使用する場合を除く）
- オフライン期間では、行動信号収集にギャップが生じる

**Experience League:**

- [Mobile SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [プッシュ通知チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### オプション C：電子メールでの行動に関する推奨事項

**最適な対象：** メールキャンペーンの製品レコメンデーション – 閲覧された製品レコメンデーションを含む閲覧メールの放棄、購入後のクロスセル電子メール、定期的な「ピック・フォー・ユー」ダイジェスト、パーソナライズされた製品の提案を含む再エンゲージメント電子メールです。

**仕組み：**

以前のセッションから蓄積された行動プロファイルデータは、メール送信時やレンダリング時にレコメンデーションの選択を通知します。 オーディエンスは、適切な受信者（閲覧したが購入しなかった訪問者、最近の購入を行った顧客など）をターゲットにするために定義されます。 キャンペーンまたはジャーニーは、レコメンデーションプレースメントを含むメールを送信するように設定されます。 送信時に、AJO Decisioning は、各受信者の行動プロファイルを選択戦略と照合して評価し、推奨される項目をメールコンテンツに挿入します。

このオプションは、セッション内のシグナルではなく、蓄積された行動履歴に依存します。 計算済み属性（カテゴリ親和性スコア、最近の製品表示、購入頻度）により、行動履歴をプロファイルレベルのシグナルに抽出して、選択戦略で効率的に評価できるので、メールのレコメンデーション品質が大幅に向上します。

**主な考慮事項：**

- メールのレコメンデーションは、開封時ではなく送信時に評価されます。送信時の行動プロファイルの状態によって、レコメンデーションが決定されます
- ランキング品質を向上させるには、計算済み属性を強くお勧めします
- メールのレンダリング制限（JavaScriptなし、制限付き CSS）によるレコメンデーションの表示形式の制限
- 設定済みおよび検証済みのメールチャネルサーフェスが必要です

**メリット：**

- 複数のセッションをまたぐ完全な行動履歴を活用して、パーソナライゼーションを深めます
- 既存のキャンペーンワークフローおよびジャーニーワークフローとの統合
- Web/アプリのタッチポイントが利用できない再エンゲージメントと勝利シナリオに効果的
- 1 つのメール内に複数のレコメンデーションプレースメントを含めることができます

**制限事項：**

- レコメンデーションは送信時に静的で、メールが開かれても更新されません
- メールレンダリングの制約により、レコメンデーションの表示形式が制限される
- オーディエンス評価および campaign/journey orchestration インフラストラクチャが必要です
- 追加の依存関係（チャネル設定、オーディエンス定義、キャンペーン実行）により、実装が複雑になる

**Experience League:**

- [メールの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/create-email)
- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### オプションの比較

次の表に、実装オプションの主な違いをまとめます。

| 条件 | オプション A:Web リアルタイム | オプション B：モバイルアプリ | オプション C：メール行動 |
| --- | --- | --- | --- |
| に最適 | Web ページの推奨事項（PDP、ホームページ、カテゴリ） | アプリ内レコメンデーションとコンテンツフィード | 製品レコメンデーションを使用したメールキャンペーン |
| 行動信号源 | インセッション + クロスセッション（[!DNL Web SDK]） | アプリ内インタラクション（[!DNL Mobile SDK]） | 蓄積された行動履歴（プロファイル） |
| 推奨待ち時間 | サブ秒（[!DNL Edge Network]） | サブ秒（[!DNL Edge Network]） | 送信時（ハブサイド評価） |
| 訪問者タイプ | 匿名で既知 | 既知（アプリユーザー） | 既知（メール受信者） |
| 複雑性 | 中 | Medium – 高 | 高 |
| チャネルの依存関係 | [!DNL Web SDK]、コードベースのエクスペリエンスサーフェス | [!DNL Mobile SDK]、アプリ内/コンテンツカードサーフェス | メールチャネルサーフェス、オーディエンス、キャンペーン/ジャーニー |
| が必要 | [!DNL Web SDK] デプロイメント、Edge結合ポリシー | [!DNL Mobile SDK] デプロイメント、Edge結合ポリシー | メールサーフェス、オーディエンス定義、キャンペーン設定 |

### 適切なオプションを選択

状況に合わせて最適なオプションを選択するには、次のガイダンスを使用します。

- Web サイト上でのリアルタイムの製品レコメンデーションが主な目標の場合は、**オプション A から開始** します。 これは、最も一般的な出発点であり、実装の複雑さを最小限に抑えながら、すぐに価値を提供します。
- モバイルアプリがプライマリエンゲージメントチャネルであり、アプリ内のレコメンデーションによってコンバージョンが大幅に向上する場合は、**オプション B を選択** します。 オプション B は、同じ選択戦略と品目カタログを使用して、オプション A と並行して実行できます。
- 行動レコメンデーションをメールキャンペーンに拡張する場合は、**オプション C を追加** します。 これは通常、オプション A または B の上に重ねて表示され、同じ品目カタログと選択戦略を使用しますが、メール固有のレンダリングテンプレートとオーディエンスベースのターゲティングを使用します。
- **オプション A と C を組み合わせる** という共通のパターンがあります。アクティブな訪問者に対するリアルタイムの web レコメンデーションに加え、コンバージョンせずに離脱した訪問者に対する放棄された参照または購入後のメールのレコメンデーション。

## 実装フェーズ

次のフェーズでは、行動に関する推奨事項のエンドツーエンドでの実装について説明します。

### フェーズ 1：行動イベントスキーマとデータ収集の設定

**アプリケーション機能：** AEP:F2 「Data Modeling &amp; Preparation」、AEP:Data Sources &amp; Collection （F3）

このフェーズでは、行動信号と項目カタログデータをキャプチャする XDM スキーマ、データセット、データ収集メカニズムを確立します。 このデータ基盤は、すべてのレコメンデーションロジックが依存するものです。

#### 決定：行動イベントのスキーマデザイン

Recommendations を推進すべき行動シグナルはどれですか？

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| 製品表示のみ | シンプルなクロスセル/アップセルの推奨事項 | 最小限の実装作業、限られたシグナル深度 |
| 製品表示+購入 | 購入除外およびクロスセルロジックを使用した Recommendations | 中程度の労力。「購入済みを除外」フィルタリングを有効にします |
| 完全な行動スイート（表示、購入、買い物かごへの追加、検索、コンテンツインタラクション） | マルチシグナルランキングによる高度なレコメンデーション | 最高レベルの信号品質。包括的な [!DNL Web SDK]/[!DNL Mobile SDK] 計測が必要 |

#### 決定：品目カタログの取り込み方法

商品またはコンテンツカタログはどのようにAEPに取り込まれますか？

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| ソースコネクタを介したバッチ取り込み | カタログの更新を定期的に行う（毎日/毎週） | セットアップの簡素化。カタログの変更はリアルタイムには反映されない |
| ストリーミング取得 | カタログをほぼリアルタイムで更新（価格の変更、可用性）する必要がある | より複雑：レコメンデーションに現在のインベントリが反映される |
| 手動/API アップロード | 変更頻度の低い小さなカタログ | 最もシンプルなセットアップで、大規模なカタログや動的なカタログに対しては拡張性がない |

**UI ナビゲーション：** データ管理/ スキーマ / スキーマを作成；データ収集/ データストリーム /新しいデータストリーム

**キー設定の詳細：**

- エクスペリエンスイベントスキーマは、イベントペイロードに製品/項目識別子（SKU、製品 ID、コンテンツ ID）を含める必要があります
- 品目カタログスキーマには、フィルタリングとランキングに使用する属性（カテゴリ、価格、画像 URL、可用性ステータス、タグ）を含める必要があります。
- データストリームでは [!DNL Adobe Journey Optimizer]Edge Decisioning 用のサービスが有効になっている必要があります
- [!DNL Web SDK] `sendEvent` 呼び出しには、XDM コマースフィールドにマッピングされた製品インタラクションデータを含める必要があります

**Experience League ドキュメント：**

- [XDM システムの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/home)
- [スキーマ構成の基本](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/schema/composition)
- [Web SDKの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/home)
- [データストリームを設定](https://experienceleague.adobe.com/ja/docs/experience-platform/datastreams/configure)
- [2 つのスキーマ間の関係の定義](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/tutorials/relationship-api)

### フェーズ 2:ID とプロファイルの設定

**アプリケーション機能：** AEP:ID およびプロファイル設定（F4）

このフェーズでは、ID 名前空間、プライマリ ID 指定および結合ポリシーを設定し、行動シグナルが訪問者プロファイルに正しく関連付けられ、リアルタイムのレコメンデーション配信に使用できるようにします。

#### 決定：Edge Decisioning の結合ポリシー

レコメンデーションユースケースには、リアルタイムのEdge評価が必要ですか？

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| Edge結合ポリシーでアクティブ | オプション A および B （web およびモバイルのリアルタイムの推奨事項） | 2 秒未満のレコメンデーション配信に必要です。サンドボックスごとに 1 つのEdge結合ポリシーのみ |
| 標準結合ポリシー（Edgeではない） | オプション C のみ（送信時に評価されるメールのレコメンデーション） | ハブサイド評価には十分です。Edge結合ポリシースロットを使用しません |

#### 決定：匿名 ID と既知の訪問者 ID の比較

匿名訪問者からの行動シグナルはどのように扱われるべきですか？

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| ECID のみ（匿名） | Recommendations は、主にセッション内行動に基づく匿名訪問者向け | よりシンプルな設定。訪問者が認証されない限り、セッション間の継続性はない |
| ECID +認証済み ID （CRM ID、メール） | ID ステッチを使用した既知の訪問者に対するクロスセッションの推奨事項 | 豊富な行動プロファイル：認証フローが必要 |
| 両方とも ID グラフリンクを使用 | ID ステッチを使用した、完全な匿名から既知のジャーニー | 最も包括的。ID リンクルールの設定が必要 |

**UI ナビゲーション：** ID/ID 名前空間；プロファイル/結合ポリシー

**キー設定の詳細：**

- ECID 名前空間は事前設定されており、[!DNL Web SDK] と [!DNL Mobile SDK] で自動的に使用されます。
- 認証済み ID 用にカスタム ID 名前空間（CRM ID、ロイヤルティ ID）を作成する必要があります
- エクスペリエンスイベントスキーマのプライマリ ID は、web/モバイル行動イベントの ECID にする必要があります
- 結合ポリシーでは、デバイス間の ID のステッチにプライベートデバイスグラフを使用する必要があります

**Experience League ドキュメント：**

- [ID サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/home)
- [ID 名前空間の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/namespaces)
- [結合ポリシーの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/merge-policies/overview)
- [ID グラフのリンクルール](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/identity-linking-logic)

### フェーズ 3：品目カタログと選択戦略の設定

**Application 関数：** AJO:Decisioning

このフェーズでは、項目カタログ（決定項目）、ランキング用の行動信号と項目属性を組み合わせた選択戦略、不適格な項目を除外するフィルタリングルール、コールドスタートプロファイルのフォールバックレコメンデーションを設定します。

#### 決定：品目カタログ範囲

レコメンデーションに使用できる項目は何ですか？

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| 商品カタログ（e コマース） | 物理的な製品またはデジタル製品を購入することをお勧めします | 品目属性には、価格、カテゴリ、有効数量、画像が含まれます。 |
| コンテンツカタログ （メディア/公開） | 記事、ビデオまたは教育コンテンツのレコメンデーション | 項目属性には、トピック、作成者、公開日、コンテンツタイプが含まれます。 |
| ハイブリッドカタログ | 製品とコンテンツの両方をお勧めします | 両方のタイプを格納する統合項目スキーマが必要です |

#### 決定：ランキングアプローチ

最適なレコメンデーションを決定するには、実施要件を満たす項目をどのようにランク付けすればよいですか？

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| 式ベースのランキング | ランキングのビジネスロジックを明確にします（例：カテゴリ親和性スコアで並べ替え、項目の人気度を乗算する） | 透過的で監査可能なランキング。定義されたランキング式が必要です |
| AI ランク （自動最適化） | 機械学習では、コンバージョンデータに基づいて最適なランキングを決定する必要があります | モデルのトレーニングには 1,000 以上のコンバージョンイベントが必要で、透明性が低い |
| 優先度ベース （手動） | 手動でキュレートされたシンプルなレコメンデーション順序 | 設定が容易で、個々の動作に適応しない |

#### 決定：フィルタールール

レコメンデーションから除外する必要がある項目

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| 購入済み項目を除外 | クロスセルと検出に関する推奨事項 | 行動プロファイルに購入履歴が必要です |
| 在庫切れ項目を除外 | 動的在庫を使用した e コマース | リアルタイムまたはほぼリアルタイムのカタログ更新が必要 |
| 以前に却下された項目を除外 | ユーザーが提案を却下できるコンテンツレコメンデーション | 行動イベントで却下のトラッキングを必要とする |
| カテゴリスコープのフィルタリング | 特定のカテゴリに限定されたレコメンデーション | フィルタリングに項目属性を使用 |

#### 決定：コールドスタート戦略

行動履歴のない新規訪問者には、何を表示すればよいですか？

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| 人気アイテム（グローバルなベストセラー） | 汎用フォールバック | 保守が容易で、パーソナライズされていない |
| カテゴリ固有の人気項目 | 訪問者がカテゴリページに到達しました | 文脈的に関連するフォールバック。ページコンテキストが必要です |
| キュレートされたエディトリアルピック | ブランドは、コールドスタートエクスペリエンスのエディトリアルコントロールを望んでいます | 手動でのキュレーションおよび更新が必要 |
| トレンド項目（時間加重された人気度） | 現在のトレンドを反映した動的フォールバック | トレンドシグナルの計算が必要 |

**UI ナビゲーション：** [!DNL Journey Optimizer]/コンポーネント/意思決定管理/決定；[!DNL Journey Optimizer]/コンポーネント/意思決定管理/オファー；[!DNL Journey Optimizer]/コンポーネント/意思決定管理/プレースメント

**キー設定の詳細：**

- 属性（カテゴリ、価格、画像 URL、タグ）を使用して、カタログ内の各製品またはコンテンツ項目を表す決定項目を作成します
- 項目カタログのフィルタリングと行動ランキングロジックを組み合わせた選択戦略を定義します
- ランキングモデルの設定 – 式ベースの式は、プロファイル属性（計算属性からのカテゴリ親和性スコアなど）を参照できます
- コールドスタートプロファイルのデフォルトのレコメンデーションとなるフォールバックオファー/項目を作成する
- 論理的なグループ化のために、コレクション修飾子（タグ）を使用してアイテムをコレクションに整理します
- 選択戦略内でフィルタ・ルールを設定し、ビジネス・ルールを適用します（購入した品目、在庫品目のみを除外）。

**Experience League ドキュメント：**

- [意思決定管理の概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [プレースメントの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [決定ルールの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [パーソナライズされたオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [フォールバックオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [コレクションの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [決定を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [ランキング戦略](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### フェーズ 4：チャネルとサーフェスの設定

**アプリケーション機能：** AJO:Channel Configuration

このフェーズでは、レコメンデーションがレンダリングされる配信サーフェスを設定します。 設定は、実装オプションによって大きく異なります。

#### 決定：配信サーフェスのタイプ

レコメンデーションはどこに表示されますか？

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| コードベースのエクスペリエンス（web） | カスタムレンダリングを使用した web ページのレコメンデーションウィジェット | レンダリングの柔軟性が最大。フロントエンド開発が必要 |
| Web チャネルサーフェス | 標準の web パーソナライゼーションサーフェス | AJO Web Designer を使用する。コードベースの Web Designer ほど柔軟性がない |
| アプリ内メッセージ | アプリの動作によってトリガーされるコンテキストの推奨事項 | 一時的；操作または解除の後に消える |
| コンテンツカード （モバイル） | モバイルアプリの永続的なレコメンデーションフィード | ユーザーが操作するまで保持され、フィードを閲覧できます。 |
| 電子メール | メールキャンペーンに組み込まれた製品レコメンデーション | 送信時は静的です。メールのレンダリング制約の対象です |

**オプションが分岐する場所：**

**オプション A （Web リアルタイム Recommendations）の場合：**
コードベースのエクスペリエンスサーフェスまたは web チャネルサーフェスを設定します。 コードベースのエクスペリエンスは、カスタムのレコメンデーションレンダリング（カルーセル、グリッド、アイテムカード）に最も柔軟に対応します。 サーフェス URI は、ページのレコメンデーションの表示場所を識別します。

**オプション B （モバイルアプリの推奨事項）の場合：**
アプリ内メッセージまたはコンテンツカードのサーフェスを設定します。 永続的なレコメンデーションフィードには、コンテンツカードをお勧めします。 アプリ内メッセージは、コンテキストに応じた行動トリガーのレコメンデーションに適しています。

**オプション C （メールでの行動の推奨事項）:**
サブドメインのデリゲーション、IP プールの割り当て、送信者の設定を含むメールチャネルサーフェスを設定します。 サーフェスの配信品質が検証されていることを確認します。

**UI ナビゲーション：** 管理/ チャネル / チャネルサーフェス / サーフェスを作成

**Experience League ドキュメント：**

- [チャネルサーフェスの設定](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [SMS チャネルの設定](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [プッシュ通知チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### フェーズ 5：コンテンツと配信の設定

**アプリケーション関数：** AJO：メッセージオーサリング

このフェーズでは、訪問者への推奨項目の表示方法を制御する推奨レンダリングテンプレートを定義します。 これには、項目レイアウトデザイン、項目属性（名前、画像、価格、リンク）を取り込むパーソナライゼーション式、全体的なレコメンデーションエクスペリエンスのデザインが含まれます。

#### 決定：レコメンデーション表示形式

推奨される項目はどのようにレンダリングする必要がありますか？

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| カルーセル（水平スクロール） | 垂直方向のスペースが制限されたホームページまたはカテゴリページ | 使い慣れた UX パターン。複数の項目をコンパクトなスペースで表示 |
| グリッド （複数行） | 十分なスペースを確保した専用のレコメンデーションセクション | 一度により多くのアイテムを表示します。「あなたにお勧め」セクションに適しています。 |
| 単一項目ウィジェット | 特定のページの場所（サイドバーなど）でのコンテキストに応じたレコメンデーション | 設置面積を最小限に抑え、インパクトの高い配置を実現 |
| インラインメールブロック | メール本文内に埋め込まれたレコメンデーション | 電子メールのHTML/CSS 制約の対象（通常、2～4 個） |

#### 決定：表示するレコメンデーションの数

決定がプレースメントごとに返す項目数

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| 3 ～ 4 項目 | 標準レコメンデーションウィジェット | 関連度と視覚密度のバランス |
| 6 ～ 8 項目 | スクロールまたはグリッドレイアウトを使用したカルーセル | 訪問者に対するその他のオプション。十分なカタログの深さが必要です |
| 1 項目 | コンテキストに応じた単一製品のレコメンデーション | 関連性に対する影響が最も大きく、レンダリングが最もシンプル |
| 10 以上の項目 | フィードスタイルのレコメンデーションエクスペリエンス | コンテンツが多いユースケース（メディア、公開） |

**オプションが分岐する場所：**

**オプション A （Web リアルタイム Recommendations）の場合：**
コードベースのエクスペリエンステンプレートを使用して、レコメンデーションレンダリングを設計します。 HTML、CSS、JavaScriptを使用して、カルーセル、グリッド、ウィジェットのレイアウトを作成します。 Personalization式は、意思決定応答属性（項目名、画像 URL、価格、商品 URL）を参照します。 インプレッションとクリックの追跡は、[!DNL Web SDK] によって自動的に処理されます。

**オプション B （モバイルアプリの推奨事項）の場合：**
項目表示ロジックを使用して、コンテンツカードまたはアプリ内メッセージテンプレートを設定します。 モバイルアプリがネイティブにレンダリングする JSON ベースのコンテンツ構造を使用します。 各推奨項目へのディープリンクを含めます。

**オプション C （メールでの行動の推奨事項）:**
メールDesignerを使用してメールコンテンツをデザインします。 決定を利用したコンテンツブロックを使用して、レコメンデーションプレースメントを挿入します。 メールテンプレート内の項目属性のパーソナライゼーション式を設定します。 件名のパーソナライゼーションで、上位の推奨項目を参照できます。

**UI ナビゲーション：** コンテンツ管理/コンテンツテンプレート；キャンペーン/ジャーニー/コンテンツを編集/メールDesigner

**キー設定の詳細：**

- 各レコメンデーションプレースメントは、フェーズ 3 で作成された決定を参照する必要があります
- Personalization式では、ハンドルバー構文を使用して項目属性をレンダリングします
- Web の場合：決定を呼び出し、応答をレンダリングするように、コードベースのエクスペリエンスを設定します
- メールの場合：メールアクションに決定をキャンペーンまたはジャーニー内に埋め込みます
- 既知の行動履歴を持つテストプロファイルを使用したレコメンデーションのプレビュー

**Experience League ドキュメント：**

- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [コンテンツのプレビューとテスト](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### フェーズ 6：オーディエンススコープとキャンペーン/ジャーニーの設定（オプション C のみ）

**Application Function:** RT-CDP:Audience Evaluation、AJO:Campaign Execution またはJourney Orchestration

メールベースのレコメンデーション（オプション C）の場合、このフェーズではターゲットオーディエンスを定義し、レコメンデーションメールを配信するキャンペーンまたはジャーニーを設定します。 レコメンデーションはページや画面の読み込み時にリアルタイムで配信されるので、オプション A と B はこのフェーズをスキップします。

#### 決定：オーディエンス評価方法

レコメンデーションメールのターゲットオーディエンスはどのように評価する必要がありますか？

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| バッチ評価 | スケジュールされたレコメンデーションメールキャンペーン （日次、週次ダイジェスト） | 予測可能な送信タイミング。送信前に評価されるオーディエンス |
| ストリーミング評価 | イベントトリガーのレコメンデーションメール（閲覧を放棄、購入後） | ほぼリアルタイムのオーディエンスの選定、Journey Orchestration とのペア |

#### 決定：配信メカニズム

メールはキャンペーンとジャーニーのどちらで配信しますか？

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| スケジュール済みキャンペーン | 定義されたオーディエンスに対する 1 回限りのレコメンデーションメールの送信または繰り返しのレコメンデーションメールの送信 | よりシンプルな設定：バッチオーディエンス評価と送信 |
| オーディエンスエントリを使用したジャーニー | オーディエンスの選定によってトリガーされた継続的なレコメンデーションメール | 複数ステップのフローを有効にする（レコメンデーションメールに続いてリマインダーを有効にする） |
| イベントトリガージャーニー | 特定のイベント（閲覧の放棄、購入）によってトリガーされたレコメンデーションメール | リアルタイムトリガー。イベントベースのジャーニーエントリが必要です。 |

**UI ナビゲーション：** 顧客/オーディエンス/オーディエンスを作成/ルールを作成；キャンペーン/キャンペーンを作成；ジャーニー/ジャーニーを作成

**キー設定の詳細：**

- 行動履歴を参照するセグメントルール式を使用してターゲットオーディエンスを定義します（例：「過去 7 日間に閲覧された製品で、購入しなかったもの」）
- フェーズ 4 のチャネルサーフェスを参照するメールアクションを使用してキャンペーンまたはジャーニーを設定します
- フェーズ 3 の決定をメールコンテンツに埋め込みます
- オーバーメッセージを避けるためのスケジュールと頻度ルールの設定

**Experience League ドキュメント：**

- [セグメントビルダー UI ガイド](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/segment-builder)
- [ストリーミングセグメント化](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [キャンペーンのライブレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)

### フェーズ 7：レポートと最適化の設定

**Application Function:** AJO: Reporting &amp; Performance Analysis、S5: Reporting &amp; Analysis

このフェーズでは、レコメンデーションのクリックスルー、コンバージョンおよび売上高指標に関するパフォーマンス監視を確立します。 レコメンデーションの有効性を測定し、最適化の機会を特定するためのレポートインフラストラクチャを作成します。

#### 決定：レポートの深度

必要なレポート分析のレベル

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| AJO ネイティブレポートのみ | 基本的なレコメンデーションパフォーマンス監視 | クイックセットアップ。AJOで追跡される指標に制限されます。 |
| AJOと [!DNL Customer Journey Analytics] の統合 | クロスチャネルレコメンデーションの影響分析と売上高アトリビューション | 接続とデータ表示 [!DNL Customer Journey Analytics] 必要とし、より深いインサイトを提供 |
| カスタムダッシュボードを使用したフル [!DNL Customer Journey Analytics] ワークスペース | 項目レベル、セグメントレベルおよびサーフェスレベルの分析を使用した継続的な最適化プログラム | 最も包括的：専門知識とセットアップ [!DNL Customer Journey Analytics] 必要 |

**UI ナビゲーション：** キャンペーン/キャンペーンを選択/全期間レポート；ジャーニー/ジャーニーを選択/全期間レポート；[!DNL Customer Journey Analytics] ーディエンス/プロジェクト/新しいプロジェクトを作成

**キー設定の詳細：**

- 配信指標とエンゲージメント指標に関するAJO キャンペーンおよびジャーニーレポートの確認
- [!DNL Customer Journey Analytics] 統合の場合、AJO エクスペリエンスイベントデータセット（メッセージフィードバック、メールトラッキング、決定）を含む接続を作成します。
- レコメンデーション固有のディメンション（項目名、項目カテゴリ、レコメンデーションサーフェス）および指標（インプレッション数、クリック数、コンバージョン数、売上高）を含む [!DNL Customer Journey Analytics] データビューを作成します
- レコメンデーション CTR、コンバージョン率およびインプレッションあたりの売上高の計算指標を作成します
- サーフェス、セグメント、期間をまたいだレコメンデーションパフォーマンスを比較する [!DNL Customer Journey Analytics] Workspace パネルの作成

**Experience League ドキュメント：**

- [キャンペーンのグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [接続の作成または編集](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-connections/create-connection)
- [データビューの作成または編集](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/home)
- [計算指標の概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

## 実装に関する考慮事項

実装前と実装中に、次のガードレール、落とし穴、ベストプラクティス、トレードオフを確認します。

### ガードレールと制限

- サンドボックスあたり最大 10,000 件の承認されたパーソナライズされたオファー（決定項目） [&#x200B; 意思決定管理ガードレール &#x200B;](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/guardrails)
- 決定あたりの最大 30 個のプレースメント
- 決定リクエストあたり最大 30 個のコレクション範囲
- オファー配信の応答時間SLA：シングルスコープのEdge リクエストの P95 における 500 ms 未満
- AI ランキングモデルでは、トレーニングに 1,000 以上のコンバージョンイベントが必要です
- オファーキャッピングカウンターは、高スループットのシナリオでは、最大で数秒の遅延が発生する場合があります
- Edgeの決定は、エッジプロファイルストアで使用できるプロファイル属性に制限されます
- サンドボックスごとにEdgeでアクティブにできる結合ポリシーは 1 つだけです。[&#x200B; プロファイルガードレール &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/guardrails)
- サンドボックスあたり最大 25 個のアクティブな計算属性 – [&#x200B; 計算属性ガードレール &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/computed-attributes/overview)
- サンドボックスあたり最大 4,000 個のセグメント定義 – [&#x200B; セグメント化ガードレール &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/guardrails)
- ストリーミング取り込み：HTTP 接続あたり最大 20,000 レコード/秒 – [&#x200B; 取り込みガードレール &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/ingestion/guardrails)

### よくある落とし穴

- **決定は、フォールバック項目のみを返します：** パーソナライズされた決定項目が有効期間内に承認され、実施要件ルールが訪問者のプロファイル属性に一致することを確認します。 キャッピング制限に達していないことを確認します。
- **Edge配信は、空のパーソナライゼーションを返します。** データストリームが [!DNL Adobe Journey Optimizer] サービスを有効にして設定され、決定範囲が [!DNL Web SDK] リクエストで正しくフォーマットされていることを確認してください。
- **ランキング式が適用されていません：** 式が構文的に有効で、アクセス可能なプロファイル属性を参照していることを確認してください。 数式エラーは、優先度ベースのランキングにサイレントにフォールバックします。
- **古いレコメンデーション：** 行動イベントデータがリアルタイムで流れない場合、レコメンデーションは古い行動プロファイルに基づきます。 [!DNL Web SDK] または [!DNL Mobile SDK] がアクティブにイベントをストリーミングしていることを確認します。
- **コールドスタートのフォールバック率が高すぎます：** 訪問者の多くがフォールバックのレコメンデーションを受け取っている場合は、行動履歴のみに依存するのではなく、コンテキストシグナル（現在のページカテゴリ、リファラルソース）を使用してコールドスタート戦略を強化することを検討してください。
- **ページに Recommendations がレンダリングされない：** コードベースのエクスペリエンスサーフェス URI がページ URL パターンと一致し、[!DNL Web SDK] ーザーが決定応答を正しくリクエストしてレンダリングしていることを確認します。
- **レコメンデーションにカタログ項目がありません：** すべてのカタログ項目が決定項目として取り込まれ、正しいコレクション修飾子でタグ付けされ、選択戦略によって参照される適切なコレクションに含まれていることを確認します。

### ベストプラクティス

- AI ランク付けモデルに投資する前に、計算済み属性（カテゴリ親和性、インタラクションの最新性）を使用した式ベースのランキングモデルから開始します。 式ベースのモデルは透明性があり、監査可能で、比較のための堅牢なベースラインを提供します。
- インプレッションを実装し、1 日目からのクリックの追跡。 インタラクションデータがない場合、AI ランキングモデルはトレーニングできず、レコメンデーションの有効性を測定することもできません。
- あらゆる場所で単一の戦略を再利用するのではなく、異なるレコメンデーションサーフェス（ホームページ、PDP、メール）に対して個別の選択戦略を作成します。 サーフェスが異なれば、提供されるユーザーインテントも異なります。
- 計算属性を使用して、行動履歴をランキングシグナルに絞り込みます。 生のイベントデータが細かすぎるので、効果的な式ベースのランキングを行えません。「カテゴリのアフィニティスコア」や「前回購入からの日数」などの集計シグナルの方が効果的です。
- パーソナライズされたレコメンデーションとは別に、フォールバックレコメンデーションをテストします。 フォールバック項目がブランドに適した高品質のデフォルトであり、新規訪問者に優れたエクスペリエンスを提供することを確認します。
- コールドスタートのフォールバック率を主要なヘルス指標として監視します。 時間の経過に伴うフォールバック率の低下は、行動範囲の拡大を示します。
- メールのレコメンデーションの場合、スケジュールは、行動プロファイルが最も完了した時間（例：閲覧時間のピーク後、その時間は送信しない）に送信します。

### トレードオフの決定

次のトレードオフは、具体的な要件に基づいて評価する必要があります。

#### リアルタイム信号と累積履歴の比較

セッション内の行動シグナルは、即時に関連性を提供しますが、深さは限られています。 蓄積された行動歴から深さが得られるが、古い場合もある。 これらのソースのバランスは、レコメンデーションの品質に影響します。

- **オプション A のお気に入り：** 既知の訪問者に対する累積履歴によって補完される、即時関連性のあるリアルタイムのシグナル
- **オプション C のお気に入り：** メールは非同期で送信されるので、累積履歴のみが保持されます
- **推奨事項：** web およびモバイル（オプション A、B）の場合、セッション内のシグナルを、過去の動作から得られた計算済み属性と組み合わせます。 メール（オプション C）の場合は、行動履歴を実用的なプロファイルレベルのシグナルにまとめる計算属性に多額の投資をします。

#### 数式ベースのモデルと AI ランクモデルの比較

式ベースのランキングは透過的で、すぐに行えます。 AI ランク付けモデルは自動的に適応しますが、トレーニングデータが必要で、ランキング決定を明確に把握する必要性が低くなります。

- **式ベースのお勧め：** 透明性、監査性、即時デプロイメントおよびランキングロジックに対するきめ細かいビジネス制御
- **AI 関連のお気に入り：** 自動最適化、推測しにくいパターンの検出、手動でのチューニング作業の削減
- **推奨事項：** 数式ベースのランキングから開始して、パフォーマンスベースラインを確立し、コンバージョンデータを蓄積します。 十分なトレーニングデータ（1,000 以上のコンバージョンイベント）があり、式の手動チューニングで達成できる範囲を超えて最適化したい場合は、AI ランクモデルに移行します。

#### レコメンデーションカバレッジと関連度

品目カタログを拡張し、フィルタリングルールを緩和すると、パーソナライズされたレコメンデーションを受信するリクエストの割合は増えますが、レコメンデーションごとの関連性は低下する可能性があります。

- **高いカバレッジのお気に入り：** パーソナライズされたレコメンデーションを表示する訪問者の数を最大化します。主な目標がエンゲージメントの場合に役立ちます
- **関連性の高いお気に入り：** 関連性の高い項目のみを表示（より多くの訪問者にフォールバックのレコメンデーションが表示されることを意味する場合でも同様）。主な目標がコンバージョンの場合に役立ちます。
- **推奨事項：** 中程度のフィルタリングから開始し（購入した項目、在庫切れの項目を除外）、フォールバック率とコンバージョン率の両方を監視します。 コンバージョンデータでサポートされている場合にのみ、フィルタリングルールを強化します。

#### Personalizationの深度と実装の複雑さの比較

より豊富な行動シグナルとより洗練されたランキングモデルにより、レコメンデーションの品質は向上しますが、実装の複雑さが増し、メンテナンスの負担が増します。

- **実装の簡素化に有利：** 価値創出までの時間の短縮、メンテナンスの減少、デバッグと反復の容易化
- **より深いパーソナライゼーションの恩恵：** コンバージョン率の向上、顧客体験の向上、競争力のある差別化
- **推奨事項：** 段階的に実装する。 製品ビューシグナルと式ベースのランキングから開始します（フェーズ 1）。 行動エンリッチメントの計算済み属性を追加します（フェーズ 2）。 基盤が完成し、十分なトレーニングデータが得られたら、AI ランクモデルを評価します（フェーズ 3）。

## 関連ドキュメント

次のリソースでは、このパターンで使用されるテクノロジーと機能について詳しく説明しています。

### 意思決定管理

- [意思決定管理の概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [プレースメントの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [決定ルールの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [パーソナライズされたオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [フォールバックオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [コレクションの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [コレクション修飾子の作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [決定を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [ランキング戦略](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Edge Decisioning API を使用したオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)

### データ収集と web/モバイルSDK

- [Web SDKの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/home)
- [Web SDKのインストール](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/install/overview)
- [Mobile SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [データストリームを設定](https://experienceleague.adobe.com/ja/docs/experience-platform/datastreams/configure)
- [Edge Network Server API の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/edge-network-server-api/overview)

### XDM とデータモデリング

- [XDM システムの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/home)
- [スキーマ構成の基本](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/schema/composition)
- [データセットの作成](https://experienceleague.adobe.com/ja/docs/experience-platform/catalog/datasets/create)
- [2 つのスキーマ間の関係の定義](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/tutorials/relationship-api)

### ID とプロファイル

- [ID サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/home)
- [ID 名前空間の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/namespaces)
- [結合ポリシーの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/merge-policies/overview)
- [リアルタイム顧客プロファイルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/home)

### オーディエンスとセグメント化

- [セグメント化サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/home)
- [セグメントビルダー UI ガイド](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/segment-builder)
- [ストリーミングセグメント化](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [エッジセグメント化](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/methods/edge-segmentation)

### 計算属性とプロファイルエンリッチメント

- [計算済み属性の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/computed-attributes/overview)
- [計算属性 UI ガイド](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/computed-attributes/ui)
- [顧客 AI の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/intelligent-services/customer-ai/overview)

### チャネル設定

- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [チャネルサーフェスの設定](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [サブドメインのデリゲート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)

### メッセージのオーサリングとパーソナライズ機能

- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### レポートと分析

- [キャンペーンのグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [CJAの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/home)
- [計算指標の概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

### データガバナンスとライフサイクル

- [データガバナンスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/home)
- [データ使用状況ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview)
- [高度なデータ・ライフサイクル管理の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-lifecycle/home)
- [データセット有効期限](https://experienceleague.adobe.com/ja/docs/experience-platform/data-lifecycle/ui/dataset-expiration)

### 監視と監視

- [Observability Insights の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/observability/home)
- [アラートの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/observability/alerts/overview)

### ガードレール

- [Journey Optimizer ガードレール](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/guardrails)
- [リアルタイム顧客プロファイルガードレール](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/guardrails)
- [取り込みガードレール](https://experienceleague.adobe.com/ja/docs/experience-platform/ingestion/guardrails)
- [ID サービスガードレール](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/guardrails)

### チュートリアルとガイド

- [ソースの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/home)
- [Tags の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/tags/home)
- [同意および環境設定フィールドグループ](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/field-groups/profile/consents)
