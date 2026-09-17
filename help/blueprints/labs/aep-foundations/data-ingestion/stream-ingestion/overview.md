---
title: ストリーム取得
description: ストリーミングソースを介して、顧客アカウントデータをデータレイクおよびプロファイルに読み込むには、ストリーミングインレットとREST APIを使用します。
doc-type: overview-page
solution: Experience Platform
exl-id: 973a9cac-dc9d-4c5f-87c3-16a55efd1314
source-git-commit: 8b3391d41cd4a3ea6cb52d5167e627b7f6bd2c6e
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%
---

# ストリーム取得

## 学習目標

この演習では、ストリーミングソースからAdobe Experience Platform Data LakeおよびProfileに顧客アカウントデータを読み込みます。 このラボを受講した後、何を持って帰るべきですか？

- ストリーミングインレットの作成
- 別のデータフローからのマッピングセットのインポート
- UIからのデータフローIDとデータセット IDの取得
- REST APIを使用したイベントの取得

>[!IMPORTANT]
>
>このラボを開始する前に、[Postmanの設定](../../setup.md)を完了してください。

>[!NOTE]
>
>以前のラボで顧客アカウントスキーマの作成を完了しなかった場合は、スキーマカタログを参照し、代わりに&#x200B;**dep：顧客アカウント**&#x200B;を使用できます
