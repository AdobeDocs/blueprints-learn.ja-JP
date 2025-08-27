---
title: Real-Time CDPと  [!DNL Campaign] v7 およびCampaign Standardの統合パターン
description: Adobe Experience Platformとそのリアルタイム顧客プロファイルおよび一元化されたセグメンテーションツールをAdobeとともに利用して、パーソナライズされた会話を提供する方法  [!DNL Campaign]  紹介します。
solution: Real-Time Customer Data Platform, [!DNL Campaign]
exl-id: a15e8304-2763-42fc-9978-11f2482ea8b8
source-git-commit: 10d49e3b712fc9d4ecdf41defe6e62dde2a86b72
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 42%

---

# [!DNL Real-Time Customer Data Platform] 統合パターンを使用した [!DNL Campaign]

Adobe [!DNL Experience Platform] とそのリアルタイム顧客プロファイルおよび一元化されたセグメンテーションツールをAdobe [!DNL Campaign] と共に利用して、パーソナライズされた会話を提供する方法を紹介します。

## アプリケーション

* アドビ [!DNL Experience Platform Real-Time Customer Data Platform]
* Adobe [!DNL Campaign] v7 以 [!DNL Campaign Standard]

## アーキテクチャ

<img src="assets/rtcdp-campaign-architecture.svg" alt="バッチメッセージおよび Adobe Experience Platform 統合パターンの参照アーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## 前提条件

* Experience Platformと [!DNL Campaign] を同じ IMS 組織でプロビジョニングし、Adobe Admin Consoleを使用してユーザーアクセスを行うことをお勧めします。 また、マーケティング UI 内からソリューション切り替えボタンを使用しても、
これにより、顧客がマーケティング UI 内からソリューションスイッチャーを利用することも可能になります

## ガードレール

次の節では、この統合のガードレールについて説明します。

### アドビ [!DNL Campaign]

* Adobe [!DNL Campaign] の単一組織単位デプロイメントのみをサポートします
* Adobe [!DNL Campaign] は、すべてのアクティブなプロファイルの情報源です。つまり、プロファイルがAdobe [!DNL Campaign] に存在する必要があり、Experience Platform セグメントに基づいて新しいプロファイルを作成してはなりません。
* 最大 4 時間ごとに実行するエクスポートワークフローを [!DNL Campaign] 定します
* Adobe [!DNL Campaign] broadLog、trackingLog および配信不能アドレス用の XDM スキーマおよびデータセットは、初期設定ではなく、設計および構築される必要があります

### Real-Time Customer Data Platform セグメントの共有

* 詳しくは、RTCDP [!DNL Campaign] 宛先コネクタ - [RTCDP Campaign 接続 ](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html?lang=ja) を参照してください。

* [ およびセグメント化のデフォルトガードレール  [!DNL Real-Time Customer Profile Data]  を参照してください ](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)

## 実装手順

次の節では、各アプリケーションの実装手順について説明します。

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=ja)。
1. broadLog、trackingLog、配信不能のアドレスおよびプロファイル環境設定（オプション）用のAdobe [!DNL Campaign] スキーマを作成します。
1. Experience Platform で取り込む[データセットを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)
1. ガバナンス用のデータセットに、Experience Platform で[データ使用ラベルを追加します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ja)
1. 宛先のガバナンスを実施する[ポリシーを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ja)

#### プロファイル／ID

1. [任意の顧客専用の名前空間を作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)
1. [スキーマに ID を追加します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. [!UICONTROL リアルタイム顧客プロファイル]の様々な表示用に[結合ポリシーを設定](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)します（オプション）。
1. Adobe [!DNL Campaign] を使用するためのセグメントを作成します。

#### ソース／宛先

1. [Experience Platformおよび  [!DNL Campaign]  標準のソースと宛先 ](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html?lang=ja)
1. [Experience Platformおよび  [!DNL Campaign] v7 のソースと宛先 ](https://experienceleague.adobe.com/docs/campaign-classic/using/integrating-with-adobe-experience-cloud/aep-sources-destinations/get-started-sources-destinations.html?lang=ja)
1. ストリーミング API およびソースコネクタを使用して、[Experience Platform にデータを取り込みます。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=ja)
1. Adobe [!DNL Azure][!DNL Campaign] 使用する BLOB ストレージの宛先を設定します。

#### アドビ [!DNL Campaign]

1. プロファイル、ルックアップデータおよび関連する配信パーソナライズ機能データ用にスキーマを設定します。

>[!IMPORTANT]
>
>Adobe [!DNL Campaign] で必要になるデータを把握するには、プロファイルとイベントのデータに関するExperience Platform内のデータモデルを現時点で理解することが重要です。

#### インポートワークフロー

1. 簡略化されたプロファイルデータをAdobe [!DNL Campaign] sFTP に読み込んで取り込みます。
1. オーケストレーションおよびメッセージングのパーソナライゼーションデータをAdobe [!DNL Campaign] sFTP に読み込んで取り込みます。
1. ワークフローを使用して [!DNL Azure] Blob から Experience Platform セグメントを取り込みます。

#### エクスポートワークフロー

1. 4 時間ごとにワークフロー（broadLog、trackingLog、配信不能アドレス）を介して、Adobe [!DNL Campaign] ログをExperience Platformに送り返します。
1. コンサルティングが作成したワークフローを使用して、4 時間ごとに Experience Platform にプロファイル環境設定を返します（オプション）。

### モバイルプッシュ設定

* プッシュ通知用にモバイルデバイスとの統合に関してサポートされる 2 つの方法を示します。
   * Experience Platform Mobile SDK
   * [!DNL Campaign] Mobile SDK
* Experience Platform Mobile SDK ルート：
   * Adobe タグと [!DNL Campaign Classic] 拡張機能を活用して、Experience Platform Mobile SDKとの統合を設定します
   * アドビタグとデータ収集に関する実務知識が必要です
   * SDK のデプロイ、FCM（Android）および APNS（iOS）との統合によるプッシュトークンの取得、プッシュ通知を受け取るためのアプリの設定、プッシュインタラクションの処理など、Android および iOS でのプッシュ通知に関するモバイル開発経験が必要です。
* [!DNL Campaign] Mobile SDK
   * [Campaign Classic SDK ドキュメントを参照してください ](https://developer.adobe.com/client-sdks/solution/adobe-campaign-classic/)

>[!IMPORTANT]
>
>[!DNL Campaign] SDKをデプロイし、他のExperience Cloud アプリケーションを使用している場合、データ収集にはExperience Platform Mobile SDKを使用する必要があります。 これにより、デバイス上でクライアント側の呼び出しが重複します。

## 関連ドキュメント

* [Adobe [!DNL Experience Platform]  ドキュメント ](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [[!DNL Campaign Classic]  ドキュメント ](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja)
* [[!DNL Campaign Standard]  ドキュメント ](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ja)
* [[!DNL Experience Platform] Launch ドキュメント ](https://experienceleague.adobe.com/docs/launch.html?lang=ja)
* [[!DNL Experience Platform] Mobile SDKのドキュメント ](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
