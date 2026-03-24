---
title: 行動の推奨事項
description: 選択戦略とランキングモデルを使用して、アイテムとコンテンツのレコメンデーションを生成する方法について説明します。
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: db16e773-e0da-46c4-9fa5-d16f04feb46b
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7545'
ht-degree: 2%

---

# 行動レコメンデーション

このガイドでは、[!DNL Adobe Journey Optimizer] （AJO） Decisioning、[!DNL Real-Time Customer Data Platform] （RT-CDP）および[!DNL Adobe Experience Platform] （AEP）を使用して、行動的商品とコンテンツの推奨事項を実装する方法について説明します。 web、モバイルアプリ、メールチャネルをまたいでパーソナライズされたレコメンデーション体験を提供する必要がある、ソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

実行可能なすべての実装オプション、各フェーズでの決定の考慮事項、および[!DNL Adobe Experience League] ドキュメントへのリンクが表示されます。 行動レコメンデーションは、商品の閲覧数、購入数、コンテンツのインタラクション、検索クエリなどの行動シグナルと、Adobe AJO Decisioningの選択戦略やランキングモデルを組み合わせることで、商品レベルまたはコンテンツレベルのレコメンデーションを生成します。 オファー決定支援では、適格性ルールとビジネス制約を使用して、オファー、プロモーション、インセンティブを決定します。一方、このパターンは、大規模で継続的に変化する項目カタログ（製品、記事、動画）に対して実行されます。このパターンでは、適格性を管理するのではなく、行動に即した親和性シグナルによって選択が促進されます。

## ユースケースの概要

製品カタログ、コンテンツライブラリ、メディアライブラリを利用している企業は、行動履歴やセッション中のアクティビティにもとづいて、各訪問者に最も関連性の高い項目を表示する必要があります。 ホームページの「おすすめ」カルーセル、製品詳細ページのクロスセルウィジェット、メールキャンペーンに埋め込まれた製品レコメンデーションなど、訪問者の行動プロファイルをカタログの最も関連性の高い項目に一致させ、適切なチャネルでタイミングよく提供するという根本的な課題は同じです。

このパターンは、[!DNL Web SDK]または[!DNL Mobile SDK]を介してリアルタイムで行動シグナルを取り込み、商品属性と行動コンテキストを組み合わせたAJO Decisioningの選択戦略を通じて処理し、web、アプリ、またはメールチャネルを通じて推奨商品を配信することで、この課題に対処します。 ランキングモデルには、数式ベース（カテゴリーの親和性スコアによるソートなど）やAIを使用したランク（パーソナライズされたレコメンデーションモデルなど）を使用できます。 このパターンは、フォールバックレコメンデーションを設定することで、行動履歴のない新規訪問者に対するコールドスタートシナリオも処理します。

このパターンのターゲットオーディエンスには、実際のユーザー行動にもとづくパーソナライズされたレコメンデーションを通じて、エンゲージメント、コンバージョン、平均注文額を向上させたいと考えているコマースマーチャンダイジングチーム、コンテンツパーソナライゼーションチーム、デジタルエクスペリエンスチームが含まれます。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

### [&#x200B; クロスセルとアップセルの収益を促進](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)

行動や購入履歴にもとづいて、既存顧客に補完的な商品やサービスを宣伝します。

**KPI:** アップセル/クロスセル %、増分収益、顧客生涯価値

### [&#x200B; コンバージョン率を向上](../../business-objectives/revenue-monetization/increase-conversion-rates.md)

購入、サインアップ、フォーム送信など、望ましいアクションを実行した訪問者と見込み顧客の割合を向上させます。

**KPI:** コンバージョン率、リードコンバージョン、リード単価

### [&#x200B; パーソナライズされた顧客体験の提供](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)

個人の好み、行動、ライフサイクルのステージに合わせて、コンテンツ、オファー、メッセージを調整。

**KPI:**&#x200B;のエンゲージメント、コンバージョン率、顧客満足度（CSAT）

## 戦術的なユースケース

このパターンの一般的な戦術的な実装は次のとおりです。

- 製品詳細ページの製品クロスセルウィジェット（「顧客も購入しました」）
- 閲覧履歴に基づくホームページの「おすすめ」カルーセル
- 読み取り行動に基づくメディアサイトでのコンテンツのレコメンデーション
- 「最近閲覧した」と類似アイテムのウィジェットの組み合わせ
- 購入後の補完商品レコメンデーション
- 行動の親和性にもとづいて商品レコメンデーションを電子メールで送信
- セッション内の閲覧行動にもとづいて、カテゴリー固有のレコメンデーションを提供
- 行動シグナルにもとづく検索結果のランキング

## 主要業績評価指標

以下のKPIは、行動レコメンデーションの実装の効果を測定するのに役立ちます。

| KPI | 測定アプローチ |
| --- | --- |
| CTR （Recommendation Click-Through Rate） | 推奨項目のクリック数をレコメンデーションのインプレッションで割った値 |
| レコメンデーションコンバージョン率 | レコメンデーションクリックからの購入または望ましいアクションを、レコメンデーションクリックの合計で割った値 |
| レコメンデーションの影響を受ける売上 | 1つ以上のレコメンデーション主導型製品を含む注文の総収益 |
| 平均注文額（AOV）リフト | レコメンデーションを利用したセッションと利用しないセッションのAOVが増加 |
| 注文あたりのアイテム | レコメンデーションエンゲージメントセッションの注文あたりのアイテム数 |
| 推奨事項 | パーソナライズされた（フォールバック以外の）レコメンデーションを受け取った、適格なページビューまたはセッションの割合 |
| コールドスタートフォールバック率 | 行動履歴が不十分なため、フォールバックロジックによって提供されたレコメンデーションリクエストの割合 |

## ユースケースパターン

**行動に関する推奨事項**

AJO Decisioningの選択戦略とランキングモデルを使用して、行動シグナルにもとづいて、コンテクストに即したコンテンツを提供するアイテムレベルまたはコンテンツレベルのレコメンデーションを生成します。

**関数チェーン：**&#x200B;行動シグナル取り込み>決定戦略評価> レコメンデーション配信> レポート

パターンの組み合わせに関するガイダンスについては、「実装の考慮事項」の「パターン構成」セクションを参照してください。

## アプリケーション

このユースケースパターンでは、次のアプリケーションを使用します。

- **[!DNL Adobe Journey Optimizer]（AJO） Decisioning** – 行動シグナルを評価し、各訪問者に最も関連性の高い項目を返す選択戦略、ランキングモデル、項目カタログ、および決定ポリシー
- **[!DNL Adobe Real-Time Customer Data Platform]（RT-CDP）** – 行動プロファイルデータの収集、レコメンデーションの範囲に対するオーディエンスの評価、行動の親和性スコアリングに対する計算属性
- **[!DNL Adobe Experience Platform]（AEP）** — [!DNL Web SDK]および[!DNL Mobile SDK]、[!DNL Edge Network]処理による行動イベントの取り込み、イベントデータおよびカタログデータのXDM スキーマ管理

## 基本関数

このユースケースパターンでは、次の基本機能を使用する必要があります。 各機能について、ステータスは、通常それが必要か、事前設定が想定されているか、適用できないかを示します。

| 基本関数 | ステータス | 整えておくべきもの | Experience League リファレンス |
| --- | --- | --- | --- |
| 管理とガバナンス | 同じ位置に仮定 | 決定権限が有効になっているAJO サンドボックス。 項目カタログ管理、選択戦略設定、チャネルサーフェス管理へのアクセスがプロビジョニングされたユーザーロール。 | [&#x200B; サンドボックスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/sandbox/home)、[&#x200B; アクセス制御の概要](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| データモデリングと準備 | 必須 | アイテム/製品識別子を使用して、行動シグナル（製品ビュー、カートへの追加、購入、コンテンツインタラクション）をキャプチャするエクスペリエンスイベントスキーマ。 推奨項目セットの項目カタログスキーマ（製品属性、カテゴリ、画像、価格）。 ID フィールドを持つプロファイルスキーマ。 [!DNL Real-Time Customer Profile]に対してすべてのスキーマが有効になっています。 | [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)、[&#x200B; スキーマ構成の基本](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)、[&#x200B; データセットの作成](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/create) |
| データソースと収集 | 必須 | [!DNL Web SDK]または[!DNL Mobile SDK]を介したリアルタイムの行動イベントストリーミングが重要です。レコメンデーションの品質は、新しい行動シグナルに依存します。 商品カタログデータは取り込む必要があります（バッチまたはストリーミング）。 AJO サービスで設定されたデータストリームは、Edge decisioningに対して有効になっています。 | [Web SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)、[&#x200B; モバイル SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)、[&#x200B; データストリームの設定](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| IDとプロファイル設定 | 必須 | 行動シグナルを行動プロファイルを構築するには、ID （ECIDで既知または匿名）に関連付ける必要があります。 既知の訪問者のレコメンデーションの場合、認証済みID （CRM ID、電子メール）を設定する必要があります。 リアルタイムのレコメンデーション配信のために、Edgeでアクティブな結合ポリシーを使用します。 | [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)、[結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| オーディエンスの定義とセグメント化 | 推奨 | オーディエンスは、レコメンデーションの範囲（プレミアム会員にプレミアム商品のみをレコメンデーションするなど）やフィルタリングに使用できます。 レコメンデーションが純粋に行動的である場合、厳密には必要ありません。 ターゲットオーディエンスを定義するメールベースのレコメンデーション（オプション C）に必要です。 | [&#x200B; セグメント化サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)、[&#x200B; セグメント ビルダーUI ガイド &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## サポート機能

次の機能は、このユースケースパターンを強化しますが、コア実行には必要ありません。

| サポート機能 | ステータス | アドビが重要である理由 | Experience League リファレンス |
| --- | --- | --- | --- |
| 計算属性/派生属性作成 | 推奨 | カテゴリーの親和性スコア、製品インタラクションの頻度、購入頻度、総支出などの計算属性により、レコメンデーションのランキング品質が向上します。[!DNL Customer AI] 傾向スコアは、購買の可能性を予測することで、関連性をさらに高めることができます。 | [計算属性の概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)、[顧客AIの概要](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| データライフサイクル管理 | 推奨 | 行動イベントデータには、適切な有効期限ポリシーを設定する必要があります。古いデータは、レコメンデーションの関連性を低下させます。 行動イベントデータセットにデータセットの有効期限ポリシーを設定することで、鮮度を確保し、ストレージを管理できます。 同意の履行により、行動データのコンプライアンス遵守を保証。 | [&#x200B; データセットの有効期限](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration)、[高度なデータライフサイクル管理の概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| データ使用のラベル付けと適用 | 推奨 | 行動データにガバナンスラベルを設定することで、レコメンデーションのためのインタラクション履歴のコンプライアンスを遵守した利用を保証します。 行動データに閲覧パターン、購入履歴、健康/金融商品への興味に関するシグナルが含まれる場合は特に重要です。 | [&#x200B; データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)、[&#x200B; データ使用ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview) |
| 監視と可観測性 | 推奨 | レコメンデーション配信の遅延、フォールバック率、商品カタログの取り込みの正常性を監視する必要があります。 行動イベントの取り込み失敗と決定エラーに関するアラートは、レコメンデーションの品質を維持するのに役立ちます。 | [&#x200B; オブザーバビリティ インサイトの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)、[&#x200B; アラートの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview) |
| レポートと分析 | 含まれる | Recommendation パフォーマンス レポートは、関数チェーン ステップ 4の一部です。[!DNL Customer Journey Analytics] サーフェスとセグメントをまたいで、レコメンデーションの効果、売上への影響、アイテムレベルのパフォーマンスを分析することで、最適化に関するインサイトを獲得できます。 | [CJAの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)、[Analysis Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home) |

## アプリケーション関数

この計画では、アプリケーション機能カタログから次の機能を実行します。 関数は、番号付きのステップではなく実装フェーズにマッピングされます。

### [!DNL Journey Optimizer] （AJO）

| 関数 | 導入フェーズ | 説明 |
| --- | --- | --- |
| 決定 | 商品カタログと選択戦略の設定 | 項目カタログ（決定項目）、行動ランキングモデル、フィルタリングルール、フォールバックレコメンデーションを使用した選択戦略を設定できます |
| チャネル設定 | チャネルとサーフェスの設定 | レコメンデーションがレンダリングされるweb （コードベースのエクスペリエンス）、アプリ内、コンテンツカード、メールチャネル用の配信サーフェスを設定します |
| メッセージ作成 | コンテンツと配信の設定 | レコメンデーションのレンダリングテンプレート、アイテム表示レイアウト、レコメンデーション用のパーソナライゼーション式のデザイン |
| レポートとパフォーマンス分析 | レポートと最適化 | AJOのネイティブレポートと[!DNL Customer Journey Analytics]との統合により、レコメンデーションのクリック率、コンバージョン、売上の指標を監視できます |

### [!DNL Real-Time CDP] （RT-CDP）

| 関数 | 導入フェーズ | 説明 |
| --- | --- | --- |
| オーディエンス評価 | オーディエンススコアリング（オプション C） | レコメンデーションの範囲を決定したり、メールによるレコメンデーションキャンペーンのターゲット母集団を定義したりするために使用されるオーディエンスセグメントを評価します |
| プロファイルエンリッチメント | 行動シグナルの強化 | レコメンデーションのランキングを向上させる計算属性（カテゴリ親和性スコア、インタラクション頻度）を使用してプロファイルを強化します |

## 前提条件

実装を開始する前に、次の手順を完了してください。

- [ ] AJO Decisioningがプロビジョニングされ、ターゲットサンドボックスで有効になっています
- [ ] [!DNL Web SDK]または[!DNL Mobile SDK]がデプロイされ、製品/コンテンツ IDを使用して行動イベントを収集しています
- [ ]製品またはコンテンツカタログデータを取り込み可能です（製品名、カテゴリ、価格、画像URL、可用性）
- [ ]行動イベントスキーマには、カタログ項目にリンクする項目/製品識別子が含まれます
- [ ] データストリームは、[!DNL Adobe Journey Optimizer] サービスが有効になっている状態で設定されています（Edge Decisioningに必要）
- [ ] `isActiveOnEdge: true`との結合ポリシーが設定されています（リアルタイム web/アプリのレコメンデーションに必要）
- [ ]電子メールのレコメンデーション （オプション C）：電子メールチャネルサーフェスが設定され、検証されています
- [ ] メールのレコメンデーション （オプション C）: ターゲットオーディエンスが定義され、評価されています

## 実装オプション

次のオプションでは、行動レコメンデーションを実装するための様々なアプローチについて説明します。 チャネルの要件と技術的な制約に最も適したオプションを選択します。

### オプション A:web リアルタイムのレコメンデーション

**Web ページでの商品またはコンテンツのレコメンデーションに最適：**&#x200B;商品またはコンテンツのレコメンデーション – クロスセルウィジェット、ホームページのレコメンデーションカルーセル、カテゴリーページのパーソナライズされたリスト、検索結果のパーソナライゼーション。

**仕組み：**

訪問者がサイトを閲覧すると、行動シグナルは[!DNL Web SDK]を介してリアルタイムで収集されます。 各ページビュー、商品インタラクション、検索クエリは、Adobe AEPにストリーミングされ、訪問者のプロファイルに関連付けられます（匿名の訪問者の場合はECID、既知の訪問者の場合は認証ID）。 レコメンデーションサーフェスを含むページが読み込まれると、[!DNL Web SDK]は[!DNL Edge Network]を介してAJOから決定評価をリクエストします。 決定エンジンは、選択戦略に対して訪問者の行動プロファイルを評価し、ランキングロジックを適用し、不適格な商品（既に購入された商品、在庫切れ商品）をフィルタリングし、推奨される商品を返品します。

レコメンデーションは、コードベースのエクスペリエンスまたはweb チャネルサーフェスを通じてページ上にレンダリングされます。 レンダリングには、カルーセル、グリッド、単一アイテムのウィジェット、またはレコメンデーションテンプレートで定義された任意のカスタムレイアウトを使用できます。 インプレッションイベントとクリックイベントは、パフォーマンスレポート用にAEPに自動的に追跡されます。

**重要な考慮事項：**

- Edge decisioningでは、Edgeで結合ポリシーをアクティブにする必要があります
- レコメンデーションの待ち時間は、[!DNL Edge Network]の応答時間に依存します（シングルスコープリクエストの場合は500 ミリ秒未満のSLA）
- 匿名の訪問者は、セッション内の行動にもとづいてレコメンデーションを受け取ります。既知の訪問者は、セッション間の行動履歴から利点を得ることができます
- 行動履歴がないコールドスタート訪問者には、フォールバックのレコメンデーションが表示されます

**利点：**

- セッション内の行動にもとづくリアルタイムのパーソナライゼーション
- [!DNL Edge Network]経由のサブセカンドレコメンデーション配信
- 匿名の訪問者と既知の訪問者の両方に対応
- インプレッションとクリックの自動追跡
- 新しいレコメンデーションにページの再読み込みは必要ありません

**制限：**

- Edge プロファイルストアには、完全なプロファイル属性のサブセットが含まれます
- 多くのプロファイル属性を持つ複雑なランキングモデルでは、ハブサイドでの評価が必要になる場合があります
- 行動イベント トラッキングを使用した[!DNL Web SDK]展開が必要です

**Experience League:**

- [Edge Decisioning APIを使用したオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Web SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)

### オプション B：モバイルアプリレコメンデーション

**アプリ内の商品レコメンデーション、パーソナライズされたコンテンツフィード、通知を活用したレコメンデーション、モバイルコマースエクスペリエンスなど、**&#x200B;に最適です。

**仕組み：**

行動シグナルは、ユーザーがアプリを操作する際に[!DNL Mobile SDK]を介して収集されます。 製品ビュー、コンテンツでのやり取り、検索、購入は、AEPにストリーミングされます。 レコメンデーションサーフェスを含む画面が読み込まれると、[!DNL Mobile SDK]は決定評価をリクエストします。 レコメンデーションは、アプリ内メッセージ、コンテンツカード、モバイルアプリ内のコードベースのエクスペリエンスを通じて配信されます。

コンテンツカードは、オーディエンスが自由に閲覧できるフィードのようなエクスペリエンスを維持できるため、モバイルアプリのレコメンデーションユースケースに特に適しています。 アプリ内メッセージは、特定の行動によってトリガーされるコンテキストに沿ったレコメンデーションに使用できます（例：商品をカートに追加した後に補完的な商品を表示する）。

**重要な考慮事項：**

- [!DNL Mobile SDK]は、関連するインタラクションの行動イベント トラッキングで設定する必要があります
- コンテンツカードは、永続的なレコメンデーションサーフェスを提供します。アプリ内メッセージは一時的なものです
- オフライン動作トラッキングでは、イベント送信の遅延にSDK キュー管理が必要です
- アプリストアの更新サイクルは、レコメンデーションレンダリングの変更をデプロイできる速度に影響します

**利点：**

- アプリが統合されたスムーズなレコメンデーションレンダリングにより、ネイティブなモバイル体験を実現します
- コンテンツカードは、永続的で閲覧可能なレコメンデーションフィードを提供し
- アプリ内メッセージにより、コンテキストに即した行動をトリガーにしたレコメンデーションが可能になります
- デバイスレベルのシグナル（場所、アプリの使用パターン）を活用して、関連性を高めます

**制限：**

- [!DNL Mobile SDK]統合とアプリ開発リソースが必要です
- レンダリングの変更にはアプリの更新が必要です（サーバー駆動型レイアウトでコードベースのエクスペリエンスを使用する場合を除く）
- オフライン期間は、行動シグナルの収集にギャップを生む

**Experience League:**

- [モバイル SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [プッシュ通知チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### オプション C：電子メールによる行動レコメンデーション

**最適な用途：**&#x200B;電子メールキャンペーンの商品レコメンデーション – 見た商品レコメンデーション、購入後のクロスセル電子メール、定期的な「おすすめ」ダイジェスト、パーソナライズされた商品レコメンデーションを含むリエンゲージメントメールを使用して、放棄された電子メールを参照します。

**仕組み：**

以前のセッションから収集された行動プロファイルデータは、メールの送信時間やレンダリング時間にレコメンデーションの選択に反映されます。 オーディエンスは、適切な受信者（例：閲覧したものの購入しなかった訪問者、最近購入した顧客）をターゲットにするように定義されます。 キャンペーンやジャーニーは、レコメンデーションの配置を含むメールを送信するように設定されています。 送信時に、AJO Decisioningは、各受信者の行動プロファイルを選択戦略に照らして評価し、推奨される項目をメールコンテンツに挿入します。

このオプションは、セッション中のシグナルではなく、蓄積された行動履歴にもとづいています。 計算属性（カテゴリー親和性スコア、最近の製品閲覧、購入頻度）は、行動履歴をプロファイルレベルのシグナルに抽出し、選択戦略で効率的に評価できるため、メールのレコメンデーション品質を大幅に向上させます。

**重要な考慮事項：**

- メールレコメンデーションは、開封時間ではなく送信時間に評価されます。送信時の行動プロファイルの状態によって、レコメンデーションが決まります
- ランキング品質を向上させるために、計算属性を強くお勧めします
- メールのレンダリングの制限（JavaScriptなし、CSS限定） レコメンデーション表示形式の制限
- 設定および検証済みのメールチャネルサーフェスが必要

**利点：**

- セッションをまたいだ行動履歴を活用し、より詳細なパーソナライゼーションを実現
- 既存のキャンペーンやジャーニーのワークフローとの統合
- web/アプリの顧客接点が利用できない場合のリエンゲージメントとウィンバックに効果的です
- 1つのメールに複数のレコメンデーションの配置を含めることができます

**制限：**

- レコメンデーションは送信時に静的です。メールが開かれても更新されません
- メールレンダリングの制約により、レコメンデーションの表示形式が制限される
- オーディエンスの評価とキャンペーン/ジャーニーオーケストレーション基盤が必要
- 依存関係（チャネル設定、オーディエンス定義、キャンペーン実行）が増えるため、実装が複雑になる

**Experience League:**

- [メールの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### オプションの比較

次の表に、実装オプションの主な違いをまとめました。

| 条件 | オプション A:Web リアルタイム | オプション B：モバイルアプリ | オプション C：メール行動 |
| --- | --- | --- | --- |
| 主な用途 | web ページレコメンデーション（PDP、ホームページ、カテゴリ） | アプリ内レコメンデーションとコンテンツフィード | 商品レコメンデーション付きのメールキャンペーン |
| 行動シグナル源 | セッション内+ クロスセッション （[!DNL Web SDK]） | アプリ内インタラクション （[!DNL Mobile SDK]） | 累積行動履歴（プロファイル） |
| レコメンデーション待ち | サブ秒（[!DNL Edge Network]） | サブ秒（[!DNL Edge Network]） | 送信時（ハブサイド評価） |
| 訪問者タイプ | 匿名および既知 | 認識済み（アプリユーザー） | 既知（メール受信者） |
| 複雑 | 中 | Medium – 高 | 高 |
| チャネル依存関係 | [!DNL Web SDK]、コードベースのエクスペリエンスサーフェス | [!DNL Mobile SDK]、アプリ内/コンテンツカードサーフェス | メールチャネルサーフェス、オーディエンス、キャンペーン/ジャーニー |
| 要件定義 | [!DNL Web SDK] デプロイメント、Edge結合ポリシー | [!DNL Mobile SDK] デプロイメント、Edge結合ポリシー | メールサーフェス、オーディエンス定義、キャンペーン設定 |

### 適切なオプションの選択

次のガイダンスを参照して、状況に最適なオプションを選択してください。

- **オプション A**&#x200B;を使用して、web サイトでのリアルタイムの商品レコメンデーションを主な目標としている場合に開始します。 これは最も一般的な出発点であり、実装の複雑さが最も小さいとすぐに価値を得られます。
- **モバイルアプリが主要なエンゲージメントチャネルであり、アプリ内レコメンデーションが有意義なコンバージョン向上をもたらす場合は、オプション B**&#x200B;を選択します。 オプション Bは、同じ選択戦略と項目カタログを使用して、オプション Aと並行して実行できます。
- 行動レコメンデーションをメール キャンペーンに拡張する場合は、**オプション C**&#x200B;を追加します。 通常、オプション AまたはBの上に重ねられ、同じ商品カタログと選択戦略を使用しますが、メール固有のレンダリングテンプレートとオーディエンスベースのターゲティングが使用されます。
- **共通パターンのオプション A + C**&#x200B;を組み合わせる：アクティブな訪問者に対するリアルタイムのweb レコメンデーションに加えて、コンバージョンせずに離脱した訪問者に対する放棄された閲覧または購入後のメール レコメンデーションを追加します。

## 実装フェーズ

以下のフェーズでは、行動レコメンデーションのエンドツーエンドの実装を紹介します。

### フェーズ 1：行動イベントスキーマとデータ収集の設定

**Application Function:** AEP: Data Modeling &amp; Preparation （F2）、AEP: Data Sources &amp; Collection （F3）

このフェーズでは、行動シグナルとアイテムカタログデータを収集するXDM スキーマ、データセット、データ収集メカニズムを確立します。 このデータ基盤は、あらゆるレコメンデーションロジックの基盤となります。

#### 決定：行動イベントスキーマ設計

どの行動シグナルがレコメンデーションを促進すべきか？

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 製品ビューのみ | シンプルなクロスセル/アップセルレコメンデーション | 最も低い実装労力、限られた信号深度 |
| 製品ビュー+購入 | 購入除外とクロスセルロジックによるレコメンデーション | 中程度の労力。「購入済みを除外」フィルタリングを有効にする |
| 包括的な行動スイート（ビュー、購入、カートへの追加、検索、コンテンツインタラクション） | マルチシグナルランキングによる高度なレコメンデーション | 最高の信号品質。包括的な[!DNL Web SDK]/[!DNL Mobile SDK]実装が必要です |

#### 決定：品目カタログ取得方法

商品カタログまたはコンテンツカタログは、AEPにどのように取り込まれますか？

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| ソースコネクタによるバッチ取り込み | カタログの更新は定期的（日次/週次）です | 設定がシンプルで、カタログの変更がリアルタイムに反映されない |
| ストリーミング取り込み | カタログは、ほぼリアルタイムの更新が必要（価格変更、可用性） | より複雑：現在の在庫を反映したレコメンデーションを提供 |
| 手動/API アップロード | 変更頻度の低い小さいカタログ | 最もシンプルなセットアップ。大規模または動的なカタログには対応できない |

**UI ナビゲーション：** データ管理/ スキーマ / スキーマの作成；データ収集/ データストリーム / 新規データストリーム

**キー設定の詳細：**

- Experience Event スキーマには、イベントペイロードに製品/項目識別子（SKU、製品ID、コンテンツ ID）を含める必要があります
- 商品カタログスキーマには、フィルターとランキングに使用する属性（カテゴリ、価格、画像URL、可用性ステータス、タグ）を含める必要があります
- データストリームでは、Edge決定に対して[!DNL Adobe Journey Optimizer] サービスを有効にする必要があります
- [!DNL Web SDK] `sendEvent`呼び出しには、XDM コマースフィールドにマッピングされた製品インタラクションデータを含める必要があります

**Experience League ドキュメント：**

- [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [スキーマ構成の基本](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Web SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [データストリームの設定](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [2つのスキーマ間の関係の定義](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-api)

### フェーズ 2:IDとプロファイルの設定

**Application Function:** AEP: Identity &amp; Profile Configuration （F4）

この段階では、ID名前空間、プライマリ ID指定、マージポリシーを設定し、行動シグナルが訪問者プロファイルに正しく関連付けられ、リアルタイムのレコメンデーション配信に利用できるようにします。

#### 決定：Edge決定の結合ポリシー

このレコメンデーションユースケースには、リアルタイムのEdge評価が必要ですか？

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| Edge結合ポリシーでアクティブ | オプション AとB （webおよびモバイルのリアルタイムのレコメンデーション） | 1秒間のレコメンデーション配信に必要。サンドボックスごとに1つのEdge結合ポリシーのみ |
| 標準の結合ポリシー（Edgeを使用しない） | オプション Cのみ（送信時に評価される電子メールレコメンデーション） | ハブサイド評価に十分です。Edge結合ポリシースロットを使用しません。 |

#### 決定：匿名と既知の訪問者ID

匿名の訪問者からの行動シグナルはどのように処理すべきですか？

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| ECIDのみ（匿名） | セッション内の行動に基づく、主に匿名訪問者向けのレコメンデーション | 設定がシンプル。訪問者が認証しない限り、クロスセッションの継続性はありません |
| ECID +認証済みID （CRM ID、メール） | IDをつなぎ合わせた既知の訪問者に対するクロスセッションレコメンデーション | より豊富な行動プロファイル。認証フローが必要 |
| ID グラフのリンク付きの両方 | IDをつなぎ合わせた、匿名から既知のジャーニー | 最も包括的。ID リンクルール設定が必要です |

**UI ナビゲーション：** ID/ID名前空間、プロファイル/結合ポリシー

**キー設定の詳細：**

- ECID名前空間は事前設定されており、[!DNL Web SDK]および[!DNL Mobile SDK]によって自動的に使用されます
- 認証されたID用にカスタム ID名前空間（CRM ID、ロイヤルティ ID）を作成する必要があります
- Experience Event スキーマのプライマリ IDは、web/モバイル行動イベントのECIDにする必要があります
- 結合ポリシーは、デバイス間でIDをつなぎ合わせるためにプライベートデバイスグラフを使用する必要があります

**Experience League ドキュメント：**

- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID名前空間の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/namespaces)
- [結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [ID グラフのリンクルール](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)

### フェーズ 3：商品カタログと選択戦略の設定

**アプリケーション関数：** AJO：決定

このフェーズでは、アイテムのカタログ（決定項目）、行動シグナルとアイテム属性を組み合わせた選択戦略のランキング、対象外のアイテムを除外するフィルタリングルール、コールドスタートプロファイルのフォールバックレコメンデーションが設定されます。

#### 決定：品目カタログ範囲

推奨事項にはどのような項目がありますか？

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 商品カタログ（e コマース） | 物理的な商品やデジタル商品の購入を勧める | 品目属性には、価格、カテゴリー、在庫状況、画像などが含まれます |
| コンテンツカタログ（メディア/公開） | おすすめの記事、動画、教育コンテンツ | 項目属性には、トピック、作成者、公開日、コンテンツタイプなどがあります |
| ハイブリッドカタログ | 商品とコンテンツの両方をレコメンデーション | 両方のタイプに対応する統合アイテムスキーマが必要 |

#### 決定：ランキングアプローチ

最適なレコメンデーションを決定するために、適格なアイテムをどのようにランク付けする必要がありますか？

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| フォーミュラベースのランキング | ランキングに対する明確なビジネスロジック（例：カテゴリー親和性スコアをアイテムの人気度で割ったソート） | 透明性のある監査可能なランキング。定義されたランキング式が必要 |
| AI ランキング（自動最適化） | マシンラーニングは、コンバージョンデータにもとづいて最適なランキングを決定する必要があります | モデルのトレーニングには最低1,000回のコンバージョンイベントが必要ですが、透明性は低い |
| 優先度ベース（手動） | 手作業でキュレーションしたシンプルなレコメンデーション注文 | 設定が簡単で、個々の動作に適応しない |

#### 決定：ルールのフィルタリング

どの項目を推奨事項から除外する必要がありますか？

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 既に購入済みの商品を除外 | クロスセルと発見の推奨事項 | 行動プロファイルに購入履歴が必要です |
| 在庫切れ商品の除外 | ダイナミック在庫機能を備えたコマース | カタログをリアルタイム、またはほぼリアルタイムで更新する必要がある |
| 以前に却下された項目を除外 | ユーザーが提案を却下できるコンテンツのレコメンデーション | 行動イベントでの却下トラッキングが必要です |
| カテゴリ範囲のフィルタリング | 特定のカテゴリーに限定されたレコメンデーション | 項目の属性をフィルタリングに使用します |

#### 決定：コールドスタート戦略

行動履歴がない新規訪問者には何を表示すべきですか？

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 人気アイテム（グローバルベストセラー） | 汎用フォールバック | 維持しやすい、パーソナライズされていない |
| カテゴリー別の人気商品 | 訪問者がカテゴリ ページに到達しました | コンテキストに関連したフォールバック。ページコンテキストが必要です |
| 厳選されたエディトリアルピック | 企業は、コールドスタート体験をエディトリアルで管理したい | 手動でのキュレーションと更新が必要 |
| トレンド項目（時間重み付けされた人気度） | 現在のトレンドを反映した動的なフォールバック | トレンド信号の計算が必要 |

**UI ナビゲーション：** [!DNL Journey Optimizer] > コンポーネント >意思決定管理>決定；[!DNL Journey Optimizer] > コンポーネント >意思決定管理> オファー；[!DNL Journey Optimizer] > コンポーネント >意思決定管理>配置

**キー設定の詳細：**

- カタログ内の各製品またはコンテンツ項目を、属性（カテゴリ、価格、画像URL、タグ）で表す決定項目を作成します
- 商品カタログフィルタリングと行動ランキングロジックを組み合わせた選択戦略を定義します
- ランキングモデルの設定：数式ベースの式は、プロファイル属性（計算属性からのカテゴリ親和性スコアなど）を参照できます
- コールドスタートプロファイルのデフォルトのレコメンデーションとして機能するフォールバックオファー/アイテムを作成する
- 論理グループ化にコレクション修飾子（タグ）を使用して、アイテムをコレクションに整理します
- ビジネスルールを適用するために、選択戦略内にフィルタリングルールを設定します（購入済みの場合は除外、在庫のみ）

**Experience League ドキュメント：**

- [意思決定管理の概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [プレースメントの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [決定ルールの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [パーソナライズされたオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [フォールバックオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [コレクションの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [決定を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [ランキング戦略](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### フェーズ 4: チャネルとサーフェスの設定

**Application Function:** AJO: Channel Configuration

このフェーズでは、レコメンデーションがレンダリングされる配信サーフェスを設定します。 設定は、実装オプションによって大きく異なります。

#### 決定：配信サーフェスのタイプ

レコメンデーションはどこに表示されますか？

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| コードベースの体験（web） | カスタムレンダリング機能を備えたweb ページ上のレコメンデーションウィジェット | レンダリングに最大限の柔軟性を提供。フロントエンド開発が必要 |
| web チャネルサーフェス | 標準web パーソナライゼーションサーフェス | AJO web デザイナーを使用しています。コードベースよりも柔軟性が低い |
| アプリ内メッセージ | アプリの行動によってトリガーされるコンテキストに関する推奨事項 | エフェメラル；相互作用または解任後に消える |
| コンテンツカード（モバイル） | モバイルアプリの永続的なレコメンデーションフィード | ユーザーがアクションするまで保持。閲覧可能なフィードのエクスペリエンス |
| 電子メール | メールキャンペーンに組み込まれた商品レコメンデーション | 送信時の静的な値。電子メールレンダリングの制約に従う |

**オプションが異なる場所：**

**オプション A （Web リアルタイム レコメンデーション）の場合：**
コードベースのエクスペリエンスサーフェスまたはweb チャネルサーフェスを設定します。 コードベースのエクスペリエンスは、カスタムレコメンデーションレンダリング（カルーセル、グリッド、アイテムカード）に最も柔軟な機能を提供します。 サーフェス URIは、ページ上のレコメンデーションが表示される場所を識別します。

**オプション B （モバイルアプリのレコメンデーション）の場合：**
アプリ内メッセージまたはコンテンツカードサーフェスを設定します。 コンテンツカードは、永続的なレコメンデーションフィードに使用することをお勧めします。 アプリ内メッセージは、コンテクストに即して行動をトリガーにしたレコメンデーションに適しています。

**オプション C （電子メールの行動レコメンデーション）の場合：**
サブドメインのデリゲーション、IP プールの割り当て、送信者の設定を使用して、メールチャネルサーフェスを設定します。 サーフェスの配信品質が検証されていることを確認します。

**UI ナビゲーション：**&#x200B;管理/ チャネル / チャネルサーフェス / サーフェスを作成

**Experience League ドキュメント：**

- [チャネルサーフェスの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [SMS チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [プッシュ通知チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### フェーズ 5：コンテンツと配信の設定

**アプリケーション関数：** AJO: メッセージ オーサリング

このフェーズでは、訪問者に推奨される項目の表示方法を制御する、推奨レンダリングテンプレートを定義します。 これには、アイテムレイアウトデザイン、アイテム属性（名前、画像、価格、リンク）を引き出すパーソナライゼーション表現、全体的なレコメンデーションエクスペリエンスデザインが含まれます。

#### 決定：レコメンデーション表示形式

推奨アイテムはどのようにレンダリングする必要がありますか？

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| カルーセル（水平スクロール） | 垂直方向のスペースが限られているホームページまたはカテゴリーページ | 使い慣れたUX パターン。コンパクトなスペースに複数のアイテムを表示 |
| グリッド （複数行） | 十分なスペースを備えた専用のレコメンデーションセクション | 一度に多くの項目を表示します。「おすすめ」セクションに適しています |
| 単一アイテムウィジェット | 特定のページの場所（サイドバーなど）でのコンテキストに関する推奨事項 | フットプリントを最小限に抑え、高い効果を発揮 |
| インラインメールブロック | メール本文に埋め込まれたレコメンデーション | 電子メール HTML/CSSの制約事項の対象。通常は2～4項目 |

#### 決定：表示する推奨事項の数

プレースメントあたりの決定返すアイテム数

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 3～4点 | 標準レコメンデーションウィジェット | 関連性と視覚的密度のバランス |
| 6～8項目 | スクロールまたはグリッドレイアウト付きのカルーセル | 訪問者に対するオプションの増加。十分なカタログの深さが必要 |
| 1項目 | コンテキストに沿った単品レコメンデーション | 最も高い関連性の影響、最もシンプルなレンダリング |
| 10以上の項目 | フィード形式のレコメンデーション体験 | コンテンツ集約的なユースケース（メディア、公開） |

**オプションが異なる場所：**

**オプション A （Web リアルタイム レコメンデーション）の場合：**
コードベースのエクスペリエンステンプレートを使用して、レコメンデーションレンダリングをデザインします。 HTML/CSS/JavaScriptを使用して、カルーセル、グリッドまたはウィジェットのレイアウトを作成します。 Personalizationの式は、決定応答属性（項目名、画像URL、価格、商品URL）を参照します。 インプレッションとクリックの追跡は、[!DNL Web SDK]によって自動的に処理されます。

**オプション B （モバイルアプリのレコメンデーション）の場合：**
アイテム表示ロジックを使用して、コンテンツカードやアプリ内メッセージのテンプレートを設定できます。 モバイルアプリがネイティブにレンダリングする、JSON ベースのコンテンツ構造を使用できます。 おすすめアイテムごとにディープリンクを含めます。

**オプション C （電子メールの行動レコメンデーション）の場合：**
Email Designerを使用したメールコンテンツのデザイン。 決定機能を活用したコンテンツブロックを使用して、レコメンデーションの配置を挿入。 メールテンプレート内の項目属性に対してパーソナライゼーション式を設定します。 件名のパーソナライズは、最も推奨される項目を参照できます。

**UI ナビゲーション：** コンテンツ管理/ コンテンツテンプレート；キャンペーン/ジャーニー/ コンテンツを編集/ メールDesigner

**キー設定の詳細：**

- 各レコメンデーションは、フェーズ 3で作成された決定を参照する必要があります
- Personalization式では、Handlebars構文を使用して項目属性をレンダリングします
- Webの場合：決定を呼び出し、応答をレンダリングするようにコードベースのエクスペリエンスを設定します
- メールの場合：キャンペーンまたはジャーニー内のメールアクションに決定を埋め込みます
- 既知の行動履歴を持つテストプロファイルを使用して、推奨事項をプレビューします

**Experience League ドキュメント：**

- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalizationの構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [コンテンツのプレビューとテスト](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### フェーズ 6：オーディエンスの範囲とキャンペーン/ジャーニーを設定する（オプション Cのみ）

**Application Function:** RT-CDP: Audience Evaluation, AJO: Campaign ExecutionまたはJourney Orchestration

メールベースのレコメンデーション（オプション C）の場合、このフェーズでは、ターゲットオーディエンスを定義し、レコメンデーションメールを配信するキャンペーンまたはジャーニーを設定します。 オプション AとBでは、ページ/画面の読み込み時にレコメンデーションがリアルタイムで配信されるため、このフェーズをスキップします。

#### 決定：オーディエンス評価方法

レコメンデーションメールのターゲットオーディエンスはどのように評価すべきですか？

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| バッチ評価 | スケジュールされたレコメンデーションメールキャンペーン（毎日、毎週のダイジェスト） | 予測可能な送信タイミング、送信前にオーディエンスを評価 |
| ストリーミング評価 | イベントトリガーのレコメンデーションメール（放棄された閲覧、購入後） | ほぼリアルタイムのオーディエンスの選定：ジャーニーオーケストレーションと組み合わせ |

#### 決定：配信メカニズム

メールはキャンペーンまたはジャーニーを通じて配信すべきですか？

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 予定キャンペーン | 定義されたオーディエンスに対して、1回限りまたは定期的に配信するレコメンデーションメール | 容易な設定、バッチオーディエンスの評価および送信 |
| ジャーニーとオーディエンス入力 | オーディエンスの選定によってトリガーされる継続的なレコメンデーションメール | マルチステップのフローを有効にします（例：レコメンデーションメールの後にリマインダー）。 |
| イベントトリガージャーニー | 特定のイベントによってトリガーされたレコメンデーションメール（閲覧の放棄、購入） | リアルタイムのトリガー：イベントベースのジャーニー入力が必要 |

**UI ナビゲーション：**&#x200B;お客様/オーディエンス/オーディエンスを作成/ルールを作成；キャンペーン/キャンペーンを作成；ジャーニー/ジャーニーを作成

**キー設定の詳細：**

- 行動履歴を参照するセグメントルール式（例：「過去7日間に閲覧したが購入していない商品」など）を使用して、ターゲットオーディエンスを定義します
- フェーズ 4からチャネルサーフェスを参照するメールアクションで、キャンペーンまたはジャーニーを設定します
- フェーズ 3の決定をメールコンテンツに埋め込みます
- 過剰なメッセージを避けるために、スケジュール設定と頻度ルールを設定する

**Experience League ドキュメント：**

- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [キャンペーンのライブレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)

### フェーズ 7：レポートと最適化の設定

**Application Function:** AJO: Reporting &amp; Performance Analysis, S5: Reporting &amp; Analysis

この段階では、レコメンデーションのクリックスルー、コンバージョン、収益指標などに関するパフォーマンスモニタリングを確立します。 レポート機能を構築して、レコメンデーションの効果を測定し、最適化の機会を特定できます。

#### 決定：レポートの深さ

必要なレポート分析のレベル？

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| AJO ネイティブレポートのみ | 基本的なレコメンデーションのパフォーマンスモニタリング | クイックセットアップ（AJOで追跡される指標に限定） |
| AJO + [!DNL Customer Journey Analytics]統合 | クロスチャネルのレコメンデーションの影響分析と収益アトリビューション | [!DNL Customer Journey Analytics]接続とデータビューが必要です。より詳細なインサイトを提供します |
| カスタムダッシュボード付きの完全な[!DNL Customer Journey Analytics] ワークスペース | アイテムレベル、セグメントレベル、表面レベルの分析を用いた継続的な最適化プログラム | 最も包括的です。[!DNL Customer Journey Analytics]の専門知識とセットアップが必要です |

**UI ナビゲーション：** キャンペーン/キャンペーンを選択/すべての時間レポート、ジャーニー/ジャーニーを選択/すべての時間レポート、[!DNL Customer Journey Analytics]/プロジェクト/新しいプロジェクトを作成

**キー設定の詳細：**

- AJOのキャンペーンとジャーニーレポートで、配信とエンゲージメント指標を確認します
- [!DNL Customer Journey Analytics]統合の場合は、AJO エクスペリエンスイベント データセット（Message Feedback、Email Tracking、Decisioning）を含む接続を作成します
- レコメンデーション固有のディメンション（項目名、項目カテゴリ、レコメンデーションサーフェス）と指標（インプレッション数、クリック数、コンバージョン数、収益）を含む[!DNL Customer Journey Analytics] データビューを作成します
- レコメンデーションのCTR、コンバージョン率、インプレッションあたりの売上に関する計算指標を構築します
- サーフェス、セグメント、期間をまたいでレコメンデーションパフォーマンスを比較する[!DNL Customer Journey Analytics] ワークスペースパネルを作成します

**Experience League ドキュメント：**

- [キャンペーングローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [接続の作成または編集](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [データビューの作成または編集](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [計算指標の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

## 実装に関する考慮事項

導入前と導入中に、次のガードレール、落とし穴、ベストプラクティス、トレードオフを確認しましょう。

### ガードレールと制限

- サンドボックスごとに最大10,000件の承認済みパーソナライズされたオファー（決定項目） — [意思決定管理ガードレール &#x200B;](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- 1決定あたり最大30件のプレースメント
- 決定リクエストごとに最大30個のコレクションスコープ
- オファーの配信時間SLA：シングルスコープのEdge リクエストの場合、P95で500 ミリ秒未満
- AI ランキングモデルのトレーニングには最低1,000回のコンバージョンイベントが必要です
- オファーキャッピングカウンターは、高スループットのシナリオで最大で数秒の遅延が発生する場合があります
- Edgeの決定は、edge profile storeで使用可能なプロファイル属性に制限されます
- サンドボックスごとにEdgeでアクティブにできる結合ポリシーは1つだけです – [&#x200B; プロファイルガードレール &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- サンドボックスあたり最大25個のアクティブな計算属性 – [計算属性ガードレール &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- サンドボックスごとに最大4,000個のセグメント定義 – [&#x200B; セグメント化ガードレール &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- ストリーミング取り込み：HTTP接続あたり1秒あたり最大20,000 レコード — [取り込みガードレール &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### よくある落とし穴

- **決定では、フォールバック項目のみが返されます。** パーソナライズされた決定項目が、有効期限範囲内で承認され、実施要件ルールが訪問者のプロファイル属性と一致することを確認します。 上限に達していないことを確認します。
- **Edge delivery returns empty personalization:** データストリームが[!DNL Adobe Journey Optimizer] サービスを有効にして設定されており、決定範囲が[!DNL Web SDK] リクエストで正しくフォーマットされていることを確認します。
- **ランキング式が適用されていません：**&#x200B;数式が構文的に有効であり、アクセス可能なプロファイル属性を参照していることを確認してください。 数式エラーはサイレントに優先順位ベースのランキングにフォールバックされます。
- **古いレコメンデーション：**&#x200B;行動イベントデータがリアルタイムで流れていない場合、古い行動プロファイルに基づいたレコメンデーションが行われます。 [!DNL Web SDK]または[!DNL Mobile SDK]がアクティブにストリーミングイベントであることを確認します。
- **コールドスタートのフォールバック率が高すぎます：**&#x200B;訪問者の大部分がフォールバックのレコメンデーションを受け取る場合、行動履歴のみに依存するのではなく、コンテキストシグナル（現在のページカテゴリ、リファラルソース）を使用してコールドスタート戦略を強化することを検討してください。
- **推奨事項がページ上でレンダリングされません：** コードベースのエクスペリエンスサーフェス URIがページ URL パターンと一致し、[!DNL Web SDK]が決定応答を正しく要求およびレンダリングしていることを確認してください。
- **レコメンデーションにカタログ項目が見つかりません：**&#x200B;すべてのカタログ項目が決定項目として取り込まれ、正しいコレクション修飾子でタグ付けされ、選択戦略で参照される適切なコレクションに含まれていることを確認します。

### ベストプラクティス

- AIでランク付けされたモデルに投資する前に、計算属性（カテゴリーの親和性、インタラクションの最新性）を使用して、数式ベースのランキングモデルから開始します。 フォーミュラベースのモデルは透明性があり、監査可能であり、比較のための確かなベースラインを提供します。
- インプレッションとクリックの追跡を初日から実装できます。 インタラクションデータがなければ、AI ランキングモデルはトレーニングできず、レコメンデーションの効果を測定することもできません。
- 複数のレコメンデーションサーフェス（ホームページ、PDP、電子メール）ごとに個別の選択戦略を作成できます。これにより、あらゆるチャネルで戦略を再利用できます。 サーフェスごとにユーザーインテントが異なります。
- 計算属性を使用して、行動履歴をランキングシグナルに抽出します。 生のイベントデータは詳細すぎて、フォーミュラベースのランキングを効果的に行うことはできません。「カテゴリーの親和性スコア」や「最後の購入からの日数」などの集計シグナルの方が効果的です。
- パーソナライズされたレコメンデーションとは別に、フォールバックレコメンデーションをテストできます。 フォールバック項目は、新規訪問者に優れた体験を提供する、ブランドに適した高品質なデフォルトにします。
- コールドスタートのフォールバック率を主要な健全性指標として監視する。 フォールバック率が時間の経過とともに低下している場合、行動のカバー率が増加していることを示しています。
- メールのレコメンデーションでは、行動プロファイルが最も完成したタイミング（例：閲覧時間のピーク後、送信中ではない）で送信スケジュールを設定します。

### トレードオフの決定

以下のトレードオフは、それぞれの企業の固有の要件にもとづいて評価する必要があります。

#### リアルタイムのシグナルと履歴の蓄積

セッション内の行動シグナルは、関連性は直ちに示されますが、深度は限られます。 行動履歴の蓄積により、詳細な情報が得られますが、陳腐化する可能性があります。 こうした情報源のバランスがレコメンデーションの品質に影響します。

- **オプション Aのユーザーは、既知の訪問者に対する累積履歴を補足して、即座に関連するリアルタイム シグナルを**&#x200B;好みます
- **オプション Cのお気に入り：**&#x200B;電子メールは非同期で送信されるため、蓄積された履歴のみ
- **推奨事項：** webとモバイル（オプション A、B）の場合、セッション内のシグナルを、過去の行動から得られた計算属性と組み合わせます。 メールの場合（オプション C）、行動履歴を実用的なプロファイルレベルのシグナルに要約する、計算された属性に多額の投資をおこないます。

#### フォーミュラベースモデルとAI ランクモデルの比較

フォーミュラベースのランキングは、透明性が高く、すぐに反映されます。 AIを利用してランク付けされたモデルは自動的に適応しますが、トレーニングに必要なデータが不足しており、ランキングに関する意思決定の可視性が低くなっています。

- **フォーミュラベースの利点：**&#x200B;透明性、監査可能性、即時のデプロイメント、ランキングロジックに対するきめ細かいビジネス管理
- **AIによる優先度：**&#x200B;自動化された最適化、明らかでないパターンの検出、手動での調整作業の削減
- **推奨事項：** パフォーマンスのベースラインを確立し、コンバージョンデータを蓄積するために、数式ベースのランキングで開始します。 十分なトレーニングデータ（1,000以上のコンバージョンイベント）があり、手作業による数式調整で実現できる以外にも最適化したい場合は、AI ランクモデルに移行します。

#### レコメンデーションのカバー範囲と関連性の比較

商品カタログを拡張し、フィルタリングルールを緩和することで、パーソナライズされたレコメンデーションを受け取るリクエストの割合は増加しますが、レコメンデーションごとの関連性は減少する可能性があります。

- **高いカバレッジの好意：** パーソナライズされたレコメンデーションを表示する訪問者の数を最大化します。主な目標がエンゲージメントの場合に役立ちます
- **関連性の高いお気に入り：**&#x200B;より多くの訪問者にフォールバックレコメンデーションが表示される場合でも、関連性の高い項目のみを表示します。主な目標がコンバージョンの場合に役立ちます
- **推奨事項：**&#x200B;中程度のフィルタリング（購入済み商品、在庫切れ商品を除く）を開始して、フォールバック率とコンバージョン率の両方を監視します。 コンバージョンデータがサポートしている場合にのみ、フィルタリングルールを強化します。

#### Personalizationの深さと導入の複雑さ

より豊かな行動シグナルと、より洗練されたランキングモデルは、レコメンデーションの品質を向上させますが、実装の複雑さやメンテナンスの負担を増やします。

- **実装を簡素化：**&#x200B;価値実現までの時間を短縮し、メンテナンスを減らし、デバッグと反復を容易にする
- **より詳細なパーソナライゼーションの支持：** コンバージョン率の向上、顧客体験の向上、競争上の差別化
- **推奨事項：**&#x200B;段階的に実装する。 製品ビューシグナルとフォーミュラベースのランキング（フェーズ 1）から始めます。 行動エンリッチメントの計算属性の追加（フェーズ 2）。 基盤が成熟し、十分なトレーニングデータが利用可能になったら、AIを活用してランクモデルを評価します（フェーズ 3）。

## 関連ドキュメント

次のリソースでは、このパターンで使用されるテクノロジーと機能に関する追加の詳細を示します。

### 意思決定管理

- [意思決定管理の概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [プレースメントの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [決定ルールの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [パーソナライズされたオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [フォールバックオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [コレクションの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [コレクション修飾子の作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [決定を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [ランキング戦略](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Edge Decisioning APIを使用したオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)

### データ収集とWeb/Mobile SDK

- [Web SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Web SDKのインストール](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [モバイル SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [データストリームの設定](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Edge Network Server APIの概要](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### XDMとデータモデリング

- [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [スキーマ構成の基本](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [データセットの作成](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/create)
- [2つのスキーマ間の関係の定義](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-api)

### IDとプロファイル

- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID名前空間の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/namespaces)
- [結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [リアルタイム顧客プロファイルの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### オーディエンスとセグメンテーション

- [セグメント サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [エッジセグメント化](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### 計算属性とプロファイルエンリッチメント

- [計算属性の概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [計算属性UI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Customer AIの概要](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### チャネル設定

- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [チャネルサーフェスの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [サブドメインをデリゲート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)

### メッセージのオーサリングとパーソナライゼーション

- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalizationの構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### レポートと分析

- [キャンペーングローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [CJAの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [計算指標の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

### データガバナンスとライフサイクル

- [データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [データ使用状況ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview)
- [高度なデータライフサイクル管理の概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [データセットの有効期限](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration)

### 監視と監視

- [Observability Insightsの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
- [アラートの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)

### ガードレール

- [Journey Optimizerのガードレール](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [リアルタイムの顧客プロファイルのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [取り込みのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- [ID サービスのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)

### チュートリアルとガイド

- [ソースの概要](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [タグの概要](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
- [同意と環境設定のフィールドグループ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
