---
title: お客様のアクティビティハブのブループリント
description: リアルタイムのお客様プロファイルの検索により、エージェント支援のサポートと販売に関するコンテキストが提供されます。
solution: Experience Platform, Data Collection
kt: 7195
translation-type: tm+mt
source-git-commit: c4bd4bbd40f2ae6b9ab980c5274a6e2007d976d3
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# お客様のアクティビティハブのブループリント

お客様のアクティビティハブのBlueprintは、外部アプリケーションがAdobe Experience Platformの[!UICONTROL リアルタイム顧客プロファイル]にアクセスする方法を示しています。

外部アプリケーションは、APIGETリクエストを使用してR[!UICONTROL リアルタイム顧客プロファイル]にアクセスできます。 属性、イベント、セグメントのメンバーシップ、およびプロファイルに保存されたモデル駆動機能は、これらの外部の非Adobeアプリケーションで使用できます。

この機能を使用すると、顧客がコールセンターに電話したときに、豊富なコンテキストを表示できます。 サポート・エージェントは、例えば、顧客のライフタイム・バリュー、傾向の変化、マーケティング・キャンペーンへの暴露などを視覚的に把握できます。 セールス・エージェントは、顧客に対するより多くの状況や洞察を得ることもできます。

>[!NOTE]
>
>プロファイルルックアップAPIでサポートされる現在の待ち時間は約500ミリ秒なので、このアプローチは、プロファイルと同じページのWebやモバイルパーソナライゼーションなどのリアルタイムの意思決定エンジンとの統合には適していません。

## 使用例

* サポートや販売体験など、エージェントがサポートするインタラクションに対して、より深い消費者コンテキストを提供します。 Experience Platformに対するプロファイル参照を使用すると、エージェントは、最近の購入、キャンペーンインタラクション、傾向、オーディエンスのメンバーシップ、およびリアルタイム顧客プロファイルに保存された他の属性やインサイトなど、消費者に関するより多くのコンテキストを受け取ることができます。

## 建築

<img src="assets/cah.svg" alt="お客様のアクティビティハブのBlueprintのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

* [リアルタイム顧客プロファイルデータのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## 導入手順

1. データセットとスキーマを設定します。
1. [!UICONTROL リアルタイム顧客プロファイルの設定]:[!UICONTROL リアルタイム顧客プロファイル]のスキーマとデータセットを設定し、結合ポリシーとIDを設定します。
1. データをプラットフォームに取り込み、[!UICONTROL リアルタイム顧客プロファイル]に処理します。
1. Entity APIを使用して、レコードエンティティまたはエクスペリエンスイベントエンティティからプロファイル属性を検索します。

## 関連ドキュメント

* [Adobe Experience Platformアクティベーション製品の説明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html)
* [顧客プロファイルに関するリアルタイムドキュメント](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en)
* [プロファイルガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [プロファイル参照API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
