---
title: ユースケースパターン
description: Adobe Experience Platformとアプリケーションを実装して主要なビジネス目標を達成するためのユースケースパターンについて説明します。
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
doc-type: overview-page
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# ユースケースパターン

ユースケースパターンは、Adobe Experience Platformとアプリケーションに対して繰り返し可能な実装アプローチを定義します。 各パターンでは、特定の機能、その機能を提供する機能チェーン、関連するアプリケーション、およびサポートする [&#x200B; 主要なビジネス目標 &#x200B;](/help/blueprints/business-objectives/overview.md) が記述されています。

以下の表を使用して実装ニーズに合ったパターンを見つけたら、オプション、フェーズ、決定ガイダンス、Experience Leagueのドキュメントなど、実装に関する完全なリファレンスへのリンクに従います。

## オーディエンスの構築とアクティベーション

次のパターンは、チャネルと宛先をまたいでオーディエンスセグメントを作成、評価およびアクティブ化するのに役立ちます。

| パターン | プライマリ機能 | コアソリューション |
| --- | --- | --- |
| [&#x200B; 宛先へのAudience Activation](audience-building-activation/audience-activation-to-destinations.md) | ターゲティングまたは抑制のために、オーディエンスセグメントを評価して外部の宛先に公開します。 | [!DNL Real-Time CDP] |
| [Segment Match を使用した Audience Collaboration](audience-building-activation/audience-collaboration-segment-match.md) | Segment Match を使用した、サンドボックスまたは組織間でのオーディエンスセグメントの共有と一致 | [!DNL Real-Time CDP], [!DNL Experience Platform] |
| [&#x200B; イベントの転送 &#x200B;](audience-building-activation/event-forwarding.md) | Edge Networkを介して収集されたリアルタイムイベントデータをAdobe以外の宛先に転送する | [!DNL Experience Platform] （Edge Network、イベント転送） |
| [B2B Audience アクティベーション](audience-building-activation/b2b-audience-activation.md) | Web、メール、広告の各チャネルでアカウントベースの B2B オーディエンスをアクティブ化 | [!DNL Real-Time CDP] B2B edition |

## パーソナライズ機能

次のパターンでは、web およびアプリのサーフェス全体で、既知の訪問者と不明な訪問者に合わせたエクスペリエンスが提供されます。

| パターン | プライマリ機能 | コアソリューション |
| --- | --- | --- |
| [&#x200B; 匿名訪問者の Web Personalization](personalization/anonymous-visitor-web-personalization.md) | 未識別の訪問者に対して、セッション内の行動シグナルに基づいてパーソナライズされたコンテンツを配信する | [!DNL Journey Optimizer] （web チャネル）、[!DNL Real-Time CDP] |
| [&#x200B; 既知の訪問者の Web/アプリPersonalization](personalization/known-visitor-web-app-personalization.md) | リアルタイムのプロファイルとセグメントメンバーシップに基づいて、識別された訪問者にパーソナライズされたコンテンツ、オファーまたはプロモーションを配信する | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Offer Decisioning](personalization/offer-decisioning.md) | 一元的な決定ロジックを使用して、チャネルをまたいでプロファイルに最適なオファーやコンテンツを選択します | [!DNL Journey Optimizer] （決定）、[!DNL Real-Time CDP] |
| [&#x200B; 行動に関する推奨事項 &#x200B;](personalization/behavioral-recommendation.md) | 選択戦略とランキングモデルを使用して、項目およびコンテンツのレコメンデーションを生成します。 | [!DNL Journey Optimizer] （決定）、[!DNL Real-Time CDP] |

## キャンペーンの管理とオーケストレーション

次のパターンでは、複数のチャネルをまたいで、スケジュール済み、トリガー済みおよび複数手順のメッセージ配信がカバーされています。

| パターン | プライマリ機能 | コアソリューション |
| --- | --- | --- |
| [&#x200B; バッチ送信メッセージの有効化 &#x200B;](campaign-management-orchestration/batch-outbound-message-activation.md) | オーディエンスを評価し、1 回のバッチ実行でスケジュールされたアウトバウンドメッセージを配信する | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [&#x200B; イベントトリガーメッセージ &#x200B;](campaign-management-orchestration/event-triggered-messaging.md) | リアルタイムの行動またはシステムイベントをリッスンし、トリガープロファイルにコンテキストメッセージを配信します。 | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [&#x200B; 複数ステップの調整されたジャーニー](campaign-management-orchestration/multi-step-orchestrated-journey.md) | 待機、条件、複数のメッセージアクションを含む、ブランチ型のマルチタッチジャーニーを通じてプロファイルをガイドします | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Decisioning を使用したクロスチャネルジャーニー](campaign-management-orchestration/cross-channel-journey-with-decisioning.md) | リアルタイムの意思決定を組み込んだマルチステップジャーニーを調整して、最適なチャネル、コンテンツまたはオファーを選択します | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [&#x200B; 購買グループベース・マーケティング&amp;ジャーニーマネジメント &#x200B;](campaign-management-orchestration/buying-group-based-marketing.md) | リードを購入グループに選定するアカウントレベルのジャーニーを開発し、B2B マーケティングの有効性を向上させます。 | B2B edition[!DNL Real-Time CDP]B2B edition[!DNL Journey Optimizer] |

## 分析

以下のパターンは、クロスチャネルの行動とパフォーマンスの分析をサポートします。

| パターン | プライマリ機能 | コアソリューション |
| --- | --- | --- |
| [Customer Analytics &amp; Insightのジェネレーション &#x200B;](analysis/customer-analytics-insight-generation.md) | 行動およびパフォーマンス分析のためのクロスチャネル分析ワークスペース、計算指標、ダッシュボードを作成 | [!DNL Customer Journey Analytics], [!DNL Experience Platform] |
| [B2B Analytics](analysis/b2b-analytics.md) | クロスチャネルカスタマージャーニー分析に B2B アカウントレベルの情報を含める | B2B edition[!DNL Real-Time CDP]B2B edition[!DNL Customer Journey Analytics] |

## 会話経験

以下のパターンにより、デジタルプロパティに対する AI を活用した、ブランドセーフの会話インタラクションが可能になります。

| パターン | プライマリ機能 | コアソリューション |
| --- | --- | --- |
| [Brand Conciergeの会話体験 &#x200B;](conversational-experience/brand-concierge-conversational-experience.md) | デジタルプロパティを AI を活用した、ブランドに安全な対話型エクスペリエンスに変換し、顧客発見の指針を示します | [!DNL Brand Concierge], [!DNL Experience Platform], [!DNL Real-Time CDP] |
