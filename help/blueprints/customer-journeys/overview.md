---
title: 顧客ジャーニーのブループリント
description: スクリーンをまたいで、ジャストインタイムで調整された個別のカスタマーエクスペリエンスを提供します。
solution: Journey Optimizer, Campaign, Experience Platform
exl-id: 273d024f-a220-4336-89f2-e3bffafcdc37
source-git-commit: 8ee7fe8d38343a669f5ad57e69367fbe6a3e1024
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 13%

---

# 顧客ジャーニーブループリント

最新のマーケティングチームには、個々の顧客行動への対応という事後的なエンゲージメントと、積極的なアウトリーチの両方をサポートし、オーディエンスをコンバージョンファネルに導くキャンペーンを開始できるプラットフォームが必要です。 これらのユースケースは、メール、SMS、プッシュなど、様々なチャネルや、web およびアプリ内エクスペリエンスにわたっています。

Adobe Journey OptimizerとAdobe Campaign v8 はどちらも、カスタマーエンゲージメントのために、次の 2 つの基本モデルをサポートしています。

- 顧客トリガージャーニー：個々の行動とシグナルに基づいて、イベント駆動型のリアルタイムのオーケストレーションを行います。
- ブランド主導のキャンペーン：セグメント化やビジネスロジックに基づいてオーディエンスをエンゲージメントファネルに導入する、戦略的なタイムドプッシュ。

どちらのソリューションも、従来のチャネルとデジタルチャネルの間でのアウトバウンド通信を可能にします。 AJOは、オーディエンス状態の共有および意思決定サービスを通じて、インバウンドチャネル（web やモバイルアプリなど）との統合もサポートしており、統合されたクロスチャネルパーソナライゼーションが可能になります。

これらのツールの選択は、待ち時間の許容値、チャネル要件、データ統合戦略、スケーラビリティなどのアーキテクチャに関する考慮事項によって異なります。

<br>

| ブループリント | 説明 | アーキテクチャ |
|---|---|:---:|
| **[Adobe Journey Optimizer](journey-optimizer/journey-optimizer-overview.md)** | イベントドリブン型の 1:1 プロファイルオーケストレーションと、メール、SMS、web、プッシュ、アプリ内メッセージ、デスクトップなど、複数のチャネルをまたいだオーディエンスベースのブランドコミュニケーションを組み合わせます。 | <img src="journey-optimizer/images/ajo-architecture.svg" alt="Journey Optimizer ブループリントの参照アーキテクチャ" style="width:75%; border:1px solid #4a4a4a" class="modal-image" /> |
| **[Adobe [!DNL Campaign] v8](campaign-v8/campaign-v8-overview.md)** | バッチベースのマルチチャネルキャンペーン管理に重点を置いており、メール、SMS、ダイレクトメールなどの従来のマーケティングチャネルに最適です。 | <img src="campaign-v8/images/campaign-v8-architecture.svg" alt="Campaign v8 ブループリントの参照アーキテクチャ" style="width:75%; border:1px solid #4a4a4a" class="modal-image" /> |

<br>

## 非推奨のブループリント

| ブループリント | アーキテクチャ |
|---|:---:|
| **[Adobe [!DNL Campaign] v7](campaign-v7/campaign-v7-overview.md)** | <img src="campaign-v7/images/campaign-v7-architecture.svg" alt="Campaign v7 ブループリントの参照アーキテクチャ" style="width:50%; border:1px solid #4a4a4a" class="modal-image" /> |