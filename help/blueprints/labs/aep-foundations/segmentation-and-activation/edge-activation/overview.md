---
hold: true
title: Edgeのアクティベーション
description: Edge、ストリーミング、バッチアクティベーションの速度がどのように異なるかを説明し、エッジセグメントの作成とイベント転送の設定に関するラボステップをプレビューします。
doc-type: overview-page
solution: Experience Platform
exl-id: 9ecadff9-3838-4cd4-93b1-7c23a232f84c
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Edgeのアクティベーション

## アクティベーション速度の概要

Adobeには、さまざまなニーズに対応するためのアクティベーション速度が3つあります。

1. Edge
1. ストリーミング
1. バッチ

イベント転送機能、Edge Audiences、Edge PersonalizationでAdobe Edgeを使用してアクティベートする方法について説明します。 次に、HubからEdgeと外部の宛先の両方にストリーミング宛先を使用する方法を示します。

>[!NOTE]
>
>このラボでは、バッチアクティベーションについては説明しません。 バッチアクティベーションは異なる間隔でスケジュールすることができ、タイミングは少なくとも3～24時間を持たずにラボ環境で紹介することを困難にします。



## ラボでカバーする内容

- Edge セグメントを作成
- イベント転送の設定
- Edge イベントでの送信
- このトリガー
  - Edgeセグメントの選定
  - Edgeでのイベント転送によるWebhookへの送信
