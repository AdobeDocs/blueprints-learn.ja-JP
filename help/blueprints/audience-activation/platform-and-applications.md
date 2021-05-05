---
title: Experience CloudアプリケーションとのオーディエンスとプロファイルのアクティベーションBlueprint
description: Experience Platform内のプロファイルとオーディエンスを管理し、Experience Cloudアプリと共有します。
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services
kt: 7722
exl-id: null
translation-type: tm+mt
source-git-commit: c1a281f0808a0f081b2b63927a8bddb6377bbbad
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 33%

---

# Experience CloudアプリケーションとのオーディエンスとプロファイルのアクティベーションBlueprint

Experience Platform内のプロファイルとオーディエンスを管理し、Experience Cloudアプリと共有します。 豊富な顧客セグメントやインサイトをExperience Platformで作成して共有し、Experience Cloudアプリで共有します。

Experience Cloudアプリケーションとのアクティベーションは、[オンライン/オフラインAudience ActivationのBlueprint](online-offline.md)と密接に連携しています。 Experience PlatformとExperience Cloudのアプリケーション間の統合に関する詳細は、このブループリントに記載されています。

## ユースケース

* Experience Cloudによる顧客インタラクションチャネル全体にわたるパーソナライズとターゲット設定。
* Experience Cloudアプリケーション間およびExperience Platform間でのオーディエンスおよびプロファイルデータの共有。

## アプリケーション

* Adobe Experience Platform
* [!UICONTROL リアルタイム顧客データプラットフォーム]
* Experience Platformアクティベーション
* Experience Cloud アプリケーション
   * Audience Manager
   * ターゲット
   * Campaign
   * Journey Optimizer

## 構造

### Experience Cloudアプリケーションとのオーディエンスとプロファイルのアクティベーション

<img src="assets/activation+apps.svg" alt="Experience Cloudアプリケーションを使用したオーディエンスおよびプロファイルアクティベーションのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

Experience PlatformとExperience Cloudアプリケーションとの統合に関する追加のアーキテクチャ図については、[Adobe Experience Platform&amp;アプリケーション図](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html)を参照してください。

## ガードレール

オーディエンスとプロファイルのアクティベーションの概要ページ](overview.md)の[ガードレールを参照してください。

## 関連ドキュメント

* [リアルタイム顧客データプラットフォーム製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)
* [プロファイルと分類のガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [セグメント化ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)
* [宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ja)

## 関連ビデオおよびチュートリアル

* [リアルタイム顧客データプラットフォームの概要](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ja)
* [[!UICONTROL リアルタイム顧客データプラットフォームのデモ]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ja)
* [セグメントの作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ja)
