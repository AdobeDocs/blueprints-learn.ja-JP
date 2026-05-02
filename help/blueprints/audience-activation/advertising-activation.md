---
title: Audience ActivationからソーシャルおよびAdvertisingの宛先
description: 複数のソースから顧客データを取り込み、顧客の単一のプロファイルビューを構築する方法を説明します。
solution: Real-Time Customer Data Platform, Data Collection
kt: 7086
exl-id: b75a7a01-04ba-4617-960d-f73f7a9cc6c7
TQID: https://experienceleague.adobe.com/GNc9ZMx62nCAEYtB1TP3buZonF6GQKBfoYLNepSzDHM
product_v2: id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2: id: ba929a52-9339-4154-9487-317dc875a3c7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 174
ht-degree: 45%

---

# Audience ActivationからソーシャルおよびAdvertisingの宛先

>[!TIP]
>このブループリントは、「オーディエンスの構築とアクティベーション」の下の[ ユースケースパターン ](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md)としても利用できます。

複数のソースから顧客データを取り込み、顧客の単一のプロファイルビューを構築します。 これらのプロファイルをセグメント化して、マーケティングやパーソナライゼーション用のオーディエンスを作成したり、FacebookやGoogleなどの広告ネットワークとオーディエンスを共有して、これらのオーディエンスをターゲットにした施策やパーソナライズされた施策を展開したりできます。

## ユースケース

* ソーシャルおよび広告の宛先の既知のオーディエンスに対するオーディエンスターゲティング。
* オンラインおよびオフライン属性を使用したオンラインパーソナライズ機能。

## アプリケーション

* Real-time Customer Data Platform

## アーキテクチャ

<img src="./assets/social_activation.svg" alt="Facebook Custom Audience アクティベーションの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## ガードレール

[プロファイルとセグメント化のガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)

## 関連ドキュメント

Facebook Custom Audiences へのアクティベーション - [宛先の設定](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/social/facebook.html?lang=ja)

Google Customer Match へのアクティベーション - [宛先の設定](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-customer-match.html?lang=ja)