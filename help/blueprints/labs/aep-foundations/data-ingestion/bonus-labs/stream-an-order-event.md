---
title: 注文イベントのストリーム
description: HTTP API ストリーミングデータフローを作成して、サンプル注文イベントを送信し、既存の顧客プロファイルにリンクします。
doc-type: article
solution: Experience Platform
exl-id: 558c21d1-f9b7-489b-9153-5f10d0b8448a
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 注文イベントのストリーム

## 前提条件

1. [ サンプルファイル ](../sample-files.md)をダウンロードし、—> **Lab\_Single\_Order\_sample.json**&#x200B;という名前のファイルを確認しました
1. データ ランディング ゾーンを使用する[ ラボが正常に完了し、読み込む有効なマッピング セットが設定されました](./using-data-landing-zone/overview.md)

## 課題

前のラボと同様に、次の一連のタスクを実行します。

1. HTTP API ソースコネクタを使用した新しいアカウントの作成
1. 新しいアカウントを使用してデータフローを設定し、独自の顧客注文データセットにデータをストリーミングします
1. データ ランディング ゾーンの使用[ ラボのマッピング セットを再利用します](./using-data-landing-zone/overview.md)
1. Postmanで、**Create Order Event**&#x200B;に必要な情報を入力して、データを正常にストリーミングし、以前に作成した顧客アカウントレコードに添付します
1. 注文がプロファイルにリンクされていることを確認します

>[!TIP]
>
>幸運を祈り、Adobe Experience Platformの神々があなたと一緒にいますように！
