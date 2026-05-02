---
title: '[!DNL Journey Optimizer] - キャンペーンオーケストレーション'
description: マーケターは、アウトバウンドメッセージチャネルをまたいで、スケジュールされたオーディエンスベースのマルチステップのマーケティングコミュニケーションを調整できます。
solution: Journey Optimizer
exl-id: a8ff16f8-146d-4e1f-9bd0-9eda6af0c69b
TQID: https://experienceleague.adobe.com/aPDagEC1zZdi-Bz29fFf6g5Uy8v4qMPhDA47Cdwl-Sw
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
feature_v2:
  - id: a653cc2e-bc85-4353-a306-399e5b247978
  - id: d998adac-2f81-400b-a669-d07bb196e4eb
  - id: df64005d-8f9a-422e-ba4d-c6f6dc3454b4
  - id: fe338112-e2ce-4876-8989-fc4d497613f1
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 358
ht-degree: 6%

---

# [!DNL Journey Optimizer] - Campaign Orchestration ブループリント

>[!TIP]
>このブループリントは、[&#x200B; ユースケースパターン &#x200B;](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md)として、「キャンペーン管理とオーケストレーション」でも利用できます。

AJO Campaign Orchestrationを使用すると、マーケターは、電子メール、SMS、プッシュ通知、ダイレクトメールなどのアウトバウンドチャネルをまたいで、スケジュールされたオーディエンスベースのマルチステップのコミュニケーションを設計して実行できます。 リアルタイムの顧客プロファイルから得られるリアルタイムのデータを利用して、個々の顧客行動に対応するジャーニーとは異なり、施策は、オーディエンスを計画的にターゲティングし、各オーディエンスに合わせて調整されたマーケティング施策です。 キャンペーンとジャーニーを組み合わせることで、補完的なアプローチを実現できます。キャンペーンはブランドエンゲージメント戦略を推進し、ジャーニーはパーソナライズされたレスポンシブなエクスペリエンスを提供します。

<br>

## アーキテクチャ

<img src="images/ajo-campaigns-architecture.svg" alt="リファレンスアーキテクチャ Adobe Journey Optimizer Campaign Orchestration Blueprint" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

### メッセージ実行アーキテクチャ

<img src="images/ajo-campaigns-message-sending-architecture.png" alt="リファレンスアーキテクチャ Adobe Journey Optimizer Campaign Orchestration Blueprint" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

### リレーショナルストア – データ取り込み遅延

<img src="images/ajo-campaigns-data-ingestion-architecture.png" alt="リファレンスアーキテクチャ Adobe Journey Optimizer Campaign Orchestration Blueprint" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## ジャーニーのアーキテクチャに関する考慮事項

- **データアーキテクチャ**: AJO Campaign Orchestrationでは、オーディエンスの構築とオーケストレーションのために、その下にリレーショナルデータベースを利用しています
- **オーディエンスポータル統合**: リアルタイム顧客プロファイル内のオーディエンスポータルとネイティブに統合され、既存のオーディエンスから読み取り、キャンペーンの構築時に新しいオーディエンスをに保存します
- **オンデマンドオーディエンス作成**：緊急のマーケティングユースケースに対応するオーディエンスを即座に作成、評価、実行します
- **リアルタイム顧客プロファイルの統合：**&#x200B;同意とコミュニケーション履歴の信頼できる情報源。パーソナライゼーションの「スキニープロファイル」設計をサポート
- **マルチエンティティメッセージ送信：**&#x200B;機能により、1つの配信でプロファイルごとに複数のメッセージを送信できます（例：予約ごとに1つのメッセージをお客様のメールアドレスに送信）
- **複数エンティティのセグメント化**：リレーショナルストア内の任意のエンティティ（製品、在庫、計画など）からオーディエンスの構築を開始します。

<br>

## ガードレール

[Orchestrated Campaigns製品リンク](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/guardrails)

[ガードレールとエンドツーエンドのレイテンシーガイダンス](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails)

<br>

## 関連ドキュメント

- [[!DNL Journey Optimizer]件のオーケストレーションされたキャンペーン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/orchestrated-campaigns-landing-page.html)
- [[!DNL Experience Platform]件のドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
- [[!DNL Experience Platform] タグのドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
- [[!DNL Experience Platform Mobile SDK]件のドキュメント](https://experienceleague.adobe.com/docs/mobile.html)
- [[!DNL Journey Optimizer]件のドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)
- [[!DNL Journey Optimizer]製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
