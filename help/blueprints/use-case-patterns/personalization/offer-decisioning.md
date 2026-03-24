---
title: Offer Decisioning
description: 一元化された意思決定ロジックを使用して、チャネルをまたいでプロファイルに最適なオファーやコンテンツを選択する方法を説明します。
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 8fd511b3-0200-41bf-aff1-e3f2a00a578e
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '8026'
ht-degree: 2%

---

# オファー決定支援

このガイドでは、[!DNL Adobe Journey Optimizer] （AJO） Decisioningと[!DNL Adobe Real-Time Customer Data Platform] （RT-CDP）を使用したオファー決定の包括的な実装リファレンスを提供します。 これは、チャネルをまたいで各顧客プロファイルに次善のオファーを決定する、一元化されたオファー選択ロジックを実装する必要がある、ソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

このガイドでは、設定すべき内容、選択肢の場所、各決定に適用されるトレードオフについて説明します。

このパターンは、「何を示すべきか」という決定を「どこで示すべきか」というチャネルロジックから切り離し、メール、web、モバイルアプリなどの顧客接点をまたいで、一貫性のある最適化されたオファー選択を可能にします。 AJO Decisioningは、オファーの作成とカタログ管理、適格性ルール（各オファーを表示できる担当者）、ランキング戦略（適格なオファーの選択方法）、プレースメント（オファーが表示される場所）、意思決定ポリシー（すべてをまとめる）など、オファーのライフサイクル全体を管理します。

## ユースケースの概要

企業は、多くの場合、顧客とのやり取りにおいて、各顧客に対して最も関連性の高いオファー、プロモーション、インセンティブを提供する必要があります。 電子メールキャンペーン、web サイトのホームページ、モバイルアプリ、マルチステップのジャーニーの意思決定段階など、顧客が誰で、何に適格か、望ましい成果を上げる可能性が最も高いオファーにもとづいて、利用可能なオプションカタログから最適なオファーを選択するという課題は同じです。

Offer Decisioningは、すべてのオファー選択ロジックをAJOの意思決定管理エンジンに一元化することで、この問題に対処します。 決定エンジンは、オファーの割り当てを個々のキャンペーンやチャネルにハードコーディングするのではなく、各プロファイルの属性、オーディエンスメンバーシップ、文脈的シグナルを評価し、最適なオファーをリアルタイムで決定します。 この一元管理により、顧客がどのチャネルを通じてエンゲージしても、同じ顧客が一貫性のある最適化されたオファーを受け取ることができます。

このパターンは、スコープにおける既知の訪問者のweb/アプリのパーソナライゼーションとは異なります。オファーの決定は、チャネルに依存せず一元化されていますが、既知の訪問者のパーソナライゼーションは、デジタルサーフェスのパーソナライゼーションに重点を置いています。 カタログモデルにおける行動レコメンデーションとは異なります。対象となる商品セットが、ビジネスルール、適格性の制約、規制要件（プロモーション、金融商品、インセンティブ）などによって管理される場合に、オファー決定機能を使用します。 アイテムセットが大規模で継続的に変化し、行動の類似性や親和性のシグナル（製品カタログ、コンテンツライブラリ）によって選択が決定される場合は、行動レコメンデーションを使用します。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

**[パーソナライズされた顧客体験の提供](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
個人の好み、行動、ライフサイクルのステージに合わせて、コンテンツ、オファー、メッセージを調整。
**KPI:** エンゲージメント、コンバージョン率、顧客満足度（CSAT）

**[クロスセルとアップセルの収益を促進](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
行動や購入履歴にもとづいて、既存顧客に補完的な商品やサービスを宣伝します。
**KPI:** アップセル/クロスセル %、増分収益、顧客生涯価値

**[顧客ロイヤルティと生涯価値の向上](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
ロイヤルティプログラム、特典、パーソナライズされたエンゲージメントを通じて、顧客関係を深化し、長期的な価値を最大化します。
**KPI:**&#x200B;顧客のライフタイムバリュー、リテンション、アップセル/クロスセル %

## 戦術的なユースケース

次のシナリオは、オファー決定を実際にどのように適用できるかを示しています。

- メール施策で「次善のオファー」を活用：送信時に、受信者ごとに最も関連性の高いプロモーションを選択します
- web サイト上のリアルタイムのプロモーションバナー：意思決定機能では、訪問者のプロファイルにもとづいて、ページ読み込み時にオファーを選択します
- ユーザーのライフサイクル段階に最適なインセンティブを提供する、パーソナライズされたアプリ内カード
- クロスチャネルのオファーの一貫性 – 同じ意思決定ロジックで電子メール、web、プッシュ通知を提供し、顧客が統一されたオファー体験を目にできるようにします
- 顧客価値の階層にもとづく動的なクーポンまたは割引の選択（価値の高い顧客にプレミアムオファーを提供するなど）
- 現在のサブスクリプションレベルに基づいて、製品のアップグレードまたはアップセルオファーを選択
- ロイヤルティ報酬：層とアクティビティ履歴にもとづいてパーソナライズされたオファー

## 主要業績評価指標

次のKPIは、オファー決定実装の有効性を測定するのに役立ちます。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| オファーの承認率 | クリック、引き換え、コンバージョンにつながる配信されたオファーの割合 | オファークリック数/引き換え数/配信されたオファー数 |
| オファーの選択の配布 | あらゆる意思決定で選択された各オファーの割合 | オファーあたりのカウント / レンダリングされた決定合計 |
| フォールバック率 | パーソナライズされたオファーが選定されず、フォールバックが提供された意思決定の割合 | フォールバックインプレッション数/総意思決定数 |
| コンバージョン率 | 目的のアクション（購入、サインアップ、引き換え）を完了したオファー受信者の割合 | コンバージョン/オファーインプレッション |
| 売上増加 | 選択したオファーとコントロールグループまたはフォールバックの決定に起因する売上 | パーソナライズされたオファーからの収益 – フォールバック/コントロールからの収益 |
| クロスチャネルの一貫性スコア | 定義されたウィンドウ内で複数のチャネルにわたって同じオファーを受け取るプロファイルの割合 | 一貫性のあるオファー/マルチチャネルのインプレッション数 |
| オファークリックスルー率 | クリックにつながるオファーインプレッションの割合 | オファークリック数/オファーインプレッション数 |

## ユースケースパターン

この節では、オファー決定の関数チェーンとパターン定義について説明します。

**オファー決定**

一元化された意思決定ロジックを使用して、チャネルをまたいでプロファイルに最適なオファーやコンテンツを選択します。

**機能チェーン：** オーディエンス評価> オファーの適格性> ランキング戦略>決定実行>配信> レポート

各コンポジションがどのように表示されるかについては、[実装オプション ](#implementation-options)の節を参照してください。

## アプリケーション

このユースケースパターンでは、次のAdobe アプリケーションを使用します。

- **[!DNL Adobe Journey Optimizer]（AJO）** — オファー作成、適格性ルール、ランキング戦略、プレースメント、および決定ポリシー用の意思決定管理エンジン、オファー配信のチャネル設定およびメッセージのオーサリング、キャンペーンおよびジャーニーの実行
- **[!DNL Adobe Real-Time Customer Data Platform]（RT-CDP）** — オファーの適格性セグメントに対するオーディエンス評価。適格性とランキングで使用されるプロファイルデータと計算属性
- **[!DNL Adobe Experience Platform]（AEP）** — AJOとRT-CDPの両方をサポートする統合プロファイルストア、ID解決、データ基盤

## 基本関数

このユースケースパターンでは、次の基本機能を使用する必要があります。 各機能について、ステータスは、通常それが必要か、事前設定が想定されているか、適用できないかを示します。

| 基本関数 | ステータス | 整えておく必要があるもの | Experience League リファレンス |
| --- | --- | --- | --- |
| 管理とガバナンス | 同じ位置に仮定 | 決定権限が有効になっているAJO サンドボックス。 実装チームに割り当てられたオファー管理の役割（Decision Manager、Offer Approver）。 | [ サンドボックスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/sandbox/home)、[ アクセス制御の概要](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| データモデリングと準備 | 必須 | プロファイルスキーマには、オファーの適格性ルールに使用される属性（ロイヤルティ層、購入履歴、サブスクリプションタイプなど）を含める必要があります。 オファーのインプレッション、クリック、コンバージョンを追跡するためのオファー応答/インタラクションスキーマを導入する必要があります。 | [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)、[ スキーマ構成の基本](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| データソースと収集 | 同じ位置に仮定 | 実施要件ルールで使用されるプロファイル属性は、最新である必要があります。 Web配信（オプション B）の場合、Web SDKは、データストリームでAJO サービスを有効にして実装する必要があります。 メール配信の場合、プロファイル属性は送信時に解決可能である必要があります。 | [Web SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)、[ データストリームの設定](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| IDとプロファイル設定 | 同じ位置に仮定 | プロファイルは、オファーが配信されるあらゆるチャネルをまたいで解決できる必要があります。 クロスチャネルのオファーの一貫性を保つためには、統合IDが不可欠です。電子メール、web、モバイルの各コンテキストで、同じプロファイルを認識する必要があります。 リアルタイム web/アプリ配信には、エッジアクティブな結合ポリシーが必要です。 | [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)、[結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| オーディエンスの定義とセグメント化 | 必須 | オファーの適格性の基準として使用されるオーディエンスを定義および評価する必要があります（例：「価値の高い顧客」、「トライアルユーザー」、「ロイヤルティゴールドレベル」）。 評価方法は、配信待ち時間と一致する必要があります。メールキャンペーンのリアルタイム web/アプリ、バッチ、ストリーミングのエッジ評価です。 | [ セグメント化サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)、[ セグメント ビルダーUI ガイド ](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## サポート機能

次の機能は、このユースケースパターンを強化しますが、コア実行には必要ありません。

| 補助機能 | ステータス | なぜそれが重要なのか | Experience League リファレンス |
| --- | --- | --- | --- |
| 計算属性/派生属性作成 | 推奨 | Customer AIの傾向スコア、生涯価値の計算、エンゲージメント指標は、ランキング戦略の効果を大幅に向上させます。 「最後に購入してからの日数」や「90日間の総支出」などの計算属性を使用すると、より正確な適格性ルールと数式ベースのランキングが可能になります。 | [計算属性の概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)、[顧客AIの概要](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| データライフサイクル管理 | 推奨 | オファーの履歴と決定イベントデータは、時間の経過とともに蓄積されます。 オファーインタラクションイベントデータセットがストレージを管理し、データ保持要件に準拠するように、保持ポリシー（有効期限）を設定する必要があります。 | [高度なデータライフサイクル管理の概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)、[ データセットの有効期限](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| データ使用のラベル付けと適用 | 推奨 | ガバナンスラベルは、機密性の高いターゲティング基準（財務状況、健康状態など）を含むオファーが、データ利用ポリシーに準拠していることを確認します。 実施要件ルールで使用されるフィールドにラベルを付けると、準拠していないオファーのターゲティングが防止されます。 | [ データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)、[ データ使用ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview) |
| 監視と可観測性 | 推奨 | 意思決定エンジンのパフォーマンス、フォールバック率、オファーの配信の健全性を監視する必要があります。 フォールバック率が高い場合のアラートは、実施要件ルールの設定ミスやデータの鮮度の問題を示している可能性があります。 | [ アラートの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)、[Observability Insightsの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| レポートと分析 | 含まれる | オファーのパフォーマンスレポートは、ファンクションチェーンの一部です（フェーズ 7）。 CJAを利用すれば、クロスチャネルのオファー有効性の測定、売上への影響のアトリビューション、最適化の機会特定を実現できます。 | [CJAの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)、[Analysis Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home) |

## アプリケーション関数

この計画では、アプリケーション機能カタログから次の機能を実行します。 関数は、番号付きのステップではなく実装フェーズにマッピングされます。

### [!DNL Journey Optimizer] （AJO）

次の表に、AJO関数と、それらが設定される実装フェーズを示します。

| 関数 | 導入フェーズ | 説明 |
| --- | --- | --- |
| 決定 | フェーズ 3：意思決定の設定 | オファー項目の作成、適格性ルールの定義、ランキング戦略の設定、フォールバックオファーの作成、プレースメントの定義、意思決定ポリシーの構築を行います |
| チャネル設定 | フェーズ 4：チャネルとサーフェスの設定 | メール、web、アプリ内、またはコードベースのチャネルサーフェスを設定して、オファーを配信します |
| メッセージ作成 | フェーズ 5：コンテンツと配信の設定 | オファープレースメントゾーンを含むメッセージテンプレートをデザインし、web/アプリ配信用のコードベースのエクスペリエンスを設定します |
| キャンペーン実行 | フェーズ 5：コンテンツと配信の設定 | 決定ポリシーを呼び出すスケジュール済みまたはAPI トリガーのキャンペーンを実行する（オプション A） |
| コンテンツの検証 | フェーズ 5：コンテンツと配信の設定 | オプションで、異なるランキング戦略のA/B テストを実施したり、クリエイティブのバリエーションを提供したりできます |
| レポートとパフォーマンス分析 | フェーズ 7：レポートとパフォーマンスの監視 | オファーの選択分布、承認率、フォールバック率、チャネルレベルのパフォーマンスを監視します |

### [!DNL Real-Time CDP] （RT-CDP）

次の表に、RT-CDP関数と、それらが設定される実装フェーズを示します。

| 関数 | 導入フェーズ | 説明 |
| --- | --- | --- |
| オーディエンス評価 | フェーズ 2：オーディエンスの評価 | オファーの適格性ルールに使用するオーディエンスを定義および評価します。適切な評価方法（バッチ、ストリーミング、エッジ）を選択します。 |
| プロファイルエンリッチメント | フェーズ 1 （サポート）：計算属性 | ランキング戦略の効果を向上させる計算属性と傾向スコアを使用してプロファイルを強化します |

## 前提条件

実装を開始する前に、次の前提条件を満たしてください。

- [ 意思決定管理機能が有効になっている] AJO サンドボックス
- [ 意思決定管理権限を持つ] ユーザーの役割（オファー、プレースメント、決定の作成/編集）
- [ ] プロファイルスキーマには、オファーの適格性に必要な属性（ロイヤルティ層、顧客セグメント、購読レベルなど）が含まれます
- [ ] プロファイル データは最新で、適格属性の鮮度のためにアクティブに取り込まれています
- [ オプション A （電子メール）の]：検証済みサブドメインとウォーム IP プールで設定された電子メール チャネル サーフェス
- [ オプション B （Web/App）の]: Web SDKは、データストリームでAJO サービスを有効にして実装されました。エッジアクティブ結合ポリシーが設定されています
- [ オプション C （ジャーニー）の]:ジャーニーキャンバスの権限と、1つ以上のジャーニーエントリイベントまたはオーディエンスが設定されています
- [ ]各オファーとプレースメントの組み合わせごとに準備されたオファークリエイティブアセット（画像、コピー、CTA）
- [ 各プレースメント用に準備された]件のフォールバックオファーコンテンツ
- [ RT-CDPで定義および評価されたオファーの適格性ルールの] オーディエンス

## 実装オプション

この節では、オファー決定で使用できる実装オプションについて説明します。 各オプションで提供される配信チャネルとユースケースのコンテキストは異なります。

### オプション A：電子メールオファー決定

このオプションは、アウトバウンドメール施策に含めるのに最適なオファー（プロモーションメール、ニュースレターのパーソナライゼーション、動的なオファーコンテンツを備えたライフサイクルメール）を選択するのに最適です。 決定は、受信者ごとにメッセージのレンダリング時間に行われます。

#### 仕組み

電子メールメッセージのレンダリング中に決定ポリシーが呼び出され、各受信者に最適なオファーが選択されます。 メールテンプレートには、決定エンジンが選択したオファーのコンテンツ表現（画像、HTML、テキスト）を挿入するオファー配置ゾーンが含まれます。 送信時に、エンジンは各受信者のプロファイルをオファーの適格性ルールと比較して評価し、ランキング戦略を適用し、勝者オファーのコンテンツをメールに埋め込みます。

このアプローチは、スケジュールされたキャンペーン（キャンペーン実行時に評価）とジャーニーに組み込まれた電子メール（プロファイルがメッセージアクションノードに到達したときに評価）の両方で機能します。 オファーコンテンツ（画像、見出し、本文、CTA）は、決定結果にもとづいて受信者ごとにパーソナライズされます。

#### 重要な考慮事項

- オファーの実施要件は、送信時にプロファイルの現在の状態を使用して評価されます
- バッチオーディエンスの評価は、メッセージのレンダリング中に意思決定が行われるため十分です
- 各オファーには、メールの配置に対応するHTMLまたは画像コンテンツ表現が必要です
- フォールバックオファーには、使用するすべてのメール配置のコンテンツが必要です

#### 利点

- 最もシンプルな実装パス – 標準的なキャンペーンやジャーニーのメール配信を使用
- クライアントサイドのSDKは不要です
- 既存のメール基盤やチャネルサーフェスと連携
- バッチキャンペーン実行により、大量のオーディエンスをサポート

#### 制限

- 送信時に決定されます。送信後の動作に適応できません
- 電子メールが配信されると、オファーコンテンツは静的になります（リアルタイムの更新はありません）
- ハブプロファイルストアで使用可能なプロファイル属性に制限されます（エッジではありません）

#### Experience Leagueの業界トレンド

- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [キャンペーンの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

### オプション B:web/アプリのリアルタイムのオファー決定

このオプションは、web ページやモバイルアプリでのリアルタイムのオファー選択に最適です。ホームページのプロモーションバナー、アカウントダッシュボードのオファーウィジェット、アプリ内のオファーカード、ページの読み込みや画面のレンダリング時にオファーを選択する必要があるデジタルサーフェスなどです。

#### 仕組み

決定ポリシーは、Edge Decisioning ネットワークまたはコードベースのエクスペリエンスを介して、ページ読み込み時またはアプリ画面レンダリング時に呼び出されます。 訪問者がページを読み込むと、Web SDKはEdge Networkにリクエストを送信し、訪問者のエッジプロファイルをオファーの適格性ルールとランキング戦略に照らして評価します。 選択したオファーが応答で返され、デジタルサーフェス上の設定されたプレースメントでレンダリングされます。

コードベースのエクスペリエンスの場合、アプリケーションは決定応答を取得し、カスタムフロントエンドロジックを使用してオファーコンテンツをレンダリングします。 web チャネルエクスペリエンスの場合、AJO web チャネルでは、ビジュアルベースまたはコードベースのオーサリングを使用して、オファーコンテンツをページに直接挿入できます。

#### 重要な考慮事項

- データストリームでAJO サービスが有効になっているWeb SDKまたはMobile SDKの実装が必要です
- リアルタイムのプロファイル検索には、Edgeのアクティブな結合ポリシーが必要です
- 実施要件に使用されるオーディエンスは、エッジ評価（単純な属性チェックとセグメントメンバーシップ）をサポートしている必要があります
- オファーコンテンツ表現は、クライアントサイドのレンダリングにJSONまたは画像URL形式を使用する必要があります
- オファーのビューとクリック数を取得するには、インプレッション追跡を実装する必要があります

#### 利点

- 訪問者の現在のプロファイル状態にもとづいて、リアルタイムのセッション中オファー選択
- Edge Networkを介したサブセカンド決定待ち時間
- オファーは、エッジで利用可能な最新のプロファイルデータに適応します
- コンテンツの検証によるオファー戦略のA/B テストをサポート

#### 制限

- クライアントサイドのSDK実装が必要（Web SDKまたはMobile SDK）
- Edge プロファイルには、完全なハブプロファイル属性のサブセットが含まれています。複雑な適格性ルールが正しく評価されない場合があります
- Edge セグメントには、セグメントルールの複雑さの制限があります（時系列クエリはありません）
- コードベースのエクスペリエンスでカスタムレンダリングをおこなうには、フロントエンド開発が必要です

#### Experience Leagueの業界トレンド

- [Edge Decisioning APIを使用したオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [コードベースのエクスペリエンスチャネル](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based-experience/get-started-code-based)

**これが既知の訪問者のweb/アプリのパーソナライゼーション オプション B:**&#x200B;とどのように異なるか

インフラストラクチャは同じですが、どちらもWeb SDKのエッジでAJO Decisioningを使用し、エッジでアクティブな結合ポリシーを使用します。 違いは、カタログガバナンスモデルです。 このオプションは、適格性ルール、キャッピングカウンター、有効期限を含むバウンドオファーカタログを管理します。このカタログは、表示できるオファーと頻度をビジネスまたは規制の制約によって決定する場合に使用します。[既知の訪問者のweb/アプリのパーソナライゼーション ](known-visitor-web-app-personalization.md) オプション Bは、オファーのライフサイクル管理なしで、セグメントメンバーシップまたはランキング戦略を使用してコンテンツ項目から選択します。 アイテムセットが大きく、継続的に変化しており、キャッピングや適格性のガバナンスを必要としない場合は、代わりに既知の訪問者オプション Bを使用してください。

### オプション C:ジャーニーの意思決定ノード

このオプションは、マルチステップのジャーニー内のオファー選択に最適です。カスタマージャーニーの意思決定ポイントで最適なオファーを選択し、次のアクションノードを通じて配信します。 オファーの決定が、待機、条件、複数のメッセージアクションを含む、より広範なオーケストレーションフローの一部である場合に使用します。

#### 仕組み

決定ポリシーは、AJO ジャーニーキャンバス内の決定ノードから呼び出されます。 プロファイルが決定ノードに到達すると、エンジンはオファーの適格性とランキングを評価して、最適なオファーを選択します。 選択したオファーは、次のメッセージアクション（オファーの結果に基づいて、含めるコンテンツ、使用するチャネル、または取るべきジャーニーブランチ）に情報を提供します。

このアプローチにより、オファーの決定がその後のジャーニーステップに影響するアダプティブジャーニーが可能になります。 たとえば、最適なオファーを選択し、電子メールで配信してエンゲージメントを待ち、オファーが開封されなかった場合にプッシュ通知を送信することができます。

#### 重要な考慮事項

- ジャーニーは、決定ノードの後に1つ以上のメッセージアクションノードが続くように設計する必要があります
- オファーの適格性は、プロファイルが決定ノードに到達した時点でのプロファイルの状態を使用して評価されます
- 決定と配信の間のジャーニー待ちステップにより、プロファイルのステータスが変更される場合があります
- ジャーニー分岐と組み合わせて、選択したオファーに基づいて異なるパスを取得できます

#### 利点

- オファー選択をマルチステップのオーケストレーションフローに統合
- オファーの選択が後続のステップに影響するアダプティブジャーニーを有効にします
- 同じジャーニー（電子メール、プッシュ、SMS）内でのクロスチャネル配信をサポート
- オファー後のエンゲージメント追跡のためのジャーニー条件と組み合わせることができます

#### 制限

- スタンドアロンのキャンペーン決定よりも設定が複雑
- ジャーニーのスループット制限が適用されます（5,000 プロファイル/秒エントリ率）
- 決定はジャーニーのコンテキストに紐づけられる：変更にはジャーニーのバージョン管理が必要
- オファーカタログまたは意思決定ポリシーの更新を有効にするには、ジャーニーを再公開する必要があります

#### Experience Leagueの業界トレンド

- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [ジャーニーを始める](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

### オプションの比較

次の表は、3つの実装オプションを主要な基準と比較したものです。

| 条件 | オプション A：電子メール決定 | オプション B:Web/アプリリアルタイム | オプション C:ジャーニーの意思決定ノード |
| --- | --- | --- | --- |
| 主な用途 | 受信者ごとにオファーを選択するバッチメールキャンペーン | web/アプリサーフェス上のリアルタイムオファーバナー | マルチステップのオーケストレーションされたジャーニー内のオファー選択 |
| 決定待ち時間 | 送信時間（バッチレンダリング中の受信者1人当たりの秒数） | サブ秒（Edge Network） | ジャーニーノード実行時（秒） |
| チャネル | 電子メール | web、モバイルアプリ、コードベースのサーフェス | ジャーニー内のあらゆるチャネル（メール、プッシュ通知、SMS） |
| SDKが必要 | いいえ | はい（Web SDKまたはモバイルSDK） | いいえ（電子メール/プッシュの場合）。はい（web チャネルがジャーニーアクションの場合） |
| オーディエンス評価 | バッチまたはストリーミング | Edge | バッチ、ストリーミング、エッジ（ジャーニーのエントリによって異なります） |
| プロファイルデータの範囲 | 完全なハブ プロファイル | Edge プロファイル（サブセット） | 完全なハブ プロファイル |
| 複雑 | 低 | Medium – 高 | 中 |
| スループット | 高（バッチキャンペーン量） | 高（Edge Networkスケール） | Medium（ジャーニースループットの制限が適用されます） |

### 適切なオプションの選択

次のガイダンスを使用して、ユースケースに最適な実装オプションを選択します。

- **主なユースケースがアウトバウンドメール施策で受信者ごとに最適なオファーを選択しており、クライアントサイドのSDKが使用できない場合は、「オプション A**」を選択します。 最もシンプルな実装パスであり、プロモーションメール、ニュースレター、ライフサイクルキャンペーンに適しています。
- **訪問者がweb ページを読み込んだり、モバイルアプリを開いたりする瞬間にリアルタイムでオファーを選択する必要がある場合は、「オプション B**」を選択します。 これには、Web SDKまたはモバイル SDKとエッジアクティブな結合ポリシーが必要ですが、最も高速でコンテキストに沿ったオファー選択が提供されます。
- **オファーの決定が、複数の手順、待機、条件分岐を伴う、より広範なカスタマージャーニーの一部である場合は、オプション C**&#x200B;を選択します。 これは、選択したオファーが下流のジャーニーのアクションに影響を与える必要がある場合や、オファーエンゲージメントにもとづくマルチチャネルのフォローアップが必要な場合に適した選択肢です。
- オファーをチャネル全体で一貫して配信する必要がある場合、**オプションを組み合わせる**。 3つのオプションすべてで同じ決定ポリシーを使用することで、顧客が電子メール（オプション A）、web サイト（オプション B）、ジャーニーフォローアップ内（オプション C）で同じオファーを見ることができます。

## 実装フェーズ

次のフェーズでは、オファー決定のエンドツーエンドの実装シーケンスの概要を説明します。

### フェーズ 1：基盤となる前提条件を検証する

**Application function:** AEP: Data Modeling &amp; Preparation, AEP: Identity &amp; Profile Configuration

このフェーズでは、基礎データレイヤーがオファー決定をサポートしていることを検証します。 プロファイルスキーマには、オファーの適格性ルールで使用される属性を含める必要があり、ID設定でクロスチャネルのプロファイル解決を有効にする必要があります。

#### 決定：適格性のプロファイル属性

オファーの適格性ルールで使用するプロファイル属性を決定します。

>[!NOTE]
>プロファイル属性の選択は、実施要件ルールの設計とランキング戦略の有効性の両方に影響します。 決定品質を高めるために、計算属性と傾向スコアを検討する。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 標準プロファイル属性（ロイヤルティ層、購入履歴） | 属性は既にプロファイルスキーマに存在します | スキーマの変更は必要ありません。データの鮮度を確認してください |
| 計算属性（生涯価値、エンゲージメントスコア） | 実施要件やランキングは、集計された行動データによって異なります | S1設定が必要です。計算属性の更新ケイデンスに依存関係を追加します |
| Customer AI傾向スコア | ランキングは、マシンラーニングベースの予測を活用すべきです | 十分なトレーニングデータが必要（ターゲットイベントを含む10,000以上のプロファイル）、モデルのトレーニング時間 |

#### 主要な設定の詳細

- プロファイルスキーマに、実施要件ルールで参照されているフィールドが含まれていることを確認します（例：`_tenantId.loyaltyTier`、`_tenantId.subscriptionType`）。
- インプレッション、クリック、コンバージョンイベントのオファーインタラクション追跡スキーマが存在することを確認します
- オプション B：エッジアクティブ結合ポリシーが設定され、Web SDK データストリームでAJO サービスが有効になっていることを確認します

#### Experience League ドキュメント

- [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [プロファイルのスキーマを有効にする](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/union-schema)
- [結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### フェーズ 2: オーディエンス評価の設定

**アプリケーション関数：** RT-CDP: オーディエンス評価

このフェーズでは、オファーの適格性基準として使用されるオーディエンスを定義および評価します。 これらのオーディエンスは、特定のオファーに適格な顧客セグメント（例：「価値の高い顧客」がプレミアムオファーに適格か、「体験版ユーザー」がコンバージョンオファーに適格か）を判断します。

#### 決定：オーディエンス評価方法

オファーの適格性を得るために、オーディエンスメンバーシップをどれだけ迅速に更新する必要があるかを決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| バッチ評価 | 送信時に実施要件が評価されるオプション A （メールキャンペーン） | 最も簡単。すべてのセグメントルール式をサポート。毎日またはオンデマンドで更新 |
| ストリーミング評価 | バッチ間でほぼリアルタイムのオーディエンス更新が必要な場合のオプション AまたはC | 対象となるセグメントに対して自動で実行。セグメントルールのサポートが限定的（単一イベント、属性比較） |
| エッジ評価 | オプション B （web/アプリのリアルタイム）で、ページ読み込み時に実施要件を評価する必要がある | 1秒後。リアルタイムのweb/アプリのオファーに必要。単純な属性チェックとセグメントメンバーシップに限定 |

**UI ナビゲーション：**&#x200B;顧客/ オーディエンス / オーディエンスの作成/ ルールの構築

#### 主要な設定の詳細

- オファーの適格性に対するターゲティングオーディエンスの定義（例：「ロイヤルティゴールドレベル」「高価値顧客」「体験版ユーザー」）
- 必要に応じて抑制オーディエンスを定義します（例：「最近受信したオファーX」）。
- オプション Bの場合：適格性オーディエンスがエッジ評価に適格であることを確認します。時系列クエリやセグメントルール式の複雑な集計は避けます

#### 選択肢が異なる点

**オプション A （電子メール決定）の場合：**
バッチまたはストリーミングの評価で十分です。 オーディエンスは、キャンペーンの開始前または実行中に評価されます。 時間ベースの条件やイベント集計などの複雑なセグメントルール式が完全にサポートされています。

**オプション B （Web/アプリ リアルタイム）の場合：**
Edgeの評価が必要です。 オーディエンスは、シンプルな属性チェックやセグメントメンバーシップ条件を使用する必要があります。 セグメントルール式がエッジセグメント化に適格であることを確認して、エッジの適格性をテストします。

**オプション C （ジャーニー決定ノード）の場合：**
任意の評価方法は、ジャーニーの入力基準に応じて機能します。 ジャーニーでオーディエンスベースのエントリを使用する場合、オーディエンスの評価方法はジャーニーの要件と一致します。

#### Experience League ドキュメント

- [セグメント サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [エッジセグメント化](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### フェーズ 3：意思決定の設定

**アプリケーション関数：** AJO：決定

これは、オファーカタログ、適格性ルール、ランキング戦略、決定ポリシーを構築するコア段階です。 このフェーズでは、すべての配信オプション（A、B、C）が共有する決定エンジン設定が作成されます。

#### 決定：配置チャネルとコンテンツ形式

オファーの表示場所と形式を決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 電子メール（HTML） | オプション A - メール本文でHTMLとしてレンダリングされるオファーコンテンツ | リッチな書式設定をサポートします。メールクライアントと互換性がある必要があります |
| 電子メール（画像URL） | オプション A — メールでホストされた画像としてレンダリングされるオファー | より簡単な操作。画像はホストしてアクセスできる必要があります。動的なテキストは使用できません |
| Web （HTML） | オプション B — web ページ上でHTMLとしてレンダリングされるオファー | 完全なレイアウト制御。インタラクティブ要素をサポート |
| Web/モバイル（JSON） | オプション B — カスタムレンダリング用にJSONとして返されるオファーデータ | 最大限の柔軟性。レンダリングにはフロントエンド開発が必要 |
| コードベース（JSON） | オプション B - コードベースのエクスペリエンスサーフェスのオファーデータ | アプリケーション制御レンダリング；最も柔軟な |

#### 決定：ランキング戦略

適格なオファーから最適なオファーを選択する方法を決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 優先度ベース（手動） | スモールオファーカタログ：オファーの順序に関する明示的なビジネスルール | 設定が最も簡単、オファーごとに優先度の値を手動で割り当て、決定論的 |
| 数式ベース（カスタム式） | ランキングでは、プロファイル属性（ロイヤルティ層、最新性など）を考慮する必要があります | 柔軟：プロファイルデータを使用してランキングスコアを計算します。セグメントルール式の設計が必要です |
| AI ランキング（自動最適化） | 大規模なオファーカタログ：時間をかけて選択を最適化したい | モデルのトレーニングには最低1,000個のコンバージョンイベントが必要です。オファーパフォーマンスデータから学習します |

#### 決定：オファーの上限

オファーを表示する回数に制限があるかどうかを判断します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| プロファイルごとの上限 | 同じオファーが1人の顧客に何度も表示されるのを防ぎます | 高スループットのシナリオで数秒の遅延に対処することで、疲労を回避 |
| グローバルキャップ | すべてのプロファイルにわたるオファーのインプレッションの合計数を制限（在庫量の制限など） | オファー供給を制御します。上限に達すると、オファーは決定から除外されます |
| キャップなし | オファーは無制限に利用できます | 最も簡単；常時稼働のプロモーションに適しています |

**UI ナビゲーション：** コンポーネント >意思決定管理> プレースメント / ルール / オファー/決定

#### 主要な設定の詳細

1. **プレースメントを作成** – 各プレースメントのチャネルタイプとコンテンツ形式を指定して、オファーの表示場所を定義します。
   - UI：コンポーネント/意思決定管理/プレースメント
   - チャネル/フォーマットの組み合わせごとに1つのプレースメントを作成します（例：「Email Hero Banner - HTML」、「Web Homepage - JSON」、「Mobile App Card - JSON」）。

2. **実施要件ルールを定義** — プロファイル属性またはオーディエンスメンバーシップを参照するセグメントルール式を使用してルールを作成します。
   - UI：コンポーネント/意思決定管理/ルール
   - ルールでは、オーディエンスメンバーシップ、プロファイル属性（ロイヤルティ層、サブスクリプションタイプ）、日付制約、コンテキストデータを参照できます

3. **パーソナライズされたオファーを作成** – 各プレースメントのコンテンツ表現を使用して各オファーを作成し、実施要件ルールを割り当て、優先順位を設定し、オプションの上限を設定します。
   - UI：コンポーネント/意思決定管理/オファー/オファーの作成
   - 各オファーには、プレースメントごとにコンテンツ表現が必要です（例：メールにはHTML、webにはJSON）。
   - 各オファーを表示できるプロファイルを制御するための適格性ルールを割り当てます
   - オファーの有効期限（開始/終了）とオプションの頻度キャップを設定
   - 各オファーを承認し、意思決定に役立てることができます

4. **フォールバックオファーを作成** — パーソナライズされたオファーが適用されない場合に表示される各プレースメントのデフォルトオファーを作成します。
   - UI：コンポーネント/意思決定管理/オファー/フォールバックオファーの作成
   - フォールバックには、決定で使用されるすべてのプレースメントに対する表現が必要です

5. **コレクション修飾子とコレクションを作成** – 修飾子タグを使用してオファーをコレクションに整理します。
   - UI：コンポーネント/意思決定管理/コレクション修飾子
   - 決定範囲で使用するグループ関連オファー（例：「サマープロモーション」、「ロイヤルティリワード」）

6. **決定ポリシーの作成** – 配置、コレクション、ランキング戦略、フォールバックオファーを実行可能な決定にバインドします。
   - UI：コンポーネント/意思決定管理/決定/決定の作成
   - 各決定範囲は、プレースメントをコレクションにリンクし、ランキング方法を指定します

#### Experience League ドキュメント

- [意思決定管理の概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [プレースメントの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [決定ルールの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [パーソナライズされたオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [フォールバックオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [コレクションの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [コレクション修飾子の作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [決定を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [ランキング戦略](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### フェーズ 4: チャネルとサーフェスの設定

**アプリケーション関数：** AJO: Channel Configuration

このフェーズでは、オファーの配信に使用するチャネルサーフェスを設定します。 設定は、使用されている実装オプションによって異なります。

#### 決定：チャネルタイプ

ユースケースに必要なメッセージングチャネルを決定する。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 電子メール | オプション Aまたはオプション Cとメール配信 | サブドメインのデリゲーション、IP プール、送信者設定が必要 |
| Web | Web サーフェス配信のオプション B | Web SDKとデータストリームの設定が必要 |
| アプリ内 | モバイルアプリ配信のオプション B | Mobile SDKとプッシュ資格情報が必要です |
| コードベースのエクスペリエンス | カスタムレンダリングサーフェスのオプション B | 最も柔軟です。アプリケーションがレンダリングを処理します |

#### 選択肢が異なる点

**オプション A （電子メール決定）の場合：**
- UI：管理/チャネル/チャネルサーフェス/サーフェスの作成（電子メール）
- サブドメイン、IP プール、送信者名/電子メール、返信先、購読解除の設定
- 送信サブドメインのSPF、DKIM、およびDMARC レコードを確認します

**オプション B （Web/アプリ リアルタイム）の場合：**
- UI：管理/チャネル/チャネルサーフェス/サーフェスを作成（Webまたはアプリ内）
- Webの場合：Web サーフェス URL パターンの設定
- コードベースのエクスペリエンスの場合：アプリケーションのサーフェス URIを定義します
- データストリームでAJO サービスが有効になっていることを確認します

**オプション C （ジャーニー決定ノード）の場合：**
- ジャーニーで使用する各チャネル（電子メール、プッシュ通知、SMS、web）のチャネルサーフェスを設定します
- 各ジャーニーメッセージアクションには、対応するアクティブチャネルサーフェスが必要です

#### Experience League ドキュメント

- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [メールサーフェス設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [サブドメインをデリゲート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [プッシュ通知チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### フェーズ 5：コンテンツと配信の設定

**アプリケーション関数：** AJO: メッセージのオーサリング、AJO: Campaign Execution

このフェーズでは、選択したオファーを表示するメッセージテンプレートまたはエクスペリエンスサーフェスを設計し、配信メカニズム（キャンペーン、ジャーニー、またはコードベースのエクスペリエンス）を設定します。

#### 決定：オファーレンダリングのためのコンテンツアプローチ

オファーコンテンツをメッセージやエクスペリエンスにどのように統合するかを決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| Email Designerのオファー決定コンポーネント | オプション A — メールテンプレートへのオファーの埋め込み | ドラッグ&amp;ドロップ：決定結果にもとづいて自動的にコンテンツをレンダリング |
| 決定ポリシーによるコードベースのエクスペリエンス | オプション B — アプリケーションがオファーデータを取得およびレンダリングする | レンダリングの最大制御。フロントエンド開発が必要 |
| 意思決定を組み込んだジャーニーメッセージのアクション | オプション C – 決定ノードフィードで、オファーのコンテンツをジャーニーメッセージに送信 | オファーの選択と配信は、ジャーニーフロー内で調整されます |

#### 決定：キャンペーンタイプ （オプション Aのみ）

スケジュール型のマーケティングキャンペーンとAPI トリガー型のキャンペーンのどちらを実施するかを判断します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 予定キャンペーン | 定義されたオーディエンスに対する1回限りまたは定期的なバッチ送信 | 実行時にオーディエンスを評価。日付/時間または繰り返しを設定 |
| API トリガーキャンペーン | 指定されたプロファイルへのイベント駆動型またはシステム駆動型の送信 | トリガーペイロードで指定されたプロファイル。1 リクエストにつき最大20人の受信者をサポート |

#### 選択肢が異なる点

**オプション A （電子メール決定）の場合：**

1. 電子メール Designerを使用して電子メールメッセージを作成する
   - UI: キャンペーン/キャンペーンを作成/電子メールを選択/コンテンツを編集
   - オファー決定コンポーネントをメールレイアウトに挿入して、プレースメントゾーンを定義します
   - プロファイルレベルのコンテンツ（名前、ロイヤルティ層）用にパーソナライゼーショントークンを追加
   - オプションのパーソナライゼーションによる件名とプリヘッダーの設定
2. キャンペーンの作成と設定
   - UI: キャンペーン/キャンペーンを作成/スケジュール済みまたはAPI トリガー
   - ターゲットオーディエンスをバインドし、チャネルサーフェスを選択します
   - 実行スケジュールまたはAPIトリガー設定の設定
   - キャンペーンのレビューとアクティベート

**オプション B （Web/アプリ リアルタイム）の場合：**

1. コードベースのエクスペリエンスまたはweb チャネルの設定
   - UI: キャンペーン/キャンペーンを作成/コードベースのエクスペリエンス（またはWeb）
   - 決定ポリシーをエクスペリエンスサーフェスにリンクする
   - レンダリング形式の定義（コードベースのJSON応答、web チャネルのビジュアルエディター）
2. クライアントサイドレンダリングの実装
   - Web SDK `sendEvent`の応答を使用して、選択したオファーを取得します
   - ページ上の指定されたプレースメントにオファーコンテンツをレンダリングします
   - インプレッションとクリックの追跡の実装

**オプション C （ジャーニー決定ノード）の場合：**

1. 決定ノードを使用したジャーニーの設計
   - UI:ジャーニー/ジャーニーを作成/決定ノードを追加
   - フェーズ 3から決定ポリシーを呼び出すように決定ノードを設定します
2. 決定後にメッセージアクションノードを追加
   - 選択したオファーを参照するメール、プッシュ、またはSMS アクションを設定します
   - オファーエンゲージメントに基づいて、待機ステップ、条件、分岐を追加します
3. ジャーニーを公開

#### Experience League ドキュメント

- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [キャンペーンの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [ジャーニーを始める](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [コンテンツのプレビューとテスト](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### フェーズ 6：テストと検証

**アプリケーション関数：** AJO：決定、AJO：メッセージオーサリング

このフェーズでは、決定エンジンがテストプロファイルに対して正しいオファーを返し、オファーのコンテンツが各配信チャネルで適切にレンダリングされていることを検証します。

#### テスト決定ロジック

既知の属性を持つテストプロファイルを使用して、実施要件とランキングに基づいて適切なオファーが選択されていることを確認します。

- 様々な適格基準に一致するテストプロファイルを作成（例：ゴールド層、シルバー層、体験版ユーザー）
- 各テストプロファイルが期待されるオファーを受信することを確認します
- 適格性ルールに一致しないプロファイルがフォールバックオファーを受信することを確認します

#### コンテンツレンダリングのテスト

各配信チャネルのオファーコンテンツをプレビューします。

- オプション A：テストプロファイルでメールプレビューを使用して、オファーコンテンツが正しくレンダリングされていることを確認します
- オプション B：ステージング環境でのEdge Decisioningのレスポンスのテスト
- オプション C：ジャーニーテストモードを使用して、決定ノードが正しく選択されていることを確認します

#### インプレッションの追跡を検証

オファーのインプレッション数、クリック数、コンバージョン数が追跡されていることを確認します。

- オファーインタラクションイベントがトラッキングデータセットに表示されることを確認します
- オファーのインプレッションと下流のコンバージョンの間のアトリビューションを確認

#### Experience League ドキュメント

- [コンテンツのプレビューとテスト](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [メール校正を送信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/proofs)

### フェーズ 7: レポートとパフォーマンスの監視の設定

**Application function:** AJO: Reporting &amp; Performance Analysis

このフェーズでは、オファーの選択分布、受け入れ率、コンバージョンへの影響、フォールバック率を追跡するためのレポートを設定します。 このフェーズでは、AJOネイティブレポートとCJAベースのクロスチャネル分析の両方が対象となります。

#### 決定：報告方法

オファーのパフォーマンス分析に必要なレポートツールを決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| AJO ネイティブレポートのみ | 個々のキャンペーンやジャーニーの運用モニタリング | クイックアクセス、組み込みの配信およびエンゲージメント指標、限定的なクロスエンティティ分析 |
| CJA workspace analysis | クロスチャネルオファーの効果、売上への貢献度、funnelの分析 | CJAとの連携やデータビューが必要。より高度な分析能力が必要 |
| AJOとCJAは | 包括的な業務および分析範囲 | 実稼動実装に推奨、リアルタイムモニタリングにはAJO、戦略的分析にはCJA |

#### 主要な設定の詳細

1. **AJO ネイティブレポート** – 組み込みレポートを使用して、キャンペーンまたはジャーニーのパフォーマンスを監視します。
   - UI: キャンペーン/キャンペーンを選択/すべての時間レポート（またはライブレポート）
   - オファー固有の指標の確認：オファーごとのインプレッション数、オファーごとのクリック率、フォールバック率
   - 配信を監視するfunnel：対象/送信済み/配信済み/開封数/クリック数

2. **CJA分析（推奨）** — クロスチャネルのオファーパフォーマンスダッシュボードを構築します。
   - AJO オファーインタラクションデータセットを含むCJA接続の設定
   - オファー固有のディメンション（オファー名、プレースメント、決定）と指標（インプレッション数、クリック数、コンバージョン数）を含むデータビューを作成します
   - ワークスペース分析を構築して、オファーの選択分布、セグメントごとの受け入れ率、収益への影響、クロスチャネルのオファーの一貫性を把握します

#### Experience League ドキュメント

- [キャンペーングローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

## 実装に関する考慮事項

このセクションでは、オファー決定支援のガードレール、一般的な落とし穴、ベストプラクティス、トレードオフの決定について説明します。

### ガードレールと制限

実装を計画する際には、次のプラットフォームのガードレールと制限に注意してください。

- サンドボックスごとに最大10,000件の承認済みパーソナライズされたオファー – [意思決定管理ガードレール ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- 1決定あたり最大30件のプレースメント
- 決定リクエストごとに最大30個のコレクションスコープ
- AI ランキングモデルのトレーニングには最低1,000回のコンバージョンイベントが必要です
- オファーキャッピングカウンターは、高スループットのシナリオで最大で数秒の遅延が発生する場合があります
- Edgeの決定は、edge profile storeで使用可能なプロファイル属性に制限されます
- サンドボックスあたり最大4,000個のセグメント定義 – [ プラットフォームガードレール ](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- サンドボックスごとにEdgeでアクティブにできる結合ポリシーは1つだけです
- サンドボックスごとに最大500個のアクティブなライブキャンペーン
- ジャーニーエントリ率の制限：毎秒5,000 プロファイル
- サンドボックスごとに1つのチャネルタイプにつき最大10個のチャネルサーフェス

### よくある落とし穴

実装中にこのような問題が頻繁に発生するのを避けます。

- **決定では、常にフォールバックオファーが返されます。**&#x200B;これは、通常、パーソナライズされたオファーが承認されないか、有効期限範囲外であるか、実施要件ルールがテストプロファイルの属性と一致しないことを意味します。 各条件（承認ステータス、日付範囲、セグメントルール式の精度）を確認します。 上限に達していないことも確認してください。
- **オファーがコレクションに表示されません：** オファーに正しいコレクション修飾子がタグ付けされており、コレクションフィルターが一致していることを確認します。 オファーがコレクションベースの決定範囲に表示されるには、タグ付けと承認の両方が必要です。
- **ランキング式が適用されていません：**&#x200B;数式が構文的に有効であり、アクセス可能なプロファイル属性を参照していることを確認してください。 数式エラーは、目に見えるエラーのない優先度ベースのランキングにサイレントにフォールバックします。
- **Edge delivery returns empty personalization:** データストリームが[!DNL Adobe Journey Optimizer] サービスを有効にして設定され、決定範囲が正しくフォーマットされていることを確認します。 エッジアクティブ結合ポリシーが存在することを確認します。
- **チャネル間で一貫性のないオファー：** チャネルごとに個別の決定ポリシーを使用する場合、同じプロファイルに異なるオファーが届く可能性があります。 一貫性を保つために、チャネルをまたいで単一の意思決定ポリシーを使用するか、チャネル固有の配置にもとづいて意図的な相違を受け入れるか。
- **電子メールでオファーのコンテンツがレンダリングされない：** オファーに、電子メールのプレースメント形式（HTMLまたは画像URL）と一致するコンテンツ表現が含まれていることを確認します。 表示域が見つからないと、空白の配置ゾーンになります。

### ベストプラクティス

オファー決定支援の実装を成功させるには、次の推奨事項に従ってください。

- **小さいオファーカタログから開始して反復** – 決定フレームワークが検証されると、5 ～ 10個のオファーから開始して拡大します。 これにより、トラブルシューティングが簡素化され、スケーリングする前に実施要件ルールが正しく機能するようになります。
- **コレクション修飾子を戦略的に使用する** — カテゴリ別にオファーをタグ付けする（例：「獲得」、「リテンション」、「アップセル」）ことで、キャンペーンやジャーニーをまたいで再利用できる、柔軟なコレクションベースの決定範囲を実現します。
- **常に有意義なフォールバックオファーを作成する** — フォールバックオファーは単なるセーフティネットではありません。適格性ルールに一致しないプロファイルのデフォルトのエクスペリエンスです。 パーソナライゼーションがなくても価値を提供するフォールバックコンテンツに投資する。
- **可能な限り相互に排他的な適格性ルールをデザインする** – 複数のオファーの適格性が重複している場合、ランキング戦略は重要になります。 ビジネス要件によって特定のセグメントに対する特定のオファーが決まる場合は、ランキングのみに依存するのではなく、適格性ルールを相互排他的にします。
- **オプション B**&#x200B;のエッジ担当者プロファイルを使用したテスト — Edge プロファイルには、ハブプロファイル属性のサブセットが含まれています。 エッジで利用可能な属性を持つプロファイルを使用してテストを実行し、実稼動環境で適格性が正しく評価されていることを確認します。
- **フォールバック率を正常性指標として監視** – 高いフォールバック率（20 ～ 30%以上）は、オファーカタログが十分な顧客セグメントをカバーしていないことを示します。 オファーカタログを拡張するか、実施要件ルールを拡張します。
- **ライブのものを編集するのではなく、バージョン決定ポリシー** – アクティブなものを変更するのではなく、新しい決定ポリシーバージョンを作成します。 これにより、実行中のキャンペーンの中断を防ぎ、決定戦略のA/B比較が可能になります。

### トレードオフの決定

アーキテクチャおよび構成に関する意思決定をおこなう際には、次のトレードオフを考慮してください。

#### 適格性の正確性とオファーカバレッジの比較

厳格な適格性ルールにより、各オファーが最も関連性の高いプロファイルのみにリーチすることが保証されます。しかし、プロファイルがどのオファーにも一致しない場合、フォールバック率が高くなる可能性があります。 広範な適格性ルールにより、オファーのカバー範囲を最大化しながら、パーソナライゼーションの精度を低減。

- **厳しい適格性のメリット：**&#x200B;受け入れ率の向上、パーソナライゼーションの強化、オファー疲れの軽減
- **幅広い適格性のメリット：** フォールバック率の低下、より多くのプロファイルへのパーソナライズされたオファーの提供、シンプルなルール管理
- **推奨事項：**&#x200B;より幅広い適格性ルールから始め、パフォーマンスデータに基づいてルールを強化します。 フォールバック率と受け入れ率を監視し、適切なバランスを見極めます。 ランキング戦略を使用して、広く実施要件を満たすオファーを区別します。

#### 優先順位ベースとAI ランキングの比較

優先順位にもとづくランキングにより、企業は表示されるオファーを完全に制御できます。一方、AIによるランク付けランキングは、コンバージョン率を最適化しますが、オファーの選択に対する人間の制御は軽減します。

- **優先度に基づく優先度：** ビジネス管理、予測可能性、トレーニングデータ不要、即時の展開
- **AIによる優先度：** コンバージョンの最適化、予期しないパターンの検出、変化する顧客行動への自動適応
- **推奨事項：**&#x200B;優先度ベースのランキングを使用して、最初のローンチと、ビジネス管理が最も重要な規制に敏感なオファーを行います。 十分なコンバージョンデータ（1,000以上のイベント）が利用可能になったら、AIを活用したランク付け機能に移行して、パフォーマンスを最適化した大量のユースケースを実現。

#### 単一の意思決定ポリシーとチャネルごとの意思決定ポリシーの比較

単一の意思決定ポリシーは、あらゆるチャネルをまたいでオファーの一貫性を確保しますが、チャネルごとの最適化は制限されます。 チャネルごとのポリシーにより、チャネルに特化したランキングと適格性を備えていますが、顧客体験の一貫性が損なわれるリスクがあります。

- **単一のポリシーの利点：** クロスチャネルの一貫性、管理の簡素化、統合レポート
- **チャネルごとのポリシーの利点：** チャネルごとに最適化されたランキング、チャネル固有の適格性（webのみのオファーなど）、独立した反復
- **推奨事項：** クロスチャネルの一貫性を確保するために、1つの決定ポリシーから開始します。 ビジネス要件がチャネル固有のオファー戦略（web限定のフラッシュセールスなど）を要求する場合にのみ、チャネルごとのポリシーを作成します。

#### ハブ決定（オプション A/C）とエッジ決定（オプション B）

Hub Decisioningは完全なプロファイルにアクセスできますが、送信時に動作します。 Edge decisioningは、2秒以下の待ち時間でリアルタイムに動作しますが、エッジで使用可能なプロファイル属性に制限されます。

- **ハブ決定のお気に入り：**&#x200B;完全なプロファイルデータ、複雑な適格性ルール、バッチキャンペーンボリュームへのアクセス
- **Edgeの意思決定に役立つ機能：** リアルタイムのコンテキスト、セッション内のパーソナライゼーション、2秒以下の応答
- **推奨事項：**&#x200B;完全なプロファイルデータによってオファーの関連性が向上するアウトバウンドチャネル（電子メール、プッシュ通知）にハブ決定を使用します。 リアルタイムの対応が重要なインバウンドチャネル（web、アプリ）に対してedge decisioningを使用します。 エッジの適格性ルールは、エッジで使用可能な属性のみを使用するようにします。

## 関連ドキュメント

次のリソースでは、このユースケースパターンで使用されるコンポーネントに関する追加の詳細を示します。

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

### オファーの配信

- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Edge Decisioning APIを使用したオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Decisioning APIを使用したオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/decisioning-api)

### チャネル設定

- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [メールサーフェス設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [サブドメインをデリゲート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [プッシュ通知チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [SMS チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### メッセージのオーサリングとパーソナライゼーション

- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalizationの構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [コンテンツのプレビューとテスト](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### キャンペーンとジャーニー

- [キャンペーンの基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [キャンペーンの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [ジャーニーを始める](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

### コンテンツの検証

- [コンテンツ実験を始める](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [コンテンツ実験を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)

### オーディエンスとセグメンテーション

- [セグメント サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [エッジセグメント化](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### プロファイルとID

- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [計算属性の概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Customer AIの概要](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### データモデリングと収集

- [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Web SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [データストリームの設定](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)

### レポートと分析

- [キャンペーングローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [CJAの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### データガバナンスとライフサイクル

- [データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [データ使用状況ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview)
- [高度なデータライフサイクル管理の概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [Journey Optimizerでの同意](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### ガードレール

- [Journey Optimizerのガードレール](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [リアルタイムの顧客プロファイルのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

### チュートリアル

- [意思決定管理APIの概要](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/getting-started)
