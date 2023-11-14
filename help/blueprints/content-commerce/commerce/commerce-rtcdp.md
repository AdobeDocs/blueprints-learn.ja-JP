---
title: Adobe Commerce - RTCDP ブループリント
description: Adobe Experience PlatformとAdobe Commerceの統合により、お客様の単一のビューを作成し、デジタルストアフロントおよび複数のチャネルでのエクスペリエンスをインテリジェントにパーソナライズできます。
solution: Real-Time Customer Data Platform, Commerce
source-git-commit: abb946358ceeee1af427c5b362ed2f48f733a6c9
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Adobe Commerceと RTCDP

この統合エクスペリエンスにより、Adobe Commerceのお客様はAdobe Experience Platformとシームレスに統合して、顧客プロファイルを強化し、デジタルストアフロントやその他のチャネルでエクスペリエンスをパーソナライズできます。

## テクニカル機能が有効

* 収集され、任意のAdobe Experience Cloud製品に送信されたストアフロントデータ（クライアント側）。 （買い物かごへの追加、買い物かごの放棄など）
* 任意のAdobe Experience Cloud製品に対するバックオフィスの注文ステータス
* バックオフィスの過去の注文をAdobe Experience Platformに送信できます
* RTCDP オーディエンスをAdobe Commerceに共有し、パーソナライズする

## 前提条件

Experience Platformコネクタを使用するには、次の条件を満たす必要があります。

* Adobe Commerce 2.4.4 以降
* Adobe IDと組織 ID
* Adobe Experience Platform/RTCDP
* [Adobeクライアントデータレイヤー (ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html?lang=en). ストアフロントイベントデータを収集するには、ACDL が必要です。

## オンボーディング手順

### Adobe CommerceからAdobe Experience Platformへのデータ収集

* [インストール](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/install.html?lang=en) Experience Platformコネクタ拡張
* [ログイン](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) をAdobeアカウントに追加し、表示で組織 ID を確認します。 組織 ID は、プロビジョニングされた組織の会社に関連付けられたExperience CloudID です。 この ID は 24 文字の英数字から成る文字列で、その後に@AdobeOrg（必須）が続きます。
* [作成または更新](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html?lang=en) コマース固有のフィールドグループを持つ XDM スキーマ。
* [データセットの作成](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=en#create-a-dataset) 作成または更新したスキーマに基づいて このデータセットには、送信したコマースデータが含まれます。
* [データストリームの作成](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html?lang=en) をクリックし、コマース固有のフィールドグループを含む XDM スキーマを選択します。
* [Commerce Services に接続](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html?lang=en).
* [Adobe Experience Platformに接続](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/connect-data.html?lang=en).

### オーディエンス共有用にAdobe Experience Platformからコマースの宛先に接続

Adobe Commerceの宛先に接続するには：

* Adobe Analytics の [Adobe Experience Platformインターフェイス](https://experience.adobe.com/platform/)で、宛先/カタログに移動します。
* 「パーソナライゼーション」を選択します。
* Adobe Commerceの宛先を選択してハイライトし、「セットアップ」を選択します。
* 次に示す手順に従います： [宛先設定のチュートリアル](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en).

## 標準搭載のデータ

* ストアフロント（ブラウザー/アプリ）イベント
* バックオフィスイベント
* 履歴注文データ

サポートされるイベントの完全なリストについては、 [コマースイベント](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/event-forwarding/events.html?lang=en)

## アーキテクチャ

<img src="../commerce/assets/commerce_rtcdp.png" alt="Adobe Commerce RTCDP のアーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## 関連する実装ガイド

| ガイド  | リンク |
|:----|:----|
| Platform コネクタ | [Adobe CommerceExperience Platformコネクタの概要](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/overview.html?lang=en) |
| コマースの宛先 | [RTCDP でのAdobe Commerce接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-commerce.html?lang=en) |
| Edge パーソナライゼーション | [エッジパーソナライゼーションの宛先に対するオーディエンスのアクティブ化](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations.html?lang=en) | |
