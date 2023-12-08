---
title: Adobe Commerce - RTCDP ブループリント
description: Adobe Experience PlatformとAdobe Commerceの統合により、お客様の単一のビューを作成し、デジタルストアフロントおよび複数のチャネルでのエクスペリエンスをインテリジェントにパーソナライズできます。
solution: Real-Time Customer Data Platform, Commerce
exl-id: e2fc5e1c-c865-4c24-9b82-861a34aba487
source-git-commit: 8a47b73065a5591673804301c61a73947346813c
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Adobe Commerceと RTCDP

The [!DNL Data Connection] 拡張機能を使用すると、Adobe Commerceのお客様はAdobe Experience Platformとシームレスに統合して、顧客プロファイルを強化し、デジタルストアフロントやその他のチャネルでエクスペリエンスをパーソナライズできます。

## テクニカル機能が有効

* 収集して任意のAdobe Experience Cloud製品に送信されたストアフロントデータ（買い物かごへの追加、買い物かごの放棄などのクライアント側）。
* 任意のAdobe Experience Cloud製品に対するバックオフィスの注文ステータス
* バックオフィスの過去の注文をAdobe Experience Platformに送信できます
* RTCDP オーディエンスをAdobe Commerceに共有し、パーソナライズする

## 前提条件

次の手順で [!DNL Data Connection] 拡張機能には、以下が必要です。

* Adobe Commerce 2.4.4 以降
* Adobe IDと組織 ID
* Adobe Experience Platform/RTCDP
* [Adobeクライアントデータレイヤー (ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html). ストアフロントイベントデータを収集するには、ACDL が必要です。

## オンボーディング手順

### Adobe CommerceからAdobe Experience Platformへのデータ収集

* [インストール](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) の [!DNL Data Connection] 拡張子。
* [ログイン](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) をAdobeアカウントに追加し、表示で組織 ID を確認します。 組織 ID は、プロビジョニングされた組織の会社に関連付けられたExperience CloudID です。 この ID は 24 文字の英数字から成る文字列で、その後に@AdobeOrg（必須）が続きます。
* [作成または更新](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html) コマース固有のフィールドグループを持つ XDM スキーマ。
* [データセットの作成](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) 作成または更新したスキーマに基づいて このデータセットには、送信したコマースデータが含まれます。
* [データストリームの作成](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html) をクリックし、コマース固有のフィールドグループを含む XDM スキーマを選択します。
* [Commerce Services に接続](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html).
* [Adobe Experience Platformに接続](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html).

### オーディエンス共有用にAdobe Experience Platformからコマースの宛先に接続

Adobe Commerceの宛先に接続するには：

* Adobe Analytics の [Adobe Experience Platformインターフェイス](https://experience.adobe.com/platform/)で、宛先/カタログに移動します。
* 「パーソナライゼーション」を選択します。
* Adobe Commerceの宛先を選択してハイライトし、「セットアップ」を選択します。
* 次に示す手順に従います： [宛先設定のチュートリアル](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html).

## 標準搭載のデータ

* ストアフロント（ブラウザー/アプリ）イベント
* バックオフィスイベント
* 履歴注文データ

サポートされるイベントの完全なリストについては、 [コマースイベント](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/event-forwarding/events.html)

## アーキテクチャ

<img src="../commerce/assets/commerce_rtcdp.png" alt="Adobe Commerce RTCDP のアーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## 関連する実装ガイド

| ガイド | リンク |
|:----|:----|
| Platform コネクタ | [Adobe CommerceExperience Platformコネクタの概要](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/overview.html) |
| コマースの宛先 | [RTCDP でのAdobe Commerce接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-commerce.html) |
| Edge パーソナライゼーション | [エッジパーソナライゼーションの宛先に対するオーディエンスのアクティブ化](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations.html) | |
