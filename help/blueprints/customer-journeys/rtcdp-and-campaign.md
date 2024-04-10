---
title: とのReal-Time CDP [!DNL Campaign] v7 とCampaign Standardの統合パターン
description: Adobe Experience Platformとそのリアルタイム顧客プロファイルおよび一元化されたセグメント化ツールをAdobeとともに利用する方法を紹介します [!DNL Campaign] パーソナライズされた会話を提供する。
solution: Real-Time Customer Data Platform, [!DNL Campaign]
exl-id: a15e8304-2763-42fc-9978-11f2482ea8b8
source-git-commit: 258aea64f6ff2f620b1adaa0c9ba4b02b47acce9
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 42%

---

# [!DNL Real-Time Customer Data Platform] （を使用） [!DNL Campaign] 統合パターン

Adobeの方法を示します [!DNL Experience Platform] また、そのリアルタイム顧客プロファイルと一元化されたセグメント化ツールをAdobeと共に利用できます [!DNL Campaign] パーソナライズされた会話を提供する。

## アプリケーション

* アドビ [!DNL Experience Platform Real-Time Customer Data Platform]
* Adobe [!DNL Campaign] v7 または [!DNL Campaign Standard]

## アーキテクチャ

<img src="assets/rtcdp-campaign-architecture.svg" alt="バッチメッセージおよび Adobe Experience Platform 統合パターンの参照アーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## 前提条件

* Experience Platformと [!DNL Campaign] 同じ IMS 組織でプロビジョニングし、ユーザーアクセスにAdobe Admin Consoleを使用することをお勧めします。 また、マーケティング UI 内からソリューション切り替えボタンを使用しても、
これにより、顧客がマーケティング UI 内からソリューションスイッチャーを利用することも可能になります

## ガードレール

次の節では、この統合のガードレールについて説明します。

### アドビ [!DNL Campaign]

* Adobeのみをサポート [!DNL Campaign] 単一組織単位の展開
* Adobe [!DNL Campaign] は、すべてのアクティブなプロファイルの情報源です。つまり、プロファイルがAdobeに存在する必要があります [!DNL Campaign] および新しいプロファイルは、Experience Platformセグメントに基づいて作成しないでください。
* [!DNL Campaign] 最大 4 時間ごとに実行するワークフローの書き出し
* Adobe用の XDM スキーマおよびデータセット [!DNL Campaign] broadLog、trackingLog および配信不能アドレスは標準提供ではなく、設計および構築する必要があります

### Real-time Customer Data Platform セグメントの共有

* RTCDP を参照してください [!DNL Campaign] 宛先コネクタ - [RTCDP キャンペーン接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html?lang=ja)

* 参照： [のデフォルトガードレール [!DNL Real-Time Customer Profile Data] とセグメント化](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)

## 実装手順

次の節では、各アプリケーションの実装手順について説明します。

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ja)。
1. Adobeを作成 [!DNL Campaign] broadLog、trackingLog、配信不能アドレスおよびプロファイル環境設定のスキーマ （オプション）。
1. Experience Platform で取り込む[データセットを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)
1. ガバナンス用のデータセットに、Experience Platform で[データ使用ラベルを追加します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ja)
1. 宛先のガバナンスを実施する[ポリシーを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ja)

#### プロファイル／ID

1. [任意の顧客専用の名前空間を作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)
1. [スキーマに ID を追加します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. [!UICONTROL リアルタイム顧客プロファイル]の様々な表示用に[結合ポリシーを設定](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)します（オプション）。
1. Adobe用のセグメントの作成 [!DNL Campaign] 使用方法。

#### ソース／宛先

1. [Experience Platformと [!DNL Campaign] 標準のソースと宛先](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html?lang=ja)
1. [Experience Platformと [!DNL Campaign] v7 ソースと宛先](https://experienceleague.adobe.com/docs/campaign-classic/using/integrating-with-adobe-experience-cloud/aep-sources-destinations/get-started-sources-destinations.html?lang=ja)
1. ストリーミング API およびソースコネクタを使用して、[Experience Platform にデータを取り込みます。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)
1. 設定 [!DNL Azure] Adobeで使用する BLOB ストレージの宛先 [!DNL Campaign].

#### アドビ [!DNL Campaign]

1. プロファイル、ルックアップデータおよび関連する配信パーソナライズ機能データ用にスキーマを設定します。

>[!IMPORTANT]
>
>Adobeに必要なデータを把握するには、プロファイルデータとイベントデータのExperience Platform内にあるデータモデルを、この時点で理解することが重要です [!DNL Campaign].

#### インポートワークフロー

1. 簡略化されたプロファイルデータの読み込みとAdobeへの取り込み [!DNL Campaign] sFTP です。
1. オーケストレーションおよびメッセージングのパーソナライゼーションデータの読み込みとAdobeへの取り込み [!DNL Campaign] sFTP です。
1. ワークフローを使用して [!DNL Azure] Blob から Experience Platform セグメントを取り込みます。

#### エクスポートワークフロー

1. Adobeを送信 [!DNL Campaign] 4 時間ごとにワークフローを通じてログをExperience Platformに戻します（broadLog、trackingLog、配信不能アドレス）。
1. コンサルティングが作成したワークフローを使用して、4 時間ごとに Experience Platform にプロファイル環境設定を返します（オプション）。

### モバイルプッシュ設定

* プッシュ通知用にモバイルデバイスとの統合に関してサポートされる 2 つの方法を示します。
   * Experience Platform Mobile SDK
   * [!DNL Campaign] Mobile SDK
* Experience Platform Mobile SDK ルート：
   * Adobeタグと [!DNL Campaign Classic] Experience Platformモバイル SDK との統合を設定するための拡張機能
   * アドビタグとデータ収集に関する実務知識が必要です
   * SDK のデプロイ、FCM（Android）および APNS（iOS）との統合によるプッシュトークンの取得、プッシュ通知を受け取るためのアプリの設定、プッシュインタラクションの処理など、Android および iOS でのプッシュ通知に関するモバイル開発経験が必要です。
* [!DNL Campaign] Mobile SDK
   * を参照してください。 [Campaign ClassicSDK ドキュメント](https://developer.adobe.com/client-sdks/solution/adobe-campaign-classic/)

>[!IMPORTANT]
>
>をデプロイする場合 [!DNL Campaign] SDK とは、他のExperience Cloudアプリケーションで動作しており、データ収集にはExperience Platform Mobile SDK を使用する必要があります。 これにより、デバイス上でクライアント側の呼び出しが重複します。

## 関連ドキュメント

* [Adobe [!DNL Experience Platform] 詳細を見る](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [[!DNL Campaign Classic] 詳細を見る](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja)
* [[!DNL Campaign Standard] 詳細を見る](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ja)
* [[!DNL Experience Platform] Launch ドキュメント](https://experienceleague.adobe.com/docs/launch.html?lang=ja)
* [[!DNL Experience Platform] Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
