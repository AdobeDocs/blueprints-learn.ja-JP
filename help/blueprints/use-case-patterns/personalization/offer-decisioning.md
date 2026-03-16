---
title: Offer Decisioning
description: 一元的な決定ロジックを使用して、チャネルをまたいでプロファイルに次善のオファーやコンテンツを選択する方法を説明します。
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '7889'
ht-degree: 2%

---


# Offer Decisioning

このガイドでは、[!DNL Adobe Journey Optimizer] （AJO） Decisioning and [!DNL Adobe Real-Time Customer Data Platform] （RT-CDP）を使用した Offer Decisioning の包括的な実装リファレンスを提供します。 これは、チャネルをまたいで各顧客プロファイルの次善のオファーを決定する一元的なオファー選択ロジックを実装する必要がある、ソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

このガイドを使用すると、設定する必要のあるもの、選択肢が存在する場所、各決定に適用されるトレードオフを理解できます。

パターンは、「何を表示するか」の決定を「どこに表示するか」チャネルロジックから切り離し、メール、web、モバイルアプリ、その他のタッチポイントをまたいで、一貫性を持ち最適化されたオファー選択を可能にします。 AJO Decisioning は、オファーの作成とカタログ管理、実施要件ルール（各オファーを表示できるユーザー）、ランキング戦略（実施要件を満たすオファーの選択方法）、プレースメント（オファーが表示される場所）、決定ポリシー（すべてを結び付ける）など、オファーのライフサイクル全体を管理します。

## ユースケースの概要

組織は、インタラクションの瞬間に、最も関連性の高いオファー、プロモーションまたはインセンティブを各顧客に提示する必要が頻繁にあります。 電子メールキャンペーン、web サイトホームページ、モバイルアプリ、複数手順のジャーニー内の決定ポイントのいずれかでインタラクションが発生するかどうかは同じです。顧客が誰で、何に適格か、目的の結果を引き起こす可能性が最も高いオファーに基づいて、利用可能なオプションのカタログから最適なオファーを選択します。

Offer Decisioning は、AJOの意思決定管理エンジンで、すべてのオファー選択ロジックを一元化することでこれを解決します。 オファーの割り当てを個々のキャンペーンやチャネルにハードコーディングする代わりに、決定エンジンで各プロファイルの属性、オーディエンスメンバーシップおよびコンテキスト信号を評価して、最適なオファーをリアルタイムで決定します。 この一元化により、同じ顧客がどのチャネルを通じてでも、一貫性のある最適化されたオファーを受け取れるようになります。

このパターンは、範囲が既知の訪問者 web/アプリのパーソナライゼーションとは異なります。offer decisioning はチャネルに依存しない一元的なパターンですが、既知の訪問者のパーソナライゼーションはデジタルサーフェスのパーソナライゼーションに重点を置いています。 これは、アプローチの行動レコメンデーションとは異なります。Offer Decisioning では明示的な実施要件ルールとランキング戦略を使用し、行動レコメンデーションでは、選択戦略と ML モデルを使用した行動信号駆動型のレコメンデーションを重視します。

## 主なビジネス目標

このユースケースパターンでは、以下のビジネス目標がサポートされています。

**[パーソナライズされたカスタマーエクスペリエンスの提供](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
コンテンツ、オファーおよびメッセージングを、個々の環境設定、行動およびライフサイクルステージに合わせて調整します。
**KPI:** エンゲージメント、コンバージョン率、顧客満足度（CSAT）

**[クロスセルとアップセルの収益を促進](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
行動および購入履歴に基づいて、既存の顧客に補完的でプレミアムな製品またはサービスを宣伝します。
**KPI:** アップセル/クロスセル %、増分収益、顧客のライフタイム値

**[顧客ロイヤルティとライフタイムバリューの向上](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
ロイヤルティプログラム、報酬、パーソナライズされたエンゲージメントを通じて、顧客関係を深め、長期的な価値を最大化します。
**KPI:** 顧客のライフタイム値、リテンション、アップセル/クロスセル %

## 戦術的な使用例

次のシナリオは、Offer Decisioning を実際にどのように適用できるかを示しています。

- メールキャンペーンの次善のオファー – 送信時に受信者ごとに最も関連性の高いプロモーションを選択します
- Web サイトのリアルタイムプロモーションバナー – decisioning では、訪問者のプロファイルに基づいてページ読み込み時にオファーを選択します
- ユーザーのライフサイクルステージに最適なインセンティブでパーソナライズされたアプリ内カード
- クロスチャネルオファーの一貫性 – 同じ決定ロジックでメール、web およびプッシュを配信するので、顧客は統一されたオファーエクスペリエンスを確認できます
- 顧客価値レベルに基づく動的なクーポンまたは割引の選択（例：価値の高い顧客にはプレミアム・オファーを提供）
- 現在のサブスクリプションレベルに基づく製品のアップグレードまたはアップセルのオファー選択
- 層とアクティビティ履歴に基づくロイヤルティ報酬オファーのパーソナライゼーション

## 主要業績評価指標

次の KPI は、Offer Decisioning 実装の有効性を測定するのに役立ちます。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| オファー受け入れ率 | クリック、引き換え、コンバージョンを発生させる配信済みオファーの割合 | オファーのクリック数または引き換え数/配信されたオファーの合計数 |
| オファー選択配分 | すべての決定で選択された各オファーの割合 | オファーあたりのカウント/レンダリングされた決定の合計 |
| フォールバック率 | パーソナライズされたオファーが選定されず、フォールバックが提供された決定の割合 | フォールバックインプレッション数/決定総数 |
| コンバージョン率 | 目的のアクション（購入、サインアップ、引き換え）を完了したオファー受信者の割合 | コンバージョン/オファーインプレッション数 |
| 増分収益 | 決定で選択したオファーに起因する売上高と、コントロールグループやフォールバックに起因する売上高 | パーソナライズされたオファーからの売上高 – フォールバック/コントロールからの売上高 |
| クロスチャネルの一貫性スコア | 定義されたウィンドウ内の複数のチャネルで同じオファーを受信するプロファイルの割合 | 一貫したオファー/マルチチャネルインプレッションの合計 |
| オファークリックスルー率 | クリックにつながるオファーインプレッション数の割合 | オファークリック数/オファーインプレッション数 |

## ユースケースパターン

ここでは、Offer Decisioning の関数チェーンとパターンの定義について説明します。

**Offer Decisioning**

一元的な決定ロジックを使用して、チャネルをまたいでプロファイルに最適なオファーやコンテンツを選択します。

**関数チェーン：** オーディエンス評価/オファーの実施要件/ ランキング戦略/決定実行/配信/レポート

各コンポジションのマニフェスト方法については、[&#x200B; 実装オプション &#x200B;](#implementation-options) の節を参照してください。

## アプリケーション

このユースケースパターンでは、次のAdobe アプリケーションが使用されています。

- **[!DNL Adobe Journey Optimizer]（AJO）** - オファーの作成、実施要件ルール、ランキング戦略、プレースメントおよび決定ポリシーに使用する意思決定管理エンジン。オファー配信のチャネル設定およびメッセージオーサリング。キャンペーンおよびジャーニーの実行
- **[!DNL Adobe Real-Time Customer Data Platform]（RT-CDP）** - オファーの実施要件セグメントに対するオーディエンス評価。実施要件とランキングに使用されるプロファイルデータと計算属性。
- **[!DNL Adobe Experience Platform]（AEP）** - AJOと RT-CDP の両方をサポートする、統合プロファイルストア、ID 解決およびデータ基盤

## 基本関数

このユースケースパターンでは、次の基本機能が配置されている必要があります。 各関数のステータスは、通常、必須、事前設定済みと想定、適用不可のいずれかを示します。

| 基本関数 | ステータス | 設定する必要があること | Experience League リファレンス |
| --- | --- | --- | --- |
| 管理とガバナンス | 所定の位置に想定 | 意思決定権限が有効なAJO サンドボックス。 実装チームに割り当てられたオファー管理の役割（決定マネージャー、オファー承認者）。 | [&#x200B; サンドボックスの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/sandbox/home)、[&#x200B; アクセス制御の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/access-control/home) |
| データモデリングと準備 | 必須 | プロファイルスキーマには、オファーの実施要件ルールに使用する属性（ロイヤルティ層、購入履歴、購読タイプなど）を含める必要があります。 オファーインプレッション数、クリック数およびコンバージョン数をトラッキングするための、オファー応答/インタラクションスキーマを配置する必要があります。 | [XDM システムの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/home)、[&#x200B; スキーマ構成の基本 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/schema/composition) |
| データソースとコレクション | 所定の位置に想定 | 実施要件ルールで使用するプロファイル属性は、最新の属性である必要があります。 Web 配信（オプション B）の場合、データストリームでAJO サービスを有効にして、web SDKを実装する必要があります。 メール配信の場合、プロファイル属性は送信時に解決可能である必要があります。 | [Web SDKの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/home)、[&#x200B; データストリームの設定 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/datastreams/configure) |
| ID とプロファイル設定 | 所定の位置に想定 | プロファイルは、オファーが配信されるすべてのチャネルで解決可能である必要があります。 クロスチャネルオファーの一貫性を保つには、統合 ID が重要です。メール、web およびモバイルのコンテキストで同じプロファイルを認識する必要があります。 リアルタイムの web/アプリ配信には、エッジアクティブ結合ポリシーが必要です。 | [ID サービスの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/home)、[&#x200B; 結合ポリシーの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/merge-policies/overview) |
| オーディエンスの定義とセグメント化 | 必須 | オファーの実施要件条件として使用するオーディエンスは、「高価値顧客」、「体験版ユーザー」、「ロイヤルティゴールド層」など、定義して評価する必要があります。 評価方法は、配信待ち時間と一致する必要があります – リアルタイム web/アプリのエッジ評価、メールキャンペーンのバッチまたはストリーミング。 | [&#x200B; セグメント化サービスの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/home)、[&#x200B; セグメントビルダー UI ガイド &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/segment-builder) |

## サポート関数

次の機能は、このユースケースのパターンを拡張しますが、コア実行には必要ありません。

| サポート機能 | ステータス | これが重要な理由 | Experience League リファレンス |
| --- | --- | --- | --- |
| 計算/派生属性の作成 | 推奨 | 顧客 AI の傾向スコア、ライフタイム値の計算およびエンゲージメント指標により、ランキング戦略の有効性が大幅に向上します。 「前回購入からの日数」や「90 日間の合計支出」などの計算済み属性を使用すると、より正確な実施要件ルールと式ベースのランキングが可能になります。 | [&#x200B; 計算済み属性の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/computed-attributes/overview)、[&#x200B; 顧客 AI の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/intelligent-services/customer-ai/overview) |
| データ・ライフサイクル管理 | 推奨 | オファー履歴と決定イベントのデータは、時間の経過と共に蓄積されます。 ストレージを管理し、データ保持要件に準拠するには、オファーインタラクションイベントデータセット用に保持ポリシー（有効期限）を設定する必要があります。 | [&#x200B; 高度なデータライフサイクル管理の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/data-lifecycle/home)、[&#x200B; データセット有効期限 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| データ使用のラベル付けと適用 | 推奨 | ガバナンスラベルを使用すると、機密性の高いターゲティング条件（財務ステータス、健康状態など）を持つオファーがデータ使用ポリシーに準拠できるようになります。 実施要件ルールで使用されるフィールドのラベルにより、オファーのターゲティングが非準拠になるのを防ぎます。 | [&#x200B; データガバナンスの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/home)、[&#x200B; データ使用ラベルの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview) |
| 監視と監視 | 推奨 | 決定エンジンのパフォーマンス、フォールバック率およびオファー配信の正常性は監視する必要があります。 高いフォールバック率に関するアラートは、実施要件ルールの設定ミスやデータの鮮度の問題を示す場合があります。 | [&#x200B; アラートの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/observability/alerts/overview)、[Observability Insights の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/observability/home) |
| レポートと分析 | Included | オファーパフォーマンスレポートは、ファンクションチェーンの一部です（フェーズ 7）。 CJA analysis を使用すると、クロスチャネルオファーの有効性の測定、売上高の影響のアトリビューション、最適化のオポチュニティの特定が可能になります。 | [CJAの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-overview/cja-overview)、[Analysis Workspaceの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/home) |

## アプリケーション関数

このプランは、アプリケーション機能カタログから次の機能を実行します。 関数は、番号付きステップではなく、実装フェーズにマッピングされます。

### [!DNL Journey Optimizer] （AJO）

次の表に、AJO関数と、それらが設定される実装フェーズを示します。

| 関数 | 実装フェーズ | 説明 |
| --- | --- | --- |
| 決定 | フェーズ 3：決定の設定 | オファー項目の作成、実施要件ルールの定義、ランキング戦略の設定、フォールバックオファーの作成、プレースメントの定義および決定ポリシーの作成 |
| チャネル設定 | フェーズ 4：チャネルとサーフェスの設定 | オファー配信用のメール、web、アプリ内またはコードベースのチャネルサーフェスの設定 |
| メッセージオーサリング | フェーズ 5：コンテンツと配信の設定 | オファーのプレースメントゾーンを使用したメッセージテンプレートの設計、web/アプリ配信用のコードベースのエクスペリエンスの設定 |
| キャンペーンの実行 | フェーズ 5：コンテンツと配信の設定 | 決定ポリシーを呼び出すスケジュール済みキャンペーンまたは API トリガーキャンペーンの実行（オプション A） |
| コンテンツ実験 | フェーズ 5：コンテンツと配信の設定 | オプションで、様々なランキング戦略を A/B テストしたり、クリエイティブのバリエーションを提供したりできます。 |
| レポートとパフォーマンスの分析 | フェーズ 7：レポートとパフォーマンスの監視 | オファー選択配分、承認率、フォールバック率およびチャネルレベルのパフォーマンスを監視 |

### [!DNL Real-Time CDP] （RT-CDP）

次の表に、RT-CDP 関数と、それらが設定される実装フェーズを示します。

| 関数 | 実装フェーズ | 説明 |
| --- | --- | --- |
| オーディエンスの評価 | フェーズ 2：オーディエンスの評価 | オファーの実施要件ルールに使用するオーディエンスを定義および評価し、適切な評価方法（バッチ、ストリーミングまたはエッジ）を選択する。 |
| プロファイルエンリッチメント | フェーズ 1 （サポート）：計算属性 | ランキング戦略の有効性を向上させる計算属性と傾向スコアを使用してプロファイルを強化します |

## 前提条件

実装を開始する前に、次の前提条件を満たしてください。

- [ 意思決定管理機能が有効なAJO サンドボックスの ] 成
- [ 意思決定管理権限（オファー、プレースメント、決定の作成/編集）を持つ ] ユーザーの役割
- [ ] プロファイルスキーマには、オファーの実施要件に必要な属性（ロイヤルティ層、顧客セグメント、サブスクリプションレベルなど）が含まれます
- [ ] プロファイルデータは最新で、実施要件属性の鮮度のためにアクティブに取り込まれています
- [ オプション A （メール）の ]：検証済みサブドメインとウォームド IP プールで設定されたメールチャネルサーフェス
- [ オプション B （Web/アプリ）の ]：データストリームでAJO サービスを有効にして実装された Web SDK。エッジアクティブ結合ポリシーが設定されている
- [ オプション C （ジャーニー）の ]:ジャーニーキャンバス権限と、1 つ以上のジャーニーエントリイベントまたはオーディエンスが設定されています。
- [ オファーとプレースメントの組み合わせごとに準備された ] オファークリエイティブアセット（画像、コピー、CTA）
- [ 各プレースメント用に準備されたフォールバックオファーのコンテンツを ] します
- [ RT-CDP で定義および評価されたオファーの実施要件ルールに対するオーディエンスの ] 定

## 実装オプション

この節では、offer decisioning で使用可能な実装オプションについて説明します。 各オプションは、異なる配信チャネルとユースケースコンテキストを提供します。

### オプション A:E メール Offer Decisioning

このオプションは、プロモーションメール、ニュースレターのパーソナライゼーション、動的なオファーコンテンツを含むライフサイクルメールなど、アウトバウンドメールキャンペーンに含める最適なオファーを選択する場合に最適です。 決定は、各受信者のメッセージレンダリング時に行われます。

#### 仕組み

決定ポリシーは、メールメッセージのレンダリング中に呼び出され、各受信者に最適なオファーを選択します。 メールテンプレートには、オファー配置ゾーンが含まれ、決定エンジンが、選択されたオファーのコンテンツ表現（画像、HTMLまたはテキスト）を挿入します。 送信時に、エンジンはオファーの実施要件ルールに照らして各受信者のプロファイルを評価し、ランキング戦略を適用して、勝者のオファーのコンテンツをメールに埋め込みます。

このアプローチは、スケジュール済みキャンペーン（キャンペーンの実行時に評価）と、ジャーニーが埋め込まれたメール（プロファイルがメッセージアクションノードに到達すると評価）の両方で機能します。 オファーコンテンツ（画像、ヘッドライン、本文コピー、CTA）は、意思決定の結果に基づいて受信者ごとにパーソナライズされます。

#### 主な考慮事項

- オファーの実施要件は、プロファイルの現在の状態を使用して送信時に評価されます
- メッセージのレンダリング中に決定が行われるので、バッチオーディエンスの評価で十分です
- 各オファーには、メールプレースメントのHTMLまたは画像コンテンツの表示域が必要です
- フォールバックオファーには、使用する電子メールプレースメントごとにコンテンツが必要

#### メリット

- 最もシンプルな実装パス – 標準のキャンペーンまたはジャーニーのメール配信を使用
- クライアントサイドのSDK要件がありません
- 既存のメールインフラストラクチャおよびチャネルサーフェスとの連携
- バッチキャンペーンの実行により、大量のオーディエンスをサポートします。

#### 制限事項

- 決定は送信時に行われ、送信後の動作に適応できない
- オファーコンテンツは、メールの配信後は静的です（リアルタイムの更新はありません）
- ハブプロファイルストアで使用できるプロファイル属性に制限（エッジではない）

#### Experience League リソース

- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [キャンペーンの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

### オプション B:Web/アプリのリアルタイム Offer Decisioning

このオプションは、web ページやモバイルアプリでリアルタイムにオファーを選択する場合（ホームページのプロモーションバナー、アカウントダッシュボードのオファーウィジェット、アプリ内オファーカード、ページの読み込みまたは画面レンダリング時にオファーを選択する必要があるデジタルサーフェス）に最適です。

#### 仕組み

決定ポリシーは、Edge Decisioning ネットワークまたはコードベースのエクスペリエンスを介して、ページの読み込み時またはアプリの画面レンダリング時に呼び出されます。 訪問者がページを読み込むと、Web SDKはEdge Networkにリクエストを送信します。これにより、オファーの実施要件ルールおよびランキング戦略に照らして訪問者のエッジプロファイルが評価されます。 選択したオファーが応答で返され、デジタルサーフェス上に設定されたプレースメントでレンダリングされます。

コードベースのエクスペリエンスの場合、アプリケーションは決定応答を取得し、カスタムのフロントエンドロジックを使用してオファーコンテンツをレンダリングします。 Web チャネルエクスペリエンスの場合、AJO web チャネルでは、ビジュアルベースまたはコードベースのオーサリングを使用して、オファーコンテンツをページに直接挿入できます。

#### 主な考慮事項

- データストリームでAJO サービスが有効になっている web SDKまたは Mobile SDKの実装が必要です
- リアルタイムのプロファイル検索にはEdge - アクティブ結合ポリシーが必要です
- 実施要件に使用するオーディエンスは、エッジ評価（簡単な属性チェックとセグメントメンバーシップ）をサポートする必要があります。
- オファーコンテンツ表示域では、クライアントサイドレンダリングに JSON 形式または画像 URL 形式を使用する必要があります
- インプレッショントラッキングを実装して、オファーのビュー数とクリック数を把握する必要があります。

#### メリット

- 訪問者の現在のプロファイル状態に基づくリアルタイムのインセッションオファー選択
- Edge Networkを介したサブ秒の決定待ち時間
- オファーは、エッジで使用可能な最新のプロファイルデータに適応します
- コンテンツ実験を介したオファー戦略の A/B テストをサポートします。

#### 制限事項

- クライアントサイドのSDK実装（Web SDKまたは Mobile SDK）が必要です
- Edge プロファイルには、完全なハブプロファイル属性のサブセットがあります。複雑な実施要件ルールは、正しく評価されない場合があります
- Edge セグメントには、セグメントルールの複雑さの制限があります（時系列クエリはありません）
- コードベースのエクスペリエンスのカスタムレンダリングには、フロントエンド開発が必要です

#### Experience League リソース

- [Edge Decisioning API を使用したオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [コードベースのエクスペリエンスチャネル](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/code-based-experience/get-started-code-based)

### オプション C:ジャーニーの決定ノード

このオプションは、複数の手順からなるジャーニー内でオファーを選択する場合に最適です。カスタマージャーニーの決定ポイントで最適なオファーを選択すると、次のアクションノードに配信されます。 オファーの決定が、待機、条件、複数のメッセージアクションを含む、より広いオーケストレーションフローの一部である場合に、これを使用します。

#### 仕組み

決定ポリシーは、AJO ジャーニーキャンバス内の決定ノードから呼び出されます。 プロファイルが決定ノードに到達すると、エンジンはオファーの実施要件とランキングを評価して、最適なオファーを選択します。 選択したオファーは、次のメッセージアクションを知らせます。オファーに含めるオファーコンテンツ、使用するチャネル、オファーの結果に基づいて実行するジャーニーブランチなどです。

このアプローチにより、オファーの決定が後続のジャーニーステップに影響を与えるアダプティブジャーニーが可能になります。 例えば、ジャーニーで最適なオファーを選択し、メールで配信し、エンゲージメントを待ってから、オファーが開封されなかった場合にプッシュ通知でフォローアップします。

#### 主な考慮事項

- ジャーニーは、決定ノードの後に 1 つ以上のメッセージアクションノードを配置する必要があります
- オファーの実施要件は、プロファイルが決定ノードに到達した時点のプロファイルの状態を使用して評価されます
- 決定と配信の間のジャーニーの待機手順により、プロファイルのステータスが変わる場合があります
- ジャーニーのブランチと組み合わせて、選択したオファーに基づいて異なるパスを作成できます。

#### メリット

- オファーの選択を複数ステップのオーケストレーションフローに統合
- オファーの選択が後続のステップに影響を与えるアダプティブジャーニーを有効にする
- 同じジャーニー内でのクロスチャネル配信のサポート（メール、プッシュ、SMS）
- オファー後のエンゲージメントトラッキングのためのジャーニー条件と組み合わせることができます。

#### 制限事項

- スタンドアロンのキャンペーン決定よりも設定が複雑になる
- ジャーニースループットの制限が適用されます（1 秒あたり 5,000 プロファイルのエントリ率）
- 決定はジャーニーのコンテキストに関連付けられています。変更には、ジャーニーのバージョン管理が必要です
- オファーカタログまたは意思決定ポリシーの更新を有効にするには、ジャーニーを再公開する必要があります

#### Experience League リソース

- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [ジャーニーの概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/orchestrate-journeys/journey)

### オプションの比較

次の表では、主要な条件を満たす 3 つの実装オプションを比較しています。

| 条件 | オプション A：電子メールの決定 | オプション B:Web/アプリのリアルタイム | オプション C:ジャーニーの決定ノード |
| --- | --- | --- | --- |
| に最適 | 受信者ごとのオファー選択を使用したバッチメールキャンペーン | Web/アプリのサーフェスに表示されるリアルタイムオファーバナー | 複数の手順で調整されたジャーニー内のオファー選択 |
| 決定待ち時間 | 送信時（バッチレンダリング時の受信者あたりの秒数） | サブ秒（Edge Network） | ジャーニーノードの実行時（秒） |
| チャネル | 電子メール | Web、モバイルアプリ、コードベースのサーフェス | ジャーニー内の任意のチャネル（メール、プッシュ、SMS） |
| SDKが必要です | いいえ | 対応（Web SDKまたは Mobile SDK） | いいえ（メールまたはプッシュの場合）、はい（web チャネルがジャーニーアクションの場合） |
| オーディエンスの評価 | バッチまたはストリーミング | Edge | バッチ、ストリーミングまたはエッジ（ジャーニーエントリに応じて異なる） |
| プロファイルデータの範囲 | 完全なハブプロファイル | Edge プロファイル（サブセット） | 完全なハブプロファイル |
| 複雑性 | 低 | Medium – 高 | 中 |
| スループット | 高（バッチキャンペーンボリューム） | 高（Edge Networkスケール） | Medium（ジャーニーのスループットの制限があります） |

### 適切なオプションを選択

次のガイダンスに従って、ユースケースに最適な実装オプションを選択してください。

- **オプション A を選択します** は、アウトバウンドメールキャンペーンで受信者ごとに最適なオファーを選択する主なユースケースであり、クライアントサイドのSDKが使用できない場合に選択します。 これは最も簡単な実装パスであり、プロモーションメール、ニュースレターおよびライフサイクルキャンペーンに適しています。
- 訪問者が web ページを読み込んだ時点、またはモバイルアプリを開いた時点で、オファーをリアルタイムで選択する必要がある場合は、**オプション B を選択** します。 これには、web SDKまたはモバイルSDK、およびエッジアクティブな結合ポリシーが必要ですが、最も高速でコンテキストに沿ったオファー選択が可能になります。
- **オファーの決定が、複数のステップ、待機、条件付きブランチを含む広範なカスタマージャーニーの一部である場合は、オプション C を選択** します。 選択したオファーがダウンストリームジャーニーのアクションに影響を与える必要がある場合や、オファーエンゲージメントに基づくマルチチャネルのフォローアップが必要な場合は、これは適切な選択です。
- **結合オプション**：チャネルをまたいで一貫してオファーを配信する必要がある場合。 3 つのオプションすべてで同じ決定ポリシーを使用して、顧客がメール（オプション A）、web サイト（オプション B）、ジャーニーのフォローアップ（オプション C）で同じオファーを確実に表示できるようにします。

## 実装フェーズ

次のフェーズでは、Offer Decisioning のエンドツーエンドの実装順序を概説します。

### フェーズ 1：基本的な前提条件の検証

**アプリケーション機能：** AEP：データモデリングと準備、AEP:ID とプロファイル設定

このフェーズでは、基本的なデータレイヤーが Offer Decisioning をサポートしているかどうかを検証します。 プロファイルスキーマには、オファーの実施要件ルールで使用される属性を含める必要があり、ID 設定によってクロスチャネルプロファイル解決を有効にする必要があります。

#### 決定：実施要件のプロファイル属性

オファーの実施要件ルールで使用するプロファイル属性を決定します。

>[!NOTE]
>プロファイル属性の選択は、実施要件ルールのデザインとランキング戦略の有効性の両方に影響を与えます。 決定の品質を高めるために、計算属性と傾向スコアを考慮します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| 標準プロファイル属性（ロイヤルティ層、購入履歴） | 属性は既にプロファイルスキーマに存在します | スキーマの変更は必要ありません。データの鮮度を確認してください |
| 計算属性（ライフタイム値、エンゲージメントスコア） | 実施要件またはランキングは、集計した行動データに依存します | S1 設定が必要です。計算属性の更新ケイデンスへの依存関係を追加します。 |
| 顧客 AI の傾向スコア | ランキングは、ML ベースの予測を活用する必要があります | 十分なトレーニングデータ（ターゲットイベントを含む 10,000 件以上のプロファイル）が必要。モデルトレーニング時間 |

#### 主要な設定の詳細

- プロファイルスキーマに実施要件ルールで参照されるフィールド（`_tenantId.loyaltyTier`、`_tenantId.subscriptionType` など）が含まれていることを確認
- インプレッション、クリックおよびコンバージョンイベント用にオファーインタラクショントラッキングスキーマが存在することを確認します
- オプション B の場合：エッジアクティブ結合ポリシーが設定され、web SDK データストリームでAJO サービスが有効になっていることを確認します

#### Experience League ドキュメント

- [XDM システムの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/home)
- [プロファイルのスキーマを有効にする](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/union-schema)
- [結合ポリシーの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/merge-policies/overview)

### フェーズ 2：オーディエンス評価の設定

**アプリケーション関数：** RT-CDP：オーディエンス評価

このフェーズでは、オファーの実施要件条件として使用するオーディエンスを定義および評価します。 これらのオーディエンスは、特定のオファーの対象となる顧客セグメントを決定します（例：「高価値顧客」はプレミアムオファーの対象となり、「体験版ユーザー」はコンバージョンオファーの対象となります）。

#### 決定：オーディエンス評価方法

オファーの実施要件を満たすためにオーディエンスメンバーシップがどの程度迅速に更新される必要があるかを決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| バッチ評価 | 実施要件が送信時に評価されるオプション A （メールキャンペーン） | 最も単純。すべてのセグメントルール式をサポート。日次またはオンデマンド更新 |
| ストリーミング評価 | バッチ間でほぼリアルタイムのオーディエンス更新が必要な場合は、オプション A または C | 適格なセグメントに対して自動。制限付きセグメントルールのサポート（単一イベント、属性比較） |
| エッジ評価 | ページの読み込み時に実施要件を評価する必要があるオプション B （web/アプリのリアルタイム） | 1 秒未満。リアルタイムの web/アプリオファーに必要。シンプルな属性チェックおよびセグメントメンバーシップに制限される |

**UI ナビゲーション：** 顧客/オーディエンス/オーディエンスを作成/ルールを作成

#### 主要な設定の詳細

- オファーの実施要件に合わせたターゲティングオーディエンスの定義（「ロイヤルティゴールド層」、「高価値顧客」、「体験版ユーザー」など）
- 必要に応じて抑制オーディエンスを定義（例：「最近受信したオファー X」）
- オプション B の場合：実施要件オーディエンスがエッジ評価の対象となっていることを確認します。セグメントルール式での時系列クエリや複雑な集計を避けます

#### オプションが異なる場所

**オプション A （Email Decisioning）の場合：**
バッチまたはストリーミングの評価で十分です。 オーディエンスは、キャンペーンの実行前または実行中に評価されます。 時間ベースの条件やイベント集計を含む複雑なセグメントルール式が完全にサポートされています。

**オプション B （Web/アプリのリアルタイム）:**
Edgeの評価が必要です。 オーディエンスでは、単純な属性チェックまたはセグメントメンバーシップ条件を使用する必要があります。 セグメントルール式がエッジセグメント化の対象であることを確認して、エッジの適格性をテストします。

**オプション C （ジャーニー決定ノード）の場合：**
どの評価方法も、ジャーニーエントリ条件に応じて機能します。 ジャーニーがオーディエンスベースのエントリを使用する場合、オーディエンスの評価方法はジャーニーの要件に一致します。

#### Experience League ドキュメント

- [セグメント化サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/home)
- [セグメントビルダー UI ガイド](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/segment-builder)
- [ストリーミングセグメント化](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [エッジセグメント化](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/methods/edge-segmentation)

### フェーズ 3：決定の設定

**Application 関数：** AJO:Decisioning

これは、オファーカタログ、実施要件ルール、ランキング戦略および決定ポリシーを構築するコアフェーズです。 このフェーズでは、すべての配信オプション（A、B、C）で共有する決定エンジン設定を作成します。

#### 決定：プレースメントチャネルとコンテンツ形式

オファーの表示場所と形式を決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| メール （HTML） | オプション A - メール本文内でHTMLとしてレンダリングされるオファーコンテンツ | 豊富なフォーマットをサポート。メールクライアントと互換性がある必要があります。 |
| メール （画像 URL） | オプション A - メールでホストされる画像としてレンダリングされるオファー | よりシンプル。画像はホストされ、アクセス可能である必要があり、ダイナミックテキストは不可 |
| Web （HTML） | オプション B - Web ページでHTMLとしてレンダリングされるオファー | 完全なレイアウトコントロール。インタラクティブな要素をサポート |
| Web/モバイル （JSON） | オプション B - カスタムレンダリング用に JSON として返されたオファーデータ | 最大限の柔軟性。レンダリングにはフロントエンド開発が必要 |
| コードベース（JSON） | オプション B - コードベースのエクスペリエンスサーフェスのオファーデータ | アプリケーションがレンダリングを制御；最も柔軟 |

#### 決定：ランキング戦略

実施要件を満たすオファーから最適なオファーを選択する方法を決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| 優先度ベース （手動） | 小規模なオファーカタログ。オファーの順序付けに関する明確なビジネスルール | 設定が最も簡単。オファーごとに手動で優先値を割り当て、決定論的 |
| 式ベース（カスタム式） | ランキングでは、プロファイル属性（ロイヤルティ層、最新性など）を考慮する必要があります | 柔軟。プロファイルデータを使用してランキングスコアを計算します。セグメントルール式のデザインが必要です。 |
| AI ランク （自動最適化） | 大規模なオファーカタログ。ML で時間の経過と共に選択を最適化する必要がある | モデルトレーニングには 1,000 以上のコンバージョンイベントが必要で、オファーパフォーマンスデータから学習します |

#### 決定：オファーキャッピング

オファーの表示回数に制限を設ける必要があるかどうかを決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| プロファイルごとのキャップ | 1 人の顧客に同じオファーが何度も表示されないようにする | オファーの疲労を回避し、高スループットのシナリオで数秒のラグを回避 |
| グローバルキャップ | すべてのプロファイルで 1 つのオファーの合計インプレッション数を制限します（在庫数を制限するなど） | オファーの提供を制御。上限に達すると、オファーは決定から除外されます。 |
| キャップなし | オファーの可用性に制限はありません | シンプルで、常時稼動のプロモーションに適しています。 |

**UI ナビゲーション：** コンポーネント /意思決定管理/ プレースメント / ルール / オファー/決定

#### 主要な設定の詳細

1. **プレースメントを作成** – 各プレースメントのチャネルタイプとコンテンツ形式を指定して、オファーの表示場所を定義します。
   - UI: コンポーネント /意思決定管理/ プレースメント
   - チャネルとフォーマットの組み合わせ（例：「メールヒーローバナー – HTML」、「web ホームページ - JSON」、「モバイルアプリカード - JSON」）ごとに 1 つのプレースメントを作成します

2. **実施要件ルールの定義** - プロファイル属性またはオーディエンスメンバーシップを参照するセグメントルール式を使用して、ルールを作成します。
   - UI: コンポーネント /意思決定管理/ ルール
   - ルールでは、オーディエンスメンバーシップ、プロファイル属性（ロイヤルティ層、購読タイプ）、日付制約またはコンテキストデータを参照できます

3. **パーソナライズされたオファーの作成** – すべてのプレースメントに対してコンテンツ表示域を使用して各オファーを作成し、実施要件ルールを割り当て、優先度を設定し、オプションのキャッピングを設定します。
   - UI: コンポーネント /意思決定管理/ オファー/ オファーを作成
   - 各オファーには、プレースメントごとにコンテンツ表現が必要です（例：メール用のHTML、web 用の JSON）
   - 実施要件ルールを割り当てて、各オファーを表示できるプロファイルを制御します
   - オファーの有効期限（開始/終了）とオプションのフリークエンシーキャップを設定する
   - 各オファーを承認して決定の対象にする

4. **フォールバックオファーを作成** - パーソナライズされたオファーが適格でない場合に表示されるプレースメントごとにデフォルトのオファーを作成します。
   - UI: コンポーネント /意思決定管理/ オファー/ フォールバックオファーを作成
   - フォールバックには、決定で使用されるすべてのプレースメントに対する表示域が必要です

5. **コレクション修飾子とコレクションの作成** – 修飾子タグを使用してオファーをコレクションに整理します。
   - UI: コンポーネント /意思決定管理/ コレクション修飾子
   - 決定範囲で使用する関連オファー（「夏物プロモーション」、「ロイヤルティ報酬」など）のグループ化

6. **決定ポリシーの作成** - プレースメント、コレクション、ランキング戦略およびフォールバックオファーを実行可能な決定にバインドします。
   - UI: コンポーネント /意思決定管理/決定/決定を作成
   - 各決定範囲は、プレースメントをコレクションにリンクし、ランキング方法を指定します

#### Experience League ドキュメント

- [意思決定管理の概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [プレースメントの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [決定ルールの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [パーソナライズされたオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [フォールバックオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [コレクションの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [コレクション修飾子の作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [決定を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [ランキング戦略](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### フェーズ 4：チャネルとサーフェスの設定

**アプリケーション関数：** AJO:Channel Configuration

このフェーズでは、オファーが配信されるチャネルサーフェスを設定します。 設定は、使用している実装オプションによって異なります。

#### 決定：チャネルタイプ

ユースケースで必要なメッセージングチャネルを決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| 電子メール | オプション A またはオプション C （メール配信付き） | サブドメインのデリゲーション、IP プール、送信者設定が必要 |
| Web | Web サーフェス配信のオプション B | Web SDKおよびデータストリーム設定が必要です |
| アプリ内 | モバイルアプリ配信のオプション B | モバイルSDKおよびプッシュ資格情報が必要です |
| コードベースのエクスペリエンス | カスタムレンダリングサーフェスのオプション B | 最も柔軟性が高く、アプリケーションがレンダリングを処理 |

#### オプションが異なる場所

**オプション A （Email Decisioning）の場合：**
- UI：管理/ チャネル / チャネルサーフェス / サーフェスを作成（メール）
- サブドメイン、IP プール、送信者名/メール、返信先、購読解除の設定
- 送信側サブドメインの SPF、DKIM、DMARC レコードを確認します

**オプション B （Web/アプリのリアルタイム）:**
- UI：管理/ チャネル / チャネルサーフェス / サーフェスを作成（Web またはアプリ内）
- Web の場合：web サーフェス URL パターンを設定します
- コードベースのエクスペリエンスの場合：アプリケーションのサーフェス URI を定義します
- データストリームでAJO サービスが有効になっていることを確認します

**オプション C （ジャーニー決定ノード）の場合：**
- ジャーニーで使用される各チャネル（メール、プッシュ、SMS または web）のチャネルサーフェスの設定
- 各ジャーニーメッセージアクションには、対応するアクティブなチャネルサーフェスが必要です

#### Experience League ドキュメント

- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [メールサーフェスの設定](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [サブドメインのデリゲート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [プッシュ通知チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### フェーズ 5：コンテンツと配信の設定

**Application function:** AJO：メッセージオーサリング、AJO：キャンペーン実行

このフェーズでは、選択したオファーを表示するメッセージテンプレートまたはエクスペリエンスサーフェスを設計し、配信メカニズム（キャンペーン、ジャーニーまたはコードベースのエクスペリエンス）を設定します。

#### 決定：オファーレンダリングのコンテンツアプローチ

オファーコンテンツをメッセージまたはエクスペリエンスに統合する方法を決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| メールDesignerのオファー決定コンポーネント | オプション A - メールテンプレートにオファープレースメントを埋め込む | ドラッグ&amp;ドロップ。オファーコンテンツは、決定結果に基づいて自動的にレンダリングされます |
| 決定ポリシーによるコードベースのエクスペリエンス | オプション B - アプリケーションはオファーデータを取得し、レンダリングします。 | レンダリングを最大限に制御。フロントエンド開発が必要 |
| 意思決定が埋め込まれたジャーニーメッセージアクション | オプション C – 決定ノードがオファーコンテンツをジャーニーメッセージにフィードします。 | オファーの選択と配信は、ジャーニーフロー内で調整されます |

#### 決定：キャンペーンタイプ （オプション A のみ）

これがスケジュール済みマーケティングキャンペーンか API トリガーキャンペーンかを判断します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| スケジュール済みキャンペーン | 定義済みのオーディエンスに 1 回限りのバッチまたは繰り返しバッチを送信 | 実行時に評価されるオーディエンス。日付/時刻または繰り返しを設定します |
| API トリガーキャンペーン | 指定したプロファイルに対するイベント駆動型またはシステムトリガーの送信 | トリガーペイロードで指定されたプロファイル。リクエストあたり最大 20 人の受信者をサポート |

#### オプションが異なる場所

**オプション A （Email Decisioning）の場合：**

1. メールDesignerを使用したメールメッセージの作成
   - UI: キャンペーン/キャンペーンを作成/メールを選択/コンテンツを編集
   - オファーの決定コンポーネントをメールレイアウトに挿入して、プレースメントゾーンを定義します
   - プロファイルレベルのコンテンツ（名前、ロイヤルティ層）のパーソナライゼーショントークンの追加
   - オプションのパーソナライゼーションを使用した件名とプリヘッダーの設定
2. キャンペーンの作成と設定
   - UI: キャンペーン/キャンペーンを作成/スケジュール済みまたは API トリガー
   - ターゲットオーディエンスをバインドし、チャネルサーフェスを選択します
   - 実行スケジュールまたは APIトリガー設定を指定
   - キャンペーンのレビューとアクティブ化

**オプション B （Web/アプリのリアルタイム）:**

1. コードベースのエクスペリエンスまたは web チャネルの設定
   - UI: キャンペーン/キャンペーンを作成/コードベースのエクスペリエンス（または web）
   - 決定ポリシーのエクスペリエンスサーフェスへのリンク
   - レンダリング形式を定義します（コードベースの場合は JSON 応答、web チャネルの場合はビジュアルエディター）。
2. クライアントサイドレンダリングの実装
   - Web SDK `sendEvent` 応答を使用して、選択したオファーを取得します
   - ページ上の指定されたプレースメントでのオファーコンテンツのレンダリング
   - インプレッションとクリックの追跡の実装

**オプション C （ジャーニー決定ノード）の場合：**

1. 決定ノードを使用したジャーニーの設計
   - UI:ジャーニー/ジャーニーを作成/決定ノードを追加
   - 決定ノードを設定して、フェーズ 3 の決定ポリシーを呼び出します。
2. 決定後のメッセージアクションノードの追加
   - 選択したオファーを参照するメール、プッシュまたは SMS アクションを設定
   - オファーエンゲージメントに基づいて待機手順、条件またはブランチを追加
3. ジャーニーの公開

#### Experience League ドキュメント

- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [キャンペーンの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [ジャーニーの概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [コンテンツのプレビューとテスト](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### フェーズ 6：テストと検証

**アプリケーション関数：** AJO：決定、AJO：メッセージオーサリング

このフェーズでは、決定エンジンがテストプロファイルに対して正しいオファーを返し、オファーコンテンツが各配信チャネルで正しくレンダリングされることを検証します。

#### 決定ロジックのテスト

既知の属性を持つテストプロファイルを使用して、実施要件とランキングに基づいて正しいオファーが選択されていることを確認します。

- 異なる実施要件条件に一致するテストプロファイルを作成します（ゴールド層、シルバー層、体験版ユーザーなど）。
- 各テストプロファイルが想定されるオファーを受け取ることを確認します
- 実施要件ルールに一致しないプロファイルがフォールバックオファーを受け取ることを確認

#### コンテンツのレンダリングのテスト

各配信チャネルでオファーコンテンツをプレビューします。

- オプション A の場合：テストプロファイルでメールプレビューを使用して、オファーコンテンツが正しくレンダリングされていることを確認します
- オプション B：ステージング環境でEdge Decisioning 応答をテストする
- オプション C の場合：ジャーニーテストモードを使用して、決定ノードが正しく選択されていることを確認します

#### インプレッショントラッキングの検証

オファーインプレッション数、クリック数およびコンバージョンを追跡中であることを確認します。

- オファーインタラクションイベントがトラッキングデータセットに表示されることを確認
- オファーインプレッション数とダウンストリームコンバージョン数の間のアトリビューションの確認

#### Experience League ドキュメント

- [コンテンツのプレビューとテスト](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [メールの配達確認の送信](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/preview-test/proofs)

### フェーズ 7：レポートとパフォーマンス監視の設定

**アプリケーション機能：** AJO:Reporting &amp; Performance Analysis

このフェーズでは、オファー選択配分、承認率、コンバージョンの影響およびフォールバック率を追跡するレポートを設定します。 このフェーズでは、AJOのネイティブレポートと、CJAベースのクロスチャネル分析の両方を扱います。

#### 決定：レポート方法

オファーパフォーマンス分析に必要なレポートツールを決定します。

| オプション | 選択すべき状況 | 検討事項 |
| --- | --- | --- |
| AJO ネイティブレポートのみ | 個々のキャンペーンまたはジャーニーの運用上の監視 | 迅速なアクセス、組み込みの配信およびエンゲージメント指標、限定的なクロスエンティティ分析 |
| CJA workspace analysis | クロスチャネルオファーの有効性、売上高アトリビューション、funnel分析 | CJAの接続とデータビュー、より深い分析機能が必要 |
| AJOとCJA | 運用および分析に関する包括的なサービス | 実稼動実装にお勧めします。リアルタイム監視のためのAJOや戦略的分析のためのCJAです。 |

#### 主要な設定の詳細

1. **AJOのネイティブレポート** – 組み込みレポートを使用して、キャンペーンまたはジャーニーのパフォーマンスを監視します。
   - UI: キャンペーン/キャンペーンを選択/全期間レポート（またはライブレポート）
   - オファー固有の指標（オファーあたりのインプレッション数、オファーあたりのクリックスルー率、フォールバック率）を確認します。
   - 配信の監視funnel: ターゲット/送信済み/配信済み/開封数/クリック数

2. **CJA分析（推奨）** - クロスチャネルオファーのパフォーマンスダッシュボードを作成します。
   - AJO オファーインタラクションデータセットを含むCJA接続の設定
   - オファー固有のディメンション（オファー名、プレースメント、決定）と指標（インプレッション数、クリック数、コンバージョン数）を使用してデータビューを作成します
   - ワークスペース分析の作成対象：オファー選択配分、セグメント別の受け入れ率、収益への影響、クロスチャネルオファーの一貫性

#### Experience League ドキュメント

- [キャンペーンのグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/home)

## 実装に関する考慮事項

このセクションでは、Offer Decisioning 実装のガードレール、一般的な落とし穴、ベストプラクティスおよびトレードオフの決定について説明します。

### ガードレールと制限

実装を計画する際は、次のプラットフォームガードレールおよび制限に注意してください。

- サンドボックスあたり最大 10,000 件の承認されたパーソナライズされたオファー – [&#x200B; 意思決定管理ガードレール &#x200B;](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/guardrails)
- 決定あたりの最大 30 個のプレースメント
- 決定リクエストあたり最大 30 個のコレクション範囲
- AI ランキングモデルでは、トレーニングに 1,000 以上のコンバージョンイベントが必要です
- オファーキャッピングカウンターは、高スループットのシナリオでは、最大で数秒の遅延が発生する場合があります
- Edgeの決定は、エッジプロファイルストアで使用できるプロファイル属性に制限されます
- サンドボックスあたり最大 4,000 個のセグメント定義 – [Platform ガードレール &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/guardrails)
- サンドボックスごとにEdgeでアクティブにできる結合ポリシーは 1 つだけです
- 1 つのサンドボックスにつき最大 500 個のアクティブなライブキャンペーン
- ジャーニーのエントリレート制限：1 秒あたり 5,000 プロファイル
- サンドボックスあたりのチャネルタイプあたり最大 10 個のチャネルサーフェス

### よくある落とし穴

実装時によく発生するこれらの問題を回避します。

- **決定は、常にフォールバックオファーを返します。** これは通常、パーソナライズされたオファーが承認されていないか、有効期限範囲外にあるか、実施要件ルールがテストプロファイルの属性に一致しないことを意味します。 承認ステータス、日付範囲、セグメントルール式の精度の各条件を確認します。 また、キャッピング制限に達していないことも確認します。
- **コレクションにオファーが表示されません：** オファーが正しいコレクション修飾子でタグ付けされており、コレクションフィルターが一致していることを確認します。 コレクションベースの決定範囲に表示するには、オファーがタグ付けされ、承認されている必要があります。
- **ランキング式が適用されていません：** 式が構文的に有効で、アクセス可能なプロファイル属性を参照していることを確認してください。 数式エラーは、エラーが表示されない優先度ベースのランキングにサイレントにフォールバックします。
- **Edge配信は、空のパーソナライゼーションを返します。** データストリームが、[!DNL Adobe Journey Optimizer] サービスが有効に設定され、決定範囲が正しくフォーマットされていることを確認してください。 エッジアクティブな結合ポリシーが存在することを確認します。
- **チャネル間でオファーに一貫性がない：** チャネルごとに個別の決定ポリシーを使用する場合、同じプロファイルが異なるオファーを受け取る場合があります。 一貫性を保つため、チャネル全体で単一の決定ポリシーを使用するか、チャネル固有の配置に基づいて意図的に異なるを受け入れます。
- **オファーコンテンツがメールでレンダリングされない：** オファーのコンテンツ表現がメールのプレースメント形式（HTMLまたは画像 URL）に一致することを確認します。 表示域が見つからない場合、プレースメントゾーンが空白になります。

### ベストプラクティス

Offer Decisioning を正常に実装するには、次の推奨事項に従います。

- **小さなオファーカタログから開始して繰り返し処理** - 5 ～ 10 個のオファーから始め、決定フレームワークが検証されたら拡張します。 これにより、トラブルシューティングが簡単になり、スケーリング前に実施要件ルールが正しく機能するようになります。
- **コレクション修飾子の戦略的な使用** - カテゴリ別のタグオファー（「獲得」、「リテンション」、「アップセル」など）を使用すると、キャンペーンやジャーニー全体で再利用できる柔軟なコレクションベースの決定範囲を有効にできます。
- **常に意味のあるフォールバックオファーを作成** — フォールバックオファーは、単なるセーフティネットではなく、実施要件ルールに一致しないプロファイルのデフォルトエクスペリエンスです。 パーソナライゼーションがなくても価値を提供できるフォールバックコンテンツに投資します。
- **可能な場合は、相互排他的に実施要件ルールをデザイン** – 複数のオファーの実施要件が重複している場合、ランキング戦略が重要になります。 ビジネス要件によって特定のセグメントに対する特定のオファーが定められている場合は、ランキングのみに依存するのではなく、実施要件ルールを相互に排他的にします。
- **オプション B のエッジを代表するプロファイルを使用したテスト** — Edge プロファイルには、ハブプロファイル属性のサブセットが含まれています。 エッジで利用可能な属性を持つプロファイルを使用したテストにより、実稼動環境で実施要件が正しく評価されることを確認します。
- **ヘルス指標としてフォールバック率を監視** – 高いフォールバック率（20～30% を超える）は、オファーカタログが十分な顧客セグメントをカバーしていないことを示します。 オファーカタログを展開するか、実施要件ルールを拡張します。
- **ライブの決定を編集するのではなく、バージョン決定ポリシーを作成** - アクティブな決定ポリシーを変更するのではなく、新しい決定ポリシーバージョンを作成します。 これにより、ライブキャンペーンの中断を防ぎ、決定戦略の A/B 比較を可能にします。

### トレードオフの決定

アーキテクチャと設定に関する決定を行う際は、次のトレードオフを考慮します。

#### 実施要件の精度とオファーの対象範囲

厳格な実施要件ルールにより、各オファーは最も関連性の高いプロファイルにのみ到達しますが、プロファイルがどのオファーにも一致しない場合、フォールバック率が高くなる可能性があります。 広範な実施要件ルールにより、オファーの範囲が最大化されますが、パーソナライゼーションの精度が低下します。

- **適格要件に対するきめ細かい支持：** 受け入れ率の向上、パーソナライゼーションの強化、オファー疲れの軽減
- **幅広い実施要件の支持：** フォールバック率が低くなり、より多くのプロファイルがパーソナライズされたオファーを受け取り、ルール管理を簡素化します
- **推奨事項：** より広い実施要件ルールから始めて、パフォーマンスデータに基づいて強化します。 フォールバック率と許容率を監視して、適切なバランスを見つけます。 ランキング戦略を使用して、大まかに実施要件を満たすオファー間を区別します。

#### 優先度ベースのランキングと AI ランクのランキングの比較

優先度ベースのランキングは、ビジネスにどのオファーを表示するかを完全に制御するのに対して、AI ランキングは、コンバージョンを最適化しますが、オファー選択に対する人間の制御を減らします。

- **優先度ベースのメリット：** ビジネス管理、予測可能性、トレーニング・データの必要性なし、迅速な導入
- **AI の活用：** 変換の最適化、想定外パターンの発見、お客様の行動変化への自動適応
- **推奨事項：** ビジネス管理が最も重要な場合に、最初のローンチや規制に敏感なオファーに対して優先度ベースのランキングを使用します。 十分なコンバージョンデータ（1,000 以上のイベント）が利用可能になったら、パフォーマンスが最適化された、大量のユースケースに対して AI ランクに移行します。

#### 単一の決定ポリシーとチャネルごとの決定ポリシーの比較

単一の決定ポリシーにより、すべてのチャネルにわたるオファーの一貫性が確保されますが、チャネルごとの最適化は制限されます。 チャネルごとのポリシーを使用すると、チャネル固有のランキングと実施要件を設定できますが、カスタマーエクスペリエンスに一貫性がなくなるリスクがあります。

- **単一ポリシーのメリット：** クロスチャネルの一貫性、シンプルな管理、統一されたレポート
- **チャネルごとのポリシーの適用：** チャネルに最適化されたランキング、チャネル固有の実施要件（web 専用オファーなど）、独立したイテレーション
- **推奨事項：** チャネル間の一貫性を保つため、単一の決定ポリシーから始める。 ビジネス要件によりチャネル固有のオファー戦略が必要な場合にのみ、チャネルごとのポリシーを作成します（web 専用のフラッシュ販売など）。

#### Hub Decisioning （オプション A/C）と Edge Decisioning （オプション B）

Hub Decisioning はプロファイル全体にアクセスできますが、送信時に動作します。 Edge decisioning は、2 秒未満の待ち時間でリアルタイムに動作しますが、エッジで利用できるプロファイル属性に制限されています。

- **Hub Decisioning のお勧め：** 完全なプロファイルデータ、複雑な実施要件ルール、バッチキャンペーンボリュームへのアクセス
- **Edge決定のお勧め：** リアルタイムコンテキスト、セッション内パーソナライゼーション、サブ秒の応答
- **推奨事項：** 完全なプロファイルデータによってオファーの関連性が向上するアウトバウンドチャネル（メール、プッシュ）には、hub decisioning を使用します。 リアルタイムの応答が重要なインバウンドチャネル（web、アプリ）に対して edge decisioning を使用する。 エッジの実施要件ルールで、エッジで使用可能な属性のみを使用するようにします。

## 関連ドキュメント

次のリソースでは、このユースケースパターンで使用されるコンポーネントの追加詳細を説明しています。

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

### オファー配信

- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Edge Decisioning API を使用したオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Decisioning API を使用したオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/decisioning-api)

### チャネル設定

- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [メールサーフェスの設定](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [サブドメインのデリゲート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [プッシュ通知チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [SMS チャネルの設定](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### メッセージのオーサリングとパーソナライズ機能

- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [コンテンツのプレビューとテスト](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### キャンペーンとジャーニー

- [キャンペーンの基本を学ぶ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [キャンペーンの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [ジャーニーの概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/orchestrate-journeys/journey)

### コンテンツ実験

- [コンテンツ実験の基本を学ぶ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [コンテンツ実験を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)

### オーディエンスとセグメント化

- [セグメント化サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/home)
- [セグメントビルダー UI ガイド](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/segment-builder)
- [ストリーミングセグメント化](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [エッジセグメント化](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/methods/edge-segmentation)

### プロファイルと ID

- [ID サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/home)
- [結合ポリシーの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/merge-policies/overview)
- [計算済み属性の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/computed-attributes/overview)
- [顧客 AI の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/intelligent-services/customer-ai/overview)

### データモデリングと収集

- [XDM システムの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/home)
- [Web SDKの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/home)
- [データストリームを設定](https://experienceleague.adobe.com/ja/docs/experience-platform/datastreams/configure)

### レポートと分析

- [キャンペーンのグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [CJAの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/home)

### データガバナンスとライフサイクル

- [データガバナンスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/home)
- [データ使用状況ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview)
- [高度なデータ・ライフサイクル管理の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-lifecycle/home)
- [Journey Optimizerの同意](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### ガードレール

- [Journey Optimizer ガードレール](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/guardrails)
- [リアルタイム顧客プロファイルガードレール](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/guardrails)

### チュートリアル

- [意思決定管理 API の概要](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/getting-started)
