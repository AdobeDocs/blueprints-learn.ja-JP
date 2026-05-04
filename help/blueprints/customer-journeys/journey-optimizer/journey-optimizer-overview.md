---
title: '[!DNL Journey Optimizer] - ジャーニーのブループリント'
description: ストリーミングデータ、顧客プロファイル、セグメント化の中央ハブとして Adobe Experience Platform を使用して、トリガーされるメッセージとエクスペリエンスを実行します。
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
TQID: https://experienceleague.adobe.com/Rfi-0QD8bQpD-Zp2CDpzqxrge0yVs2CFt5mDKibNogI
product_v2: id: cb954087-f4fc-4456-afb9-e939cabcdc79
feature_v2: id: a653cc2e-bc85-4353-a306-399e5b247978id: d998adac-2f81-400b-a669-d07bb196e4ebid: df64005d-8f9a-422e-ba4d-c6f6dc3454b4id: fe338112-e2ce-4876-8989-fc4d497613f1
subfeature_v2: id: fa683eda-48de-4558-af32-2673edcd44fe
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: addf009e-030a-4310-8534-776a3e62ed48id: b5520579-b31f-4df7-9281-f0d9f91e2edcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d00e9f03-e50b-4162-b143-0c0817c937c2id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: fd2e3797-f2ea-4b36-a9af-52acf5e90513id: ff2b9b37-92e0-45fc-b853-379d44c08c89
source-git-commit: a99add31cc9f485db119ca00426798545e6a7316
workflow-type: tm+mt
source-wordcount: 718
ht-degree: 16%

---

# [!DNL Journey Optimizer]個のブループリント

Adobe [!DNL Journey Optimizer]は、Adobe Experience Platform上に構築されたクラウドネイティブなアプリケーションで、複数のチャネルにまたがるカスタマージャーニーのリアルタイムかつスケジュールされたオーケストレーションを可能にします。 イベント駆動型トリガー、オーディエンスセグメンテーション、意思決定サービスをサポートし、電子メール、SMS、プッシュ通知、web、アプリ内メッセージなどを通じてパーソナライズされたエクスペリエンスを提供できます。 インバウンドおよびアウトバウンドシステムと統合することで、顧客ライフサイクル全体でオーディエンスの状態管理と文脈的エンゲージメントを統合できます。

この設計図では、アプリケーションの技術的な機能の概要を説明し、[!DNL Journey Optimizer]を構成するさまざまなアーキテクチャ コンポーネントについて詳しく説明します。

<br>

## ユースケース

>[!BEGINTABS]
>[!TAB ジャーニー（イベント駆動型、リアルタイム） ]

- **放棄のトリガー:**&#x200B;利用者がカート、フォーム、またはセッションを放棄した際に、電子メール、プッシュ通知、またはアプリ内でパーソナライズされたメッセージを回復します。
- **新規ユーザー登録：**&#x200B;新規ユーザーが新規アカウントの環境設定、関連するプロモーションまたは特典に登録した直後にエンゲージします
- **トランザクションメッセージ：** イベントトリガーを使用して、リアルタイムの確認、アラート、または更新（注文品の発送、パスワードリセットなど）を送信します。
- **コンテキストのターゲット設定：** シグナルと場所に基づいて瞬時にユーザーとコミュニケーションを取り、ユーザーのエクスペリエンスを導き、指示します
- **コンテクスト型アップセル/クロスセル：** リアルタイムのプロファイル属性と最近のやり取りにもとづいて、パーソナライズされたオファーを提供します。

>[!TAB  キャンペーンオーケストレーション （スケジュール済み、ブランド主導） ]

- **プロモーションキャンペーン**：製品の発売、季節オファー、販売イベント用のマルチステップ、マルチチャネルキャンペーンを開始します。
- **ライフサイクルマーケティング**：誕生日メッセージ、更新リマインダー、ロイヤルティマイルストーンなどの定期的なキャンペーンを自動化します。
- **オーディエンスベースのFunnel プッシュ**：ビジネスロジックまたはCRM属性に基づいて、オーディエンスをセグメント化し、構造化キャンペーンにプッシュします。
- **ニュースレターとコンテンツ配信**：電子メールとモバイルをまたいで、ターゲットとするオーディエンスにパーソナライズされたコンテンツをスケジュールして配信します。
- **リエンゲージメント施策**：休眠ユーザーを特定し、非アクティブのしきい値に基づいてエンゲージメントフローに再導入します。

>[!ENDTABS]

<br>

## アーキテクチャ

<img src="images/ajo-architecture.svg" alt="リファレンスアーキテクチャ Adobe Journey Optimizer Blueprint" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## ブループリントのシナリオ

| シナリオ | 説明 |
| :-- | :-- |
| [ジャーニー](journey-optimizer-journeys.md) | Adobe Adobe Journey OptimizerのAJOジャーニーは、リアルタイムのイベントやオーディエンスセグメントをトリガーにして、自動的にパーソナライズされた顧客体験を提供できます。これにより、マーケターは、電子メール、SMS、プッシュ通知などのチャネルをまたいで、適切なメッセージを配信できます。 |
| [ キャンペーンオーケストレーション ](journey-optimizer-campaigns.md) | AJO Campaign Orchestrationを活用すると、マーケターはリアルタイムのデータとオーディエンスインサイトを活用して、パーソナライズされたクロスチャネルキャンペーンを設計して実行できます。 動的なターゲティング、メッセージ配信、ジャーニーロジックをサポートし、メール、SMS、プッシュ通知、カスタムチャネルをまたいで顧客エンゲージメントを最適化できます。 |

<br>

## 統合パターン

| 統合 | 説明 | 技術的な考慮事項 |
| :-- | :-- | :-- |
| [サードパーティメッセージング](3rd-party-messaging.md) | Adobe [!DNL Journey Optimizer]をサードパーティのメッセージングプラットフォームと統合して、パーソナライズされた顧客コミュニケーションを調整および配信する方法を示します。 | <ul><li>サードパーティシステムは&#x200B;**ベアラートークン認証**&#x200B;をサポートする必要があります</li><li>マルチテナントアーキテクチャのため、**静的IPはサポートされていません**。</li><li>サードパーティシステムの&#x200B;**API レート制限**&#x200B;に注意してください。お客様は、**Adobe Journey Optimizer**&#x200B;からのトラフィックを処理するために、追加のキャパシティを購入する必要がある場合があります。</li><li>**意思決定管理**&#x200B;は、メッセージペイロードまたは配信ロジックではサポートされていません。</li></ul> |
| [[!DNL Journey Optimizer] とAdobe Campaign v8](../campaign-v8/ajo-and-campaign-v8.md) | Adobe [!DNL Journey Optimizer]が、Adobe Campaign v8のトランザクションメッセージ機能と連携して、最終的なメッセージ配信を実行する方法を示します。 | <ul><li>メッセージのスロットリングはありません。 5分あたり4,000件のメッセージの上限。</li><li>イベント開始ジャーニーのみをサポート</li><li>意思決定管理は、Campaignで送信されるメッセージではサポートされていません</li></ul> |

<br>

## 前提条件

Adobe [!DNL Experience Platform]:

- [!DNL Journey Optimizer] データソースを設定する前に、システムでスキーマとデータセットを設定する必要があります
- XDM Experience Event クラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合は、「Orchestration eventID フィールドグループ」を追加します
- XDM Individual Profile クラスベースのスキーマの場合、「プロファイルテストの詳細」フィールドグループを追加して、[!DNL Journey Optimizer]で使用するテストプロファイルを読み込むことができます

<br>

電子メール：

- メッセージ送信に使用するサブドメインの準備が整っている必要があります
- サブドメインは、アドビに完全にデリゲートすることも（推奨）、CNAME を使用してアドビ固有の DNS サーバー（カスタム）を指すこともできます
- Google TXT レコードは、配信品質を高めるために各サブドメインに必要

<br>

モバイルプッシュ：

- 顧客は、モバイルデベロッパーを使用してアプリを作成できる必要があります
- Adobe Experience Platform Mobile SDK

<br>

## ガードレール

[[!DNL Journey Optimizer] ガードレール製品リンク](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails.html)

[ガードレールとエンドツーエンドのレイテンシーガイダンス](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## 関連ドキュメント

- [[!DNL Experience Platform]件のドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
- [[!DNL Experience Platform] タグのドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
- [[!DNL Experience Platform Mobile SDK]件のドキュメント](https://experienceleague.adobe.com/docs/mobile.html)
- [[!DNL Journey Optimizer]件のドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)
- [[!DNL Journey Optimizer]製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
