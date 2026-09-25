---
title: Journey Optimizer - サードパーティーメッセージ
description: Adobe Journey Optimizerをサードパーティのメッセージングシステムと組み合わせて使用し、パーソナライズされたコミュニケーションを送信する方法を示します。
solution: Journey Optimizer
exl-id: 3a14fc06-6d9c-4cd8-bc5c-f38e253d53ce
TQID: https://experienceleague.adobe.com/dlCwgPnHuoU0IGois2Yy3e9wPELIQsLkStzTBVl5M1M
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
    internal-label: Journey Optimizer
feature_v2:
  - id: a653cc2e-bc85-4353-a306-399e5b247978
    internal-label: Journey Optimizer campaigns
  - id: d556b755-390a-43f0-be32-a08cf6236126
    internal-label: Configuration
  - id: d998adac-2f81-400b-a669-d07bb196e4eb
    internal-label: Journeys
subfeature_v2:
  - id: af7571a6-3ddb-4c1c-abdf-4d4dde592140
    internal-label: Source connectors
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
    internal-label: Governance
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
    internal-label: Customer profiles
source-git-commit: 79738031788419872e32b8f754febacbfd18cc06
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 15%
---
# サードパーティーメッセージ

>[!TIP]
>このアーキテクチャは、「キャンペーン管理とオーケストレーション」の下に[&#x200B; ユースケースパターン &#x200B;](/help/blueprints/use-case-patterns/campaign-management-orchestration/third-party-messaging.md)として文書化されています。

Adobe Journey Optimizerをサードパーティのメッセージングシステムと組み合わせて使用し、パーソナライズされたコミュニケーションを送信する方法を示します。

<br>

## アーキテクチャ

![参照アーキテクチャ Journey Optimizer](images/ajo-third-party-messaging.png){width="1000" zoomable="yes"}

<br>

トポロジには、[!DNL Journey Optimizer]がサードパーティにトランザクションペイロードを送信していることが表示されます
カスタムアクションまたはREST API統合によるメッセージングアプリケーション。 [&#x200B; サードパーティのメッセージのユースケース パターンを使用](/help/blueprints/use-case-patterns/campaign-management-orchestration/third-party-messaging.md)
前提条件、ガードレール、導入ガイダンスに関する情報を提供します。

<br>

## 関連ドキュメント

* [Experience Platform ドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Experience Platform Tags ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [Experience Platform Mobile SDKのドキュメント](https://experienceleague.adobe.com/docs/mobile.html)
* [Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)
* [Journey Optimizerの製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
