---
title: メッセージ配信の実際
description: 基本プランメンバーをターゲットとし、AEP プロファイルとリレーショナルスキーマメールチャネル間の配信動作を比較するオーケストレーションキャンペーンの構築の概要を説明します。
doc-type: overview-page
solution: Experience Platform
exl-id: 84b16fff-f733-439a-9a93-726811e543ce
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%
---

# メッセージ配信の実際

## 前提条件

>[!WARNING]
>
>以下のラボは、このラボを開始する前に完了している必要があります

- **Data Stores — リレーショナルストアの動作** **—>** [Profile Target Dimension](../../data-stores/relational-store-in-action/profile-target-dimension.md)
- **データストア —>** [電子メールチャネルの設定](../../data-stores/configure-email-channels/overview.md) *（この設定ステップは完了までに3時間以内に必要です）*

ラボを完了していない場合は、続行する前に今すぐ完了してください。

>[!CAUTION]
>
>このラボでは、サンドボックスでAdobeにデリゲートされたサブドメインが必要です。 自分のペースで進めている場合は、[ セットアップ ](../../setup.md)を参照してください。

## ラボの概要

このビデオでは、基本プランメンバーオーディエンスの構築とフォーク、プロファイルメールチャネルとリレーショナルメールチャネル間の配信結果の比較など、このラボ用にオーケストレーションされたキャンペーンを構築する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3486541/)

## 学習目標

- 複数のワークフローアクティビティを使用したオーケストレーションされたキャンペーンの構築
- オーディエンスを作成アクティビティを使用してオーディエンスを作成する
- オーディエンスをフォークして2つのブランチを作成し、前のラボで作成したメールチャネルを使用してメッセージを送信します
- キャンペーンをテストし、メールチャネル間の動作の違いを把握します

「基本」プランのメンバーをターゲットにするには、このラボでキャンペーンを作成し、オーケストレーションされた様々なキャンペーン設定がメールチャネル設定にどのような影響を与えるかを調べます。
