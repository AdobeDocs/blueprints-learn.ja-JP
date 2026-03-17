---
title: ユースケースカタログ
description: 業種、成熟度レベル、実装パターン別に業界のユースケースを参照して、Adobe Experience Platform ジャーニーに適切な出発点を見つけます。
doc-type: overview-page
exl-id: 7a3c2f1e-9b4d-4e6a-8f5c-2d1b3a4e7c9f
source-git-commit: 8ad59ff130dae13553f10049eb685cf557a73ead
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 6%

---

# ユースケースカタログ

[!DNL Adobe Experience Platform] とアプリケーションの業界でのユースケースを確認します。 業界別を参照して業種ごとのユースケースを確認したり、成熟度レベル別に組織の適切な出発点を見つけたり、実装パターン別に参照してニーズに合った技術的アプローチを把握したりできます。

各ユースケースは、ユースケースパターンを通じて詳細な実装ガイダンスにリンクしています。これは、ユースケースを実現するために必要な機能チェーン、決定ポイントおよび設定手順を説明しています。

## 業界別に参照

>[!BEGINTABS]

>[!TAB  小売 ]

小売組織は、[!DNL Adobe Experience Platform] を使用して、オンラインストア、物理的な場所、ロイヤルティプログラムの顧客データを統合して、各買い物客の単一のビューにまとめます。

| | ユースケース | 説明 | 成熟度 | パターン |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="パーソナライズされた製品レコメンデーション" width="40"> | [&#x200B; パーソナライズされた製品レコメンデーション &#x200B;](retail/retail-overview.md#personalized-product-recommendations) | 閲覧および購入履歴に基づいてパーソナライズされた製品を表示します | [!BADGE &#x200B; 新興 &#x200B;]{type=Informative} | [&#x200B; 行動に関する推奨事項 &#x200B;](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="放棄されたカート" width="40"> | [&#x200B; 放棄された買い物かごのメール復元 &#x200B;](retail/retail-overview.md#abandoned-cart-email-recovery) | 放棄された買い物かごに対するパーソナライズされたリマインダーの送信 | [!BADGE &#x200B; 基礎知識 &#x200B;]{type=Neutral} | [&#x200B; イベントトリガーメッセージ &#x200B;](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="在庫の緊急度" width="40"> | [&#x200B; 在庫ベースの緊急度キャンペーン &#x200B;](retail/retail-overview.md#inventory-based-urgency-campaigns) | 商品インベントリが少ない場合のトリガーリアルタイムアラート | [!BADGE &#x200B; 基礎知識 &#x200B;]{type=Neutral} | [&#x200B; イベントトリガーメッセージ &#x200B;](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="クロスセルのアップセル" width="40"> | [&#x200B; クロスセルとアップセルの推奨事項 &#x200B;](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | チェックアウト時およびメールでの関連するクロスセル製品およびアップセル製品の表示 | [!BADGE &#x200B; 詳細 &#x200B;]{type=Caution} | [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="ウェルカムシリーズ" width="40"> | [&#x200B; 新しい Customer Welcome シリーズ &#x200B;](retail/retail-overview.md#new-customer-welcome-series) | パーソナライズされたレコメンデーションを使用した、複数のメールを含むウェルカムシリーズの自動化 | [!BADGE &#x200B; 新興 &#x200B;]{type=Informative} | [&#x200B; 複数ステップの調整されたジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="価格の下落" width="40"> | [&#x200B; 価格下落アラート &#x200B;](retail/retail-overview.md#price-drop-alerts) | ウィッシュリストや閲覧したアイテムの価格が下がった場合に顧客に通知する | [!BADGE &#x200B; 基礎知識 &#x200B;]{type=Neutral} | [&#x200B; イベントトリガーメッセージ &#x200B;](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="補充" width="40"> | [&#x200B; 補充リマインダ &#x200B;](retail/retail-overview.md#replenishment-reminders) | 定期的に購入した消耗品に対する自動リマインダーの送信 | [!BADGE &#x200B; 新興 &#x200B;]{type=Informative} | [&#x200B; 複数ステップの調整されたジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="カテゴリページ" width="40"> | [&#x200B; パーソナライズされたカテゴリページ &#x200B;](retail/retail-overview.md#personalized-category-pages) | 各顧客の環境設定に基づいてカテゴリページを動的に並べ替える | [!BADGE &#x200B; 新興 &#x200B;]{type=Informative} | [&#x200B; 行動に関する推奨事項 &#x200B;](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="購入後" width="40"> | [&#x200B; 購入後のフォローアップキャンペーン &#x200B;](retail/retail-overview.md#post-purchase-follow-up-campaigns) | ケアに関するヒント、レビューリクエストおよび関連する製品の提案の送信 | [!BADGE &#x200B; 新興 &#x200B;]{type=Informative} | [&#x200B; 複数ステップの調整されたジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| | [VIPのお客様向け限定オファー &#x200B;](retail/retail-overview.md#vip-customer-exclusive-offers) | 価値の高い顧客に限定オファーと早期アクセスを提供 | [!BADGE &#x200B; 詳細 &#x200B;]{type=Caution} | [Decisioning を使用したクロスチャネルジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |
| | [&#x200B; 在庫切れの通知 &#x200B;](retail/retail-overview.md#out-of-stock-notifications) | 在庫切れの製品が利用可能になった際に顧客に通知 | [!BADGE &#x200B; 基礎知識 &#x200B;]{type=Neutral} | [&#x200B; イベントトリガーメッセージ &#x200B;](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| | [&#x200B; ソーシャルプルーフPersonalization](retail/retail-overview.md#social-proof-personalization) | 顧客プロファイルに基づいてパーソナライズされたレビューと評価の表示 | [!BADGE &#x200B; 新興 &#x200B;]{type=Informative} | [&#x200B; 既知の訪問者の Web/アプリPersonalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) |

>[!TAB  金融サービス ]

金融サービスのユースケースについては、近日中に提供を開始します。[現在の Financial Services の使用例 &#x200B;](financial-services/financial-services-overview.md) 表示します。

>[!TAB  ヘルスケア ]

ヘルスケアのユースケースは、近日中に提供されます。[現在のヘルスケアのユースケース &#x200B;](healthcare/healthcare-overview.md) 表示

>[!TAB  自動車 ]

自動車のユースケースは、近日中に提供されます。[現在の自動車のユースケースを見る &#x200B;](automotive/automotive-overview.md)

>[!TAB  旅行・ホスピタリティ ]

旅行およびホスピタリティのユースケースについては、近日中に提供されます。[現在の旅行およびホスピタリティのユースケース &#x200B;](travel-hospitality/travel-hospitality-overview.md) 表示します。

>[!TAB  電気通信 ]

通信関連のユースケースについては、近日中に提供を開始します。[現在の通信の使用例 &#x200B;](telecommunications/telecommunications-overview.md) 表示します。

>[!TAB  メディア&amp;エンターテインメント ]

メディアとエンターテインメントのユースケースは、近日中に提供されます。[現在のメディアおよびエンターテインメントのユースケースを表示 &#x200B;](media-entertainment/media-entertainment-overview.md) ます。

>[!TAB  保険 ]

保険のユースケースについては、近日中にお知らせします。[現在の保険の使用例 &#x200B;](insurance/insurance-overview.md) 表示します。

>[!TAB B2B]

B2B のユースケースは、近日中に提供されます。[現在の B2B のユースケースを表示 &#x200B;](b2b/b2b-overview.md)

>[!ENDTABS]

## 成熟度レベルで参照

>[!BEGINTABS]

>[!TAB  基礎知識 ]

シングルチャネル配信を使用した、基本的で実証済みのパターン。 [!DNL Experience Platform] ジャーニーを開始する組織にとって理想的な出発点です。

| | ユースケース | 業種 | ビジネスへの影響 | パターン |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="放棄されたカート" width="40"> | [&#x200B; 放棄された買い物かごのメール復元 &#x200B;](retail/retail-overview.md#abandoned-cart-email-recovery) | 小売 | 買い物かごの回復率 25～35% | [&#x200B; イベントトリガーメッセージ &#x200B;](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="在庫の緊急度" width="40"> | [&#x200B; 在庫ベースの緊急度キャンペーン &#x200B;](retail/retail-overview.md#inventory-based-urgency-campaigns) | 小売 | コンバージョン率が 30～40% 向上 | [&#x200B; イベントトリガーメッセージ &#x200B;](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="価格の下落" width="40"> | [&#x200B; 価格下落アラート &#x200B;](retail/retail-overview.md#price-drop-alerts) | 小売 | コンバージョン率 20～30% | [&#x200B; イベントトリガーメッセージ &#x200B;](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| | [&#x200B; 在庫切れの通知 &#x200B;](retail/retail-overview.md#out-of-stock-notifications) | 小売 | コンバージョン率 40～50% | [&#x200B; イベントトリガーメッセージ &#x200B;](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |

>[!TAB  新興 ]

AI 駆動型パーソナライゼーションと調整されたジャーニーにより、基本機能に基づいて構築されたマルチチャネルおよびマルチステップパターン。

| | ユースケース | 業種 | ビジネスへの影響 | パターン |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="製品レコメンデーション" width="40"> | [&#x200B; パーソナライズされた製品レコメンデーション &#x200B;](retail/retail-overview.md#personalized-product-recommendations) | 小売 | CTR が 20～30% 増加、コンバージョン率が 15～25% 向上 | [&#x200B; 行動に関する推奨事項 &#x200B;](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="カテゴリページ" width="40"> | [&#x200B; パーソナライズされたカテゴリページ &#x200B;](retail/retail-overview.md#personalized-category-pages) | 小売 | エンゲージメントが 25～35% 増加 | [&#x200B; 行動に関する推奨事項 &#x200B;](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="ウェルカムシリーズ" width="40"> | [&#x200B; 新しい Customer Welcome シリーズ &#x200B;](retail/retail-overview.md#new-customer-welcome-series) | 小売 | エンゲージメント率 40～50% | [&#x200B; 複数ステップの調整されたジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="補充" width="40"> | [&#x200B; 補充リマインダ &#x200B;](retail/retail-overview.md#replenishment-reminders) | 小売 | リピート購入率 30～40% | [&#x200B; 複数ステップの調整されたジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="購入後" width="40"> | [&#x200B; 購入後のフォローアップキャンペーン &#x200B;](retail/retail-overview.md#post-purchase-follow-up-campaigns) | 小売 | レビュー率 15～20%、リピート購入 10～15% | [&#x200B; 複数ステップの調整されたジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| | [&#x200B; ソーシャルプルーフPersonalization](retail/retail-overview.md#social-proof-personalization) | 小売 | コンバージョン率が 10～15% 向上 | [&#x200B; 既知の訪問者の Web/アプリPersonalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) |

>[!TAB  詳細 ]

最も高度な顧客体験のためのリアルタイム意思決定と AI 駆動のオファー選択を使用したクロスチャネルオーケストレーション。

| | ユースケース | 業種 | ビジネスへの影響 | パターン |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="クロスセルのアップセル" width="40"> | [&#x200B; クロスセルとアップセルの推奨事項 &#x200B;](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | 小売 | AOV が 25～75 ドル増加、売上収益が 10～15% 増加 | [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) |
| | [VIPのお客様向け限定オファー &#x200B;](retail/retail-overview.md#vip-customer-exclusive-offers) | 小売 | VIP からのエンゲージメント率 50～70% | [Decisioning を使用したクロスチャネルジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |

>[!ENDTABS]

## 実装パターンで参照

>[!BEGINTABS]

>[!TAB  キャンペーン管理とオーケストレーション ]

### イベントトリガーメッセージ

タイムリーな単一チャネルメッセージでリアルタイムの行動イベントに対応します。

| | ユースケース | 業種 | 成熟度 | ビジネスへの影響 |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="放棄されたカート" width="40"> | [&#x200B; 放棄された買い物かごのメール復元 &#x200B;](retail/retail-overview.md#abandoned-cart-email-recovery) | 小売 | [!BADGE &#x200B; 基礎知識 &#x200B;]{type=Neutral} | 買い物かごの回復率 25～35% |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="在庫の緊急度" width="40"> | [&#x200B; 在庫ベースの緊急度キャンペーン &#x200B;](retail/retail-overview.md#inventory-based-urgency-campaigns) | 小売 | [!BADGE &#x200B; 基礎知識 &#x200B;]{type=Neutral} | コンバージョン率が 30～40% 向上 |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="価格の下落" width="40"> | [&#x200B; 価格下落アラート &#x200B;](retail/retail-overview.md#price-drop-alerts) | 小売 | [!BADGE &#x200B; 基礎知識 &#x200B;]{type=Neutral} | コンバージョン率 20～30% |
| | [&#x200B; 在庫切れの通知 &#x200B;](retail/retail-overview.md#out-of-stock-notifications) | 小売 | [!BADGE &#x200B; 基礎知識 &#x200B;]{type=Neutral} | コンバージョン率 40～50% |

### 複数ステップの調整されたジャーニー

エンゲージメントと行動に基づいて適応するマルチタッチシーケンスを通じて、顧客をガイドします。

| | ユースケース | 業種 | 成熟度 | ビジネスへの影響 |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="ウェルカムシリーズ" width="40"> | [&#x200B; 新しい Customer Welcome シリーズ &#x200B;](retail/retail-overview.md#new-customer-welcome-series) | 小売 | [!BADGE &#x200B; 新興 &#x200B;]{type=Informative} | エンゲージメント率 40～50% |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="補充" width="40"> | [&#x200B; 補充リマインダ &#x200B;](retail/retail-overview.md#replenishment-reminders) | 小売 | [!BADGE &#x200B; 新興 &#x200B;]{type=Informative} | リピート購入率 30～40% |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="購入後" width="40"> | [&#x200B; 購入後のフォローアップキャンペーン &#x200B;](retail/retail-overview.md#post-purchase-follow-up-campaigns) | 小売 | [!BADGE &#x200B; 新興 &#x200B;]{type=Informative} | レビュー率 15～20%、リピート購入 10～15% |

### Decisioning を使用したクロスチャネルジャーニー

すべてのタッチポイントでリアルタイムの Offer Decisioning を使用してクロスチャネルエクスペリエンスを調整します。

| | ユースケース | 業種 | 成熟度 | ビジネスへの影響 |
| --- | --- | --- | --- | --- |
| | [VIPのお客様向け限定オファー &#x200B;](retail/retail-overview.md#vip-customer-exclusive-offers) | 小売 | [!BADGE &#x200B; 詳細 &#x200B;]{type=Caution} | VIP からのエンゲージメント率 50～70% |

>[!TAB Personalization]

### 行動の推奨事項

AI 駆動モデルを使用して、行動シグナルに基づいてパーソナライズされたコンテンツや製品を表示します。

| | ユースケース | 業種 | 成熟度 | ビジネスへの影響 |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="製品レコメンデーション" width="40"> | [&#x200B; パーソナライズされた製品レコメンデーション &#x200B;](retail/retail-overview.md#personalized-product-recommendations) | 小売 | [!BADGE &#x200B; 新興 &#x200B;]{type=Informative} | CTR が 20～30% 増加、コンバージョン率が 15～25% 向上 |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="カテゴリページ" width="40"> | [&#x200B; パーソナライズされたカテゴリページ &#x200B;](retail/retail-overview.md#personalized-category-pages) | 小売 | [!BADGE &#x200B; 新興 &#x200B;]{type=Informative} | エンゲージメントが 25～35% 増加 |

### Offer Decisioning

一元的な決定ロジックを使用して、顧客やコンテキストごとに最適なオファーを評価および選択します。

| | ユースケース | 業種 | 成熟度 | ビジネスへの影響 |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="クロスセルのアップセル" width="40"> | [&#x200B; クロスセルとアップセルの推奨事項 &#x200B;](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | 小売 | [!BADGE &#x200B; 詳細 &#x200B;]{type=Caution} | AOV が 25～75 ドル増加、売上収益が 10～15% 増加 |

### 既知の訪問者の Web/アプリPersonalization

プロファイル、環境設定および閲覧コンテキストに基づいて、特定された訪問者のために web およびアプリのコンテンツをパーソナライズします。

| | ユースケース | 業種 | 成熟度 | ビジネスへの影響 |
| --- | --- | --- | --- | --- |
| | [&#x200B; ソーシャルプルーフPersonalization](retail/retail-overview.md#social-proof-personalization) | 小売 | [!BADGE &#x200B; 新興 &#x200B;]{type=Informative} | コンバージョン率が 10～15% 向上 |

>[!ENDTABS]
