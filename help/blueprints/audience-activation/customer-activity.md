---
title: お客様のアクティビティハブのブループリント
description: '[!UICONTROL リアルタイムのお客様] プロファイル・アップ：エージェント支援のサポートと販売に関するコンテキストを提供します。'
solution: Experience Platform,Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c,4f15aa5d-9ee3-4d92-8012-3e2f0c0d615f
translation-type: tm+mt
source-git-commit: f217273f29e1091a121a60c2a19d71190df0f0ff
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# お客様のアクティビティハブのブループリント

お客様のアクティビティハブのBlueprintは、外部アプリケーションがAdobe Experience Platformの[!UICONTROL リアルタイム顧客プロファイル]にアクセスする方法を示しています。

外部アプリケーションは、APIGETリクエストを使用してプロファイルにアクセスできます。 属性、イベント、セグメントのメンバーシップ、およびプロファイルに保存されたモデル駆動機能は、これらの外部の非Adobeアプリケーションで使用できます。

この機能を使用すると、顧客がコールセンターに電話したときに、豊富なコンテキストを表示できます。 サポート・エージェントは、例えば、顧客のライフタイム・バリュー、傾向の変化、マーケティング・キャンペーンへの暴露などを視覚的に把握できます。 セールス・エージェントは、顧客に対するより多くの状況や洞察を得ることもできます。

>[!NOTE]
>
>プロファイルルックアップAPIでサポートされる現在の待ち時間は約500ミリ秒なので、このアプローチは、プロファイルと同じページのWebやモバイルパーソナライゼーションなどのリアルタイムの意思決定エンジンとの統合には適していません。

## 使用例

* サポートや販売体験など、エージェントがサポートするインタラクションに対して、より深い消費者コンテキストを提供します。 Experience Platformに対するプロファイル参照を使用すると、エージェントは、最近の購入、キャンペーンインタラクション、傾向、オーディエンスのメンバーシップ、およびリアルタイム顧客プロファイルに保存された他の属性やインサイトなど、消費者に関するより多くのコンテキストを受け取ることができます。

## 建築

<img src="assets/cah.svg" alt="お客様のアクティビティハブのBlueprintのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

* [リアルタイム [!UICONTROL 顧客プロファイル] データのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)

## 導入手順

1. データセットとスキーマを設定します。
1. [!UICONTROL リアルタイム顧客プロファイル]を設定：[!UICONTROL リアルタイム顧客プロファイル]のスキーマとデータセットを設定し、結合ポリシーとIDを設定します。
1. データをプラットフォームに取り込み、[!UICONTROL リアルタイム顧客プロファイル]に処理します。
1. Entity APIを使用して、レコードエンティティまたはエクスペリエンスイベントエンティティからプロファイル属性を検索します。

## 関連ドキュメント

* [Adobe Experience Platformアクティベーション製品の説明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html)
* [[!UICONTROL リアルタイムのお客様] プロファイルに関するドキュメント](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en)
* [プロファイルガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
* [プロファイル参照API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
