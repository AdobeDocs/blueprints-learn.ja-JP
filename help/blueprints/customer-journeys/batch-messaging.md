---
title: バッチメッセージおよび Adobe Experience Platform ブループリント
description: Adobe Experience Platform を顧客プロファイルおよびセグメント化の中央ハブとして使用して、スケジュールされたキャンペーンおよびバッチメッセージキャンペーンを実行します。
solution: Experience Platform, Campaign
kt: 7196
exl-id: 4e55218c-c158-4f78-9f0b-c03528d992fa
source-git-commit: f323d2deee5547abd0ccc8247a23ac7a144b2f07
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 100%

---

# バッチメッセージおよび Adobe Experience Platform ブループリント

Adobe Experience Platform を顧客プロファイルおよびセグメント化の中央ハブとして使用して、スケジュールされたキャンペーンおよびバッチメッセージキャンペーンを実行します。

## ユースケース

* スケジュールされた電子メールキャンペーン
* オンボーディングおよびリマーケティングキャンペーン

## アプリケーション

* Adobe Experience Platform
* Adobe Campaign Classic または Standard

## 統合パターン

* Adobe Experience Platform → Adobe Campaign Classic
* Adobe Experience Platform → Adobe Campaign Standard

## アーキテクチャ

<img src="assets/aepbatch.svg" alt="バッチメッセージおよび Adobe Experience Platform ブループリントの参照アーキテクチャ" style="width:80%; border:1px solid #4a4a4a" />

## ガードレール

* Adobe Campaign の単一の組織単位デプロイメントのみをサポートします
* Adobe Campaign は、すべてのアクティブなプロファイルに関する信頼できるソースです。つまり、プロファイルは Adobe Campaign に存在する必要があるため、Experience Platform セグメントに基づいた新しいプロファイルを作成しないでください。
* Experience Platform からのセグメントメンバーシップ適合は、バッチ（1 日 1 回）およびストリーミング（5 分以内）の両方に対して待ち時間があります

Adobe Campaign に共有する&#x200B;**[!UICONTROL リアルタイム顧客データプラットフォーム]セグメント：**

* 20 セグメントに制限することをお勧めします
* アクティベーションは、24 時間ごとに制限されます
* アクティベーションには、結合スキーマ属性のみを使用できます（配列／マップ／エクスペリエンスイベントはサポートされません）。
* セグメントあたり 20 個以下の属性にすることをお勧めします
* 「適合された」セグメントメンバーシップを含むすべてのプロファイルのセグメントごとに 1 ファイル、またはセグメントメンバーシップがファイルの属性として追加されている場合は、「適合」および「既存」の両方のプロファイルのセグメントごとに 1 ファイル
* 増分またはフルセグメント書き出しがサポートされます
* ファイルの暗号化はサポートされません
* Adobe Campaign エクスポートワークフローは最大で 4 時間ごとに実行します
* [Experience Platform のプロファイルおよびデータ取り込みのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)を参照してください

## 実装手順

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)
1. broadLog、trackingLog、配信不能アドレスおよびプロファイル環境設定用に Adobe Campaign スキーマを作成します（オプション）。
1. Experience Platform で取り込む[データセットを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)
1. ガバナンス用のデータセットに、Experience Platform で[データ使用ラベルを追加します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ja)
1. 宛先のガバナンスを実施する[ポリシーを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ja)

#### プロファイル／ID

1. [任意の顧客専用の名前空間を作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)
1. [スキーマに ID を追加します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. [!UICONTROL リアルタイム顧客プロファイル]の様々な表示用に[結合ポリシーを設定](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)します（オプション）。
1. Adobe Campaign 使用状況用のセグメントを作成します。

#### ソース／宛先

1. ストリーミング API およびソースコネクタを使用して、[Experience Platform にデータを取り込みます。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)
1. Adobe Campaign で使用する [!DNL Azure] Blob ストレージ宛先を設定します。

#### モバイルアプリデプロイメント

1. Adobe Campaign Classic 用の Adobe Campaign SDK または Adobe Campaign Standard 用の Experience Platform SDK を実装します。Experience Platform Launch がある場合は、Adobe Campaign Classic または Adobe Campaign Standard 拡張と Experience Platform SDK を使用することをお勧めします。

#### Adobe Campaign

1. プロファイル、ルックアップデータおよび関連する配信パーソナライズ機能データ用にスキーマを設定します。

>[!IMPORTANT]
>
>この時点で、Experience Platform 内にあるプロファイルおよびイベントデータ用のデータモデルを把握し、Adobe Campaign で必要になるデータを知っておくことが重要です。

#### インポートワークフロー

1. シンプル化されたプロファイルデータを Adobe Campaign sFTP に読み込んで取り込みます。
1. オーケストレーションおよびメッセージングパーソナライズ機能データを Adobe Campaign sFTP に読み込んで取り込みます。
1. ワークフローを使用して [!DNL Azure] Blob から Experience Platform セグメントを取り込みます。

#### エクスポートワークフロー

1. ワークフローを使用して、4 時間ごとに Experience Platform に Adobe Campaign ログを返します（broadLog、trackingLog、配信不能アドレス）。
1. コンサルティングが作成したワークフローを使用して、4 時間ごとに Experience Platform にプロファイル環境設定を返します（オプション）。


## 関連ドキュメント

* [Adobe Experience Platform ドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Campaign Classic ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja)
* [Campaign Standard ドキュメント](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ja)
* [Experience Platform Launch ドキュメント](https://experienceleague.adobe.com/docs/launch.html?lang=ja)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
