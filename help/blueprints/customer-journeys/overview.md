---
title: 顧客ジャーニーのブループリント
description: あらゆるスクリーンをまたいで、個別のジャストインタイムのオーケストレーションされた顧客体験を提供します。
solution: Journey Optimizer, Campaign, Experience Platform
exl-id: 273d024f-a220-4336-89f2-e3bffafcdc37
TQID: https://experienceleague.adobe.com/vJUJiLr7je-Pp2daoYoNYipfVBRyaEYNv-XCx9PrjzM
product_v2: id: cb954087-f4fc-4456-afb9-e939cabcdc79id: dfc56824-e8b9-499e-85d4-21aedb507314id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a075b2c1-7748-4328-b7f6-343aa314616aid: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914id: d998adac-2f81-400b-a669-d07bb196e4ebid: daec7ead-f475-492a-a3b3-02ae08565d6fid: df64005d-8f9a-422e-ba4d-c6f6dc3454b4id: fe338112-e2ce-4876-8989-fc4d497613f1
subfeature_v2: id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5520579-b31f-4df7-9281-f0d9f91e2edcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: df401a2a-327d-468c-a5e4-b7b7ccd071a0id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: a99add31cc9f485db119ca00426798545e6a7316
workflow-type: tm+mt
source-wordcount: 235
ht-degree: 13%

---

# 顧客ジャーニーのブループリント

今日のマーケティング部門には、オーディエンスをコンバージョンファネルに導くキャンペーンを開始する、受動的なエンゲージメント（個々の顧客行動への対応）と積極的なアウトリーチの両方をサポートできるプラットフォームが必要です。 これらのユースケースは、電子メール、SMS、プッシュ通知など、webやアプリ内の体験などのチャネルをまたいです。

Adobe Journey OptimizerとAdobe Campaign v8は、どちらも顧客エンゲージメント用の2つの基本モデルをサポートしています。

- 顧客をトリガーにしたジャーニー：個々の行動やシグナルにもとづいて、イベント主導のリアルタイムのオーケストレーションを実現できます
- ブランド主導のキャンペーン：セグメンテーションやビジネスロジックにもとづいて、オーディエンスをエンゲージメントファネルに導く、戦略的なタイミングで行うプッシュです。

どちらのソリューションも、従来のチャネルとデジタルチャネルの両方でアウトバウンドコミュニケーションを可能にします。 AJOでは、オーディエンスの状態共有および決定サービスを通じて、インバウンドチャネル（webやモバイルアプリなど）との統合をさらにサポートしており、統合されたクロスチャネルのパーソナライゼーションが可能です。

これらのツール間の選択は、待ち時間の許容範囲、チャネル要件、データ統合戦略、スケーラビリティなどのアーキテクチャ上の考慮事項によって異なります。

<br>

| ブループリント | 説明 | アーキテクチャ |
|---|---|:---:|
| **[Adobe Journey Optimizer](journey-optimizer/journey-optimizer-overview.md)** | イベント駆動型の1:1 プロファイルオーケストレーションと、電子メール、sms、web、プッシュ通知、アプリ内メッセージ、デスクトップ PCなど、複数のチャネルをまたいだオーディエンスベースのブランドコミュニケーションを組み合わせることができます。 | <img src="journey-optimizer/images/ajo-architecture.svg" alt="Journey Optimizer ブループリントの参照アーキテクチャ" style="width:75%; border:1px solid #4a4a4a" class="modal-image" /> |
| **[Adobe [!DNL Campaign] v8](campaign-v8/campaign-v8-overview.md)** | バッチベースのマルチチャネルキャンペーン管理に重点を置いており、電子メール、SMS、ダイレクトメールなどの従来のマーケティングチャネルに最適です。 | <img src="campaign-v8/images/campaign-v8-architecture.svg" alt="Campaign v8 ブループリントの参照アーキテクチャ" style="width:75%; border:1px solid #4a4a4a" class="modal-image" /> |

<br>

## 非推奨のブループリント

| ブループリント | アーキテクチャ |
|---|:---:|
| **[Adobe [!DNL Campaign] v7](campaign-v7/campaign-v7-overview.md)** | <img src="campaign-v7/images/campaign-v7-architecture.svg" alt="Campaign v7 ブループリントの参照アーキテクチャ" style="width:50%; border:1px solid #4a4a4a" class="modal-image" /> |