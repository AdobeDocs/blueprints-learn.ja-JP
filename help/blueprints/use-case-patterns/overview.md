---
title: ユースケースパターン
description: Adobe Adobe Experience Platformを実装するためのユースケースパターンと、主要なビジネス目標を達成するためのアプリケーションについて解説します。
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
doc-type: overview-page
exl-id: 58caa6ad-0d1c-4290-9614-c68c9c9028bb
source-git-commit: 27f7e230982807ec70ca96af7f737944a6588f27
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# ユースケースパターン

ユースケースパターンは、Adobe Experience Platformとアプリケーションの繰り返し可能な実装アプローチを定義します。 各パターンは、特定の機能、それを提供する機能チェーン、関連するアプリケーション、およびそれがサポートする[主なビジネス目標](/help/blueprints/business-objectives/overview.md)を表します。

以下の表を使用して、実装ニーズに一致するパターンを見つけ、オプション、フェーズ、決定ガイダンス、Experience League ドキュメントなどの実装リファレンスへのリンクに従います。

## オーディエンスの構築とアクティベーション

次のパターンは、チャネルと配信先をまたいでオーディエンスセグメントを構築、評価、活用するのに役立ちます。

| パターン | プライマリ能力 | コアソリューション |
| --- | --- | --- |
| [宛先へのオーディエンスアクティベーション ](audience-building-activation/audience-activation-to-destinations.md) | ターゲティングまたは抑制のために、オーディエンスセグメントを評価して外部宛先に公開します | [!DNL Real-Time CDP] |
| [Audience Collaboration](audience-building-activation/audience-collaboration-segment-match.md) | Segment Matchを使用すると、サンドボックスや組織間でオーディエンスセグメントを共有して一致させることができます | [!DNL Real-Time CDP], [!DNL Experience Platform] |
| [ イベント転送](audience-building-activation/event-forwarding.md) | Edge Networkを通じて収集したリアルタイムのイベントデータを、Adobe以外の宛先に転送します | [!DNL Experience Platform] （Edge Network、イベント転送） |
| [B2B オーディエンスのアクティブ化](audience-building-activation/b2b-audience-activation.md) | web、電子メール、広告のチャネルをまたいで、アカウントベースのB2B オーディエンスを活用できます | [!DNL Real-Time CDP] B2B edition |

## パーソナライズ機能

次のパターンは、webとアプリのサーフェスをまたいで、既知の訪問者と未知の訪問者に合わせたエクスペリエンスを提供します。

| パターン | プライマリ能力 | コアソリューション |
| --- | --- | --- |
| [匿名の訪問者のweb パーソナライゼーション ](personalization/anonymous-visitor-web-personalization.md) | セッション中の行動シグナルにもとづいて、パーソナライズされたコンテンツを配信し、未特定の訪問者に提供します | [!DNL Journey Optimizer] （web チャネル）、[!DNL Real-Time CDP] |
| [既知の訪問者のweb/アプリのパーソナライゼーション ](personalization/known-visitor-web-app-personalization.md) | リアルタイムのプロファイルとセグメントメンバーシップにもとづいて、特定された訪問者にパーソナライズされたコンテンツ、オファー、プロモーションを配信します | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [ オファー決定](personalization/offer-decisioning.md) | 一元化された意思決定ロジックを使用して、チャネルをまたいでプロファイルに最適なオファーやコンテンツを選択します | [!DNL Journey Optimizer] （決定）、[!DNL Real-Time CDP] |
| [行動レコメンデーション ](personalization/behavioral-recommendation.md) | 選択戦略とランキングモデルを使用して、アイテムとコンテンツのレコメンデーションを生成します | [!DNL Journey Optimizer] （決定）、[!DNL Real-Time CDP] |

## キャンペーン管理とオーケストレーション

次のパターンは、スケジュール済み、トリガー済み、マルチステップのメッセージ配信を、チャネルをまたいで取り扱います。

| パターン | プライマリ能力 | コアソリューション |
| --- | --- | --- |
| [ バッチアウトバウンドメッセージのアクティベーション ](campaign-management-orchestration/batch-outbound-message-activation.md) | オーディエンスを評価し、スケジュールされたアウトバウンドメッセージを1回のバッチで配信します | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [ イベントトリガーのメッセージ ](campaign-management-orchestration/event-triggered-messaging.md) | リアルタイムの行動イベントやシステムイベントをリッスンし、トリガープロファイルにコンテキストメッセージを配信します | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [ マルチステップ オーケストレーション ジャーニー](campaign-management-orchestration/multi-step-orchestrated-journey.md) | 待機、条件、複数のメッセージアクションを含む分岐マルチタッチジャーニーを通じてプロファイルを導きます | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [決定を伴うクロスチャネルジャーニー](campaign-management-orchestration/cross-channel-journey-with-decisioning.md) | リアルタイムの意思決定を組み込んだマルチステップのジャーニーを編成し、最適なチャネル、コンテンツ、オファーを選択できます | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [購買グループベースのマーケティングとジャーニー管理](campaign-management-orchestration/buying-group-based-marketing.md) | リードを購買グループに選別するアカウントレベルのジャーニーを作成して、B2B マーケティングの効果を向上できます | [!DNL Journey Optimizer] B2B edition、[!DNL Real-Time CDP] B2B edition |

## 分析

次のパターンは、クロスチャネルの行動分析とパフォーマンス分析をサポートしています。

| パターン | プライマリ能力 | コアソリューション |
| --- | --- | --- |
| [顧客分析とinsightの生成](analysis/customer-analytics-insight-generation.md) | 行動とパフォーマンスの分析のために、クロスチャネルの分析ワークスペース、計算指標、ダッシュボードを構築します | [!DNL Customer Journey Analytics], [!DNL Experience Platform] |
| [B2B分析](analysis/b2b-analytics.md) | クロスチャネルのカスタマージャーニー分析にB2B アカウントレベルの情報を含める | [!DNL Customer Journey Analytics] B2B edition、[!DNL Real-Time CDP] B2B edition |

## 会話体験

次のパターンは、デジタルプロパティで、AIを活用したブランドの基準に即した、対話型のインタラクションを実現します。

| パターン | プライマリ能力 | コアソリューション |
| --- | --- | --- |
| [Brand Conciergeの会話体験](conversational-experience/brand-concierge-conversational-experience.md) | デジタルプロパティを、AIを活用したブランドの基準に即した会話体験に変換し、顧客のニーズに対応できます | [!DNL Brand Concierge], [!DNL Experience Platform], [!DNL Real-Time CDP] |

## シナリオセレクター

シナリオが複数のパターンに当てはまる可能性がある場合は、このガイドを使用します。 分岐の質問に答えてプライマリパターンを見つけ、オプションでパターンを表示して拡張します。

### インセンティブオファーによるウィンバック

*解約したお客様は、90日以内に購入していません。 ターゲットを絞ったオファーでリエンゲージメントする必要があります。*

- **オファーの選択は動的ですか（異なる顧客は、適格性またはランキングに基づいて異なるオファーを受け取ります）?**
   - はい[ オファー決定](personalization/offer-decisioning.md)をオファーレイヤーとして→用し、再エンゲージメント シーケンス用に[ マルチステップのオーケストレーションされたジャーニー](campaign-management-orchestration/multi-step-orchestrated-journey.md)に折り返します
   - [ マルチステップのオーケストレーションされたジャーニー](campaign-management-orchestration/multi-step-orchestrated-journey.md)のみ→は、（対象となるすべての解約した顧客に対して同じオファー）はありません

### 購入後のフォローアップ

*お客様は購入を完了しました。 確認、クロスセルのレコメンデーション、およびロイヤルティ報酬の通知を送信する場合。*

- **シーケンスでは、リアルタイムのイベント（例：要求された報酬、レビューされた製品）に基づいてアダプティブ分岐が必要ですか？**
   - はい→ [ マルチステップ オーケストレーション ジャーニー](campaign-management-orchestration/multi-step-orchestrated-journey.md)
   - いいえ（固定シーケンス、分岐なし） → [ バッチアウトバウンドメッセージのアクティベーション ](campaign-management-orchestration/batch-outbound-message-activation.md)
- **パーソナライズされた商品レコメンデーションが含まれていますか？**
   - はい→ コンテンツ レイヤーで[行動レコメンデーション ](personalization/behavioral-recommendation.md)を使用して拡張できます

### ロイヤルティマイルストーンパーソナライゼーション

*顧客が新しいロイヤルティ階層に到達しました。 パーソナライズされたweb コンテンツを表示し、お祝いのメッセージを送信する必要があります。*

- **Web コンテンツはパーソナライズされていますか（層またはセグメントごとに異なるコンテンツ）?**
   - はい→Web サーフェスの[既知の訪問者のweb/アプリのパーソナライゼーション ](personalization/known-visitor-web-app-personalization.md)
- **送信メッセージは、1回の送信またはナーチャリング シーケンスですか？**
   - 1回→送信[ イベントトリガーメッセージ ](campaign-management-orchestration/event-triggered-messaging.md)
   - シーケンス → [ マルチステップのオーケストレーションされたジャーニー](campaign-management-orchestration/multi-step-orchestrated-journey.md)

### リエンゲージメントキャンペーン

*非アクティブなユーザーのセグメントには、マルチタッチの再アクティブ化シーケンスが必要です。*

- **個々のメッセージは、リアルタイムで複数のオファーのバリエーションから選択する必要がありますか？**
   - はい→ [意思決定を行うクロスチャネルジャーニー](campaign-management-orchestration/cross-channel-journey-with-decisioning.md)
   - → [ マルチステップ オーケストレーション ジャーニー](campaign-management-orchestration/multi-step-orchestrated-journey.md)がありません
