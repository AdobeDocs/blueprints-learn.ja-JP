---
title: '[!DNL Journey Optimizer] - ジャーニーブループリント'
description: ストリーミングデータ、顧客プロファイル、セグメント化の中央ハブとして Adobe Experience Platform を使用して、トリガーされるメッセージとエクスペリエンスを実行します。
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: e96b48e55c0fe2f48dc83f48ad41f5b686ec8dc1
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 15%

---

# [!DNL Journey Optimizer] ブループリント

Adobe [!DNL Journey Optimizer] は、Adobe Experience Platform上に構築されたクラウドネイティブなアプリケーションであり、複数のチャネルをまたいで、カスタマージャーニーをリアルタイムかつスケジュールに沿って編成できます。 メール、SMS、プッシュ、web およびアプリ内メッセージを通じてパーソナライズされたエクスペリエンスを提供するために、イベント駆動型のトリガー、オーディエンスのセグメント化および意思決定のサービスをサポートします。 インバウンドシステムとアウトバウンドシステムを統合し、カスタマーライフサイクル全体で統一されたオーディエンス状態管理とコンテキストエンゲージメントを可能にします。

このブループリントでは、アプリケーションの技術的機能の概要を説明し、ア [!DNL Journey Optimizer] ットを構成する様々なアーキテクチャコンポーネントについて詳しく説明します。

<br>

## ユースケース

>[!BEGINTABS]
>[!TAB ジャーニー（イベント駆動型、リアルタイム） ]

- **放棄の復元：** メール、プッシュまたはアプリ内で、ユーザーが買い物かご、フォーム、またはセッションを放棄した際に、パーソナライズされたメッセージをトリガーにします。
- **新規ユーザーのサインアップ：** 新規ユーザーは、新しいアカウント設定、関連するプロモーションまたは特典に登録後、すぐにエンゲージできます
- **トランザクションメッセージ：** イベントトリガーを使用して、リアルタイムに確認、アラートまたは更新（注文の発送、パスワードのリセットなど）を送信します。
- **コンテキストのターゲット設定：** ユーザーのシグナルと場所に基づいて、その時点のユーザーとコミュニケーションを取り、エクスペリエンスのガイドと指示を行います
- **コンテキストアップセル/クロスセル：** リアルタイムのプロファイル属性と最近のインタラクションに基づいてパーソナライズされたオファーを配信します。

>[!TAB  キャンペーンオーケストレーション （スケジュール済み、ブランド開始） ]

- **プロモーションキャンペーン**：製品ローンチ、季節的なオファーまたはセールスイベント用の複数手順のマルチチャネルキャンペーンを開始します。
- **ライフサイクルマーケティング**：誕生日メッセージ、更新リマインダー、ロイヤルティマイルストーンなど、繰り返しキャンペーンを自動化します。
- **オーディエンスベースのFunnel プッシュ**：ビジネスロジックまたは CRM 属性に基づいて、オーディエンスをセグメント化し、構造化されたキャンペーンにプッシュします。
- **ニュースレターおよびコンテンツ配信**: メールやモバイルを問わず、ターゲットオーディエンスに対してパーソナライズされたコンテンツをスケジュールして配信します。
- **再エンゲージメントキャンペーン**：休眠状態のユーザーを特定し、無操作状態のしきい値に基づいてエンゲージメントフローに再導入します。

>[!ENDTABS]

<br>

## アーキテクチャ

<img src="images/ajo-architecture.svg" alt="リファレンスアーキテクチャのAdobe Journey Optimizerブループリント" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## ブループリントのシナリオ

| シナリオ | 説明 |
| :-- | :-- |
| [ジャーニー](journey-optimizer-journeys.md) | Adobe Journey OptimizerのAJOジャーニーは、リアルタイムイベントまたはオーディエンスセグメントによってトリガーされるパーソナライズされた自動カスタマーエクスペリエンスであり、マーケターは、メール、SMS、プッシュ通知などのチャネルをまたいで、関連性の高いメッセージを配信できます。 |
| [&#x200B; キャンペーンオーケストレーション &#x200B;](journey-optimizer-campaigns.md) | AJO キャンペーンオーケストレーションを使用すると、マーケターは、リアルタイムデータとオーディエンスインサイトを使用して、パーソナライズされたクロスチャネルキャンペーンを設計および実行できます。 動的ターゲティング、メッセージ配信、ジャーニーロジックをサポートし、メール、SMS、プッシュおよびカスタムチャネルをまたいで顧客エンゲージメントを最適化します。 | |

<br>

## 統合パターン

| 統合 | 説明 | 技術上の考慮事項 |
| :-- | :-- | :-- |
| [サードパーティメッセージング](3rd-party-messaging.md) | Adobe [!DNL Journey Optimizer] をサードパーティのメッセージングプラットフォームと統合して、パーソナライズされたカスタマーコミュニケーションを編成し、提供する方法を示します。 | <ul><li>サードパーティシステムは、**ベアラートークン認証** をサポートしている必要があります。</li><li>**マルチテナントアーキテクチャが原因で、静的 IP はサポートされていません**。</li><li>サードパーティシステムでは **API レート制限** に注意してください。お客様は、**Adobe Journey Optimizer** から発生するトラフィックを処理するために、追加容量を購入する必要が生じる場合があります。</li><li>**意思決定管理** は、メッセージペイロードまたは配信ロジック内ではサポートされていません。</li></ul> |
| [[!DNL Journey Optimizer] Adobe Campaign v8 を使用する場合 &#x200B;](../campaign-v8/ajo-and-campaign-v8.md) | Adobe [!DNL Journey Optimizer] をAdobe Campaign v8 のトランザクションメッセージ機能と統合して最終的なメッセージ配信を実行する方法を示します。 | <ul><li>メッセージのスロットルはありません。 上限は 5 分あたり 4,000 メッセージ。</li><li>イベントで開始されたジャーニーのみをサポート</li><li>Campaign から送信されるメッセージでは、意思決定管理はサポートされていません</li></ul> |

<br>

## 前提条件

Adobe[!DNL Experience Platform]:

- [!DNL Journey Optimizer] データソースを設定する前に、システムでスキーマとデータセットを設定する必要があります
- XDM Experience Event クラスベースのスキーマで、ルールベースのイベントではないイベントをトリガーする場合は、「Orchestration eventID フィールドグループ」を追加します
- XDM 個人プロファイルクラスベースのスキーマの場合は、「プロファイルテストの詳細」フィールドグループを追加して、[!DNL Journey Optimizer] で使用するテストプロファイルを読み込むことができます

<br>

メール：

- メッセージ送信に使用するサブドメインの準備が整っている必要があります
- サブドメインは、アドビに完全にデリゲートすることも（推奨）、CNAME を使用してアドビ固有の DNS サーバー（カスタム）を指すこともできます
- Google TXT レコードは、配信品質を高めるために各サブドメインに必要

<br>

モバイルプッシュ：

- 顧客は、モバイルデベロッパーを使用してアプリを作成できる必要があります
- Adobe Experience Platform Mobile SDK

<br>

## ガードレール

[[!DNL Journey Optimizer]  ガードレール製品リンク &#x200B;](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails.html)

[&#x200B; ガードレールとエンドツーエンドの待ち時間のガイダンス &#x200B;](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=ja)

## 関連ドキュメント

- [[!DNL Experience Platform]  ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
- [[!DNL Experience Platform]  タグのドキュメント &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
- [[!DNL Experience Platform Mobile SDK]  ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
- [[!DNL Journey Optimizer]  ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
- [[!DNL Journey Optimizer]  製品の説明 &#x200B;](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)