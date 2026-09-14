---
title: API コレクション
description: AEP Foundations ラボ全体で使用されるリクエストを含むbootcampのPostman API コレクションをダウンロードして読み込みます。
doc-type: article
solution: Experience Platform
exl-id: 18d820c5-56ad-46b8-a9cf-f725555d2db3
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%
---

# API コレクション

## Postman API コレクションファイル

ファイルをダウンロード — [AEP Foundations Bootcamp （Labs）.postman_collection.json](assets/aep-foundations-bootcamp-labs.postman_collection.json)



## API コレクションのインポート

1. ファイルをクリックして、ブラウザーの上から`Postman API Collection File`を開きます
1. ファイルのURLをクリップボードにコピーします
1. ローカルマシンでPostmanを起動し、ワークスペース内の「`Import`」ボタンをクリックします
1. インポート モーダル テキスト ボックスに`Postman API Collection File`のURLを貼り付けます。 これにより、自動インポートがトリガーされます

![Postman ワークスペースの「読み込み」ボタンをクリックしてAPI コレクションを読み込む](assets/api-collection-click-import-button.png "読み込みボタン ")



![API コレクションファイルのURLをPostmanの読み込みモーダルテキストボックスにペースト &#x200B;](assets/api-collection-import-modal-paste-url.png " ボタンモーダルテキストボックスの読み込み")

左側のサイドバーの`Collections` タブの下に`AEP Foundations Bootcamp`というコレクションが表示されました



![AEP Foundations Bootcamp コレクションが「Postman コレクション」サイドバーのタブに入力されました](assets/api-collection-imported-collection-in-sidebar.png)

## AEP Foundations Bootcamp コレクションの概要

読み込んだAPI コレクションには、ブートキャンプ全体でラボに必要なすべてのAPI呼び出しが含まれています。  各ラボは、独自のAPI セットを持つ特定のフォルダーに編成されます。  今週ラボを完了する際には、このフォルダー構造に注意してください。

各フォルダーの詳細は次のとおりです。

- **IMS Authenticate** - Adobe Experience Platform APIを使用する際に必要なアクセス\_tokenを生成する1回のリクエストが含まれています
- **XDM スキーマ Lab** - リアルタイム顧客プロファイルのスキーマの構築と設定に必要なXDM コンポーネントを作成するための一連の要求が含まれています
- **Data Ingestion Lab** - Experience Platformにデータをストリーミングするための一連のリクエストが含まれます
- **Profile Lab** - リアルタイム顧客プロファイルの特性と行動を表示するための一連のリクエストが含まれます

>[!SUCCESS]
>
>おめでとうございます。  bootcampのPostman コレクションが正常に読み込まれました
