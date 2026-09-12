---
title: API モデリング
description: クラス、フィールドグループ、ID、関係、参照記述子を含む、Experience Platform APIを通じてXDM スキーマを完全に構築する方法について説明します。
doc-type: overview-page
solution: Experience Platform
exl-id: f0ae0459-719c-4602-8dfa-e5819658f0b0
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# API モデリング

## ラボの概要

Experience Platform APIを使用することは、プラットフォームのさまざまな機能を自動化および運用する方法を理解するために非常に重要です。 スキーマを定義し、それらのスキーマによってデータがどのように記述されているかを理解することは、お客様がデータアーキテクチャを定義する際にAdobe Experience Platformで最初に行うことのひとつです。

このラボでは、APIのみを使用したAdobe Experience Platform スキーマ設計エクスペリエンスについて説明します。 既存のXDM コンポーネントを使用して独自のスキーマを作成する方法、XDMに独自のカスタマイズを追加する方法、リアルタイム顧客プロファイルで使用する様々なID記述子を識別して作成する方法について説明します。

## 学習目標

次のような様々なXDM基本コンポーネントを通じて、Experience Platform APIのみを使用してスキーマを構築できます。

1. クラス
1. フィールドグループ
1. 記述子
   1. ID （プライマリを含む）
   2. 関係
   3. 参照
