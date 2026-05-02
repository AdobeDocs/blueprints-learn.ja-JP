---
title: '[!DNL Journey Optimizer] - トリガーされたメッセージとAdobe Experience Platform ブループリント'
description: ストリーミングデータ、顧客プロファイル、セグメント化の中央ハブとして Adobe Experience Platform を使用して、トリガーされるメッセージとエクスペリエンスを実行します。
solution: Journey Optimizer
exl-id: 70573eb9-cd69-4fe6-b2ae-dae81665a308
TQID: https://experienceleague.adobe.com/MuodOvJ52G9lmUAmsuj06q1aTXkRg7W0Bj6nxLp96N8
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
feature_v2:
  - id: a653cc2e-bc85-4353-a306-399e5b247978
  - id: d998adac-2f81-400b-a669-d07bb196e4eb
  - id: fe338112-e2ce-4876-8989-fc4d497613f1
  - id: fe96aceb-8194-4a8a-a6b0-75302d02804d
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 357
ht-degree: 12%

---

# [!DNL Journey Optimizer] - ジャーニーのブループリント

>[!TIP]
>このブループリントは、[&#x200B; ユースケースパターン &#x200B;](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md)として、「キャンペーン管理とオーケストレーション」でも利用できます。

ジャーニーは、顧客一人ひとりの行動にもとづいて、パーソナライズされたマルチステップのエクスペリエンスを提供する、リアルタイムのイベント駆動型ワークフローです。 メール、SMS、プッシュ通知、アプリ内メッセージ、コードベースの体験、カスタム API ベースの統合など、幅広いチャネルをサポートしており、顧客が好みの顧客接点でコンテキストに沿って顧客とエンゲージすることができます。

<br>

## アーキテクチャ

<img src="images/ajo-journeys-architecture.svg" alt="リファレンスアーキテクチャ：ジャーニーの設計図" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## ジャーニーのアーキテクチャに関する考慮事項

- **プロファイルの鮮度**: AJO ジャーニーは、顧客プロファイルのリアルタイム更新に依存しています。 プロファイルの精度を維持するために、Adobe Experience Platform（AEP）にフィードするデータソースが、低遅延の取り込み用に設定されていることを確認します。
- **スケーラブルなイベント処理：** インフラストラクチャが大量のジャーニートリガーとメッセージ配信を処理できることを確認します。
- **モジュール統合：** AJOを外部システムと接続し、動的なパーソナライゼーションを実現するためのAPIとカスタムアクションを設計します。
- **ID解決**: デバイスとチャネルをまたいで顧客IDを正確につなぎ合わせることが重要です。 IDが一致していないと、ジャーニーの方向性が壊れたり、誤ったりする可能性があります。
- **セグメントの選定タイミング**: オーディエンスベースのジャーニーは、セグメントメンバーシップに依存します。 セグメントが評価される頻度と、そのタイミングがジャーニーの入力とパーソナライゼーションにどのように影響するかを把握します。
- **ジャーニーの入力条件**: プロファイルは、ジャーニーに入るには、特定の条件を満たす必要があります。 これらの条件は、意図しない除外事項や重複を避けるように注意深く設計する必要があります。
- **オーディエンスの評価と待ち時間**: オーディエンスの読み取り手順は、Adobe Experience Platform内のセグメント評価によって異なりますが、リアルタイムでは行われない場合があります。 評価頻度と待ち時間を把握してジャーニーを構築し、オーディエンスの選定の遅延を回避して、タイムリーなパーソナライゼーションを実現できます。

<br>

## ガードレール

[[!DNL Journey Optimizer] ガードレール製品リンク](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails.html)

[ガードレールとエンドツーエンドのレイテンシーガイダンス](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=ja)

<br>

## 関連ドキュメント

- [[!DNL Experience Platform]件のドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
- [[!DNL Experience Platform] タグのドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
- [[!DNL Experience Platform Mobile SDK]件のドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
- [[!DNL Journey Optimizer]件のドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
- [[!DNL Journey Optimizer]製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
