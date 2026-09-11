---
title: 開発者コンソールの設定
description: DEP CLIのOAuth サーバー間の資格情報を使用してAdobe Developer Console プロジェクトを作成し、サンドボックスに対して認証します。
doc-type: article
solution: Experience Platform
exl-id: 4a7c9e2b-1d3f-4a6e-8b9c-2d5e7f1a3c6b
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# 開発者コンソールの設定

>[!NOTE]
>
>これは、ラボを自分のペースで進めている場合にのみ必要です。 ライブトレーニングコースやイベントを受講している場合は、サンドボックスが既に展開されています。

DEP CLIは、Adobe Developer Console プロジェクトのOAuth サーバー間の資格情報を使用してサンドボックスに認証します。 このページでは、プロジェクトの作成を順を追って説明します。 これを一度おこなうだけで、AEP FoundationsとAJO Architectural Foundationsの両方のトラックで同じ資格情報が機能します。両方のAPIを追加する必要があります。

>[!NOTE]
>
>Adobe Experience Platformの資格情報（および必要に応じてAdobe Journey Optimizer）を含むDeveloper Console プロジェクトが既にある場合は、このセクションをスキップして、[ デプロイメント手順](deployment-instructions.md)に進みます。

## 前提条件

- Adobe IDからの企業への開発者アクセス
- 空でタイプ `dev`のAdobe Experience Platform サンドボックス
- サンドボックスに対するすべての権限が付与されたAdobe Experience Platform ロール（不明な場合はシステム管理者にお問い合わせください）

## プロジェクトの作成

1. [Adobe Developer Console](https://developer.adobe.com/console)に移動してログインします
1. 複数の組織にアクセスできる場合は、右上の組織スイッチャーを使用して正しい組織を選択します
1. **新しいプロジェクトの作成**&#x200B;を選択
1. プロジェクトを後で認識できる名前に変更します（例：`DEP Sandbox`）。

## Experience Platform APIの追加

1. プロジェクトの概要から、**APIを追加**&#x200B;を選択します
1. **Adobe Experience Platform**&#x200B;製品アイコンを選択し、**Adobe Experience Platform API**&#x200B;を選択します
1. **次へ**&#x200B;を選択
1. 認証タイプとして&#x200B;**OAuth サーバー間**&#x200B;を選択し、**次**&#x200B;を選択します
1. 資格情報に名前を付けて、**次へ**&#x200B;を選択します
1. 使用するサンドボックスに一致する製品プロファイルを選択し、**設定したAPIを保存**&#x200B;を選択します

## 値の収集

資格情報の&#x200B;**OAuth サーバー間**&#x200B;概要ページを開きます。 CLIの環境ファイルには4つの値が必要です。

| **開発コンソールの値** | **Env ファイル フィールド** |
| --------------------- | ------------------------------- |
| クライアント ID | `API_KEY` |
| クライアント秘密鍵 | `CLIENT_SECRET` |
| 組織ID | `IMS_ORG` （`@AdobeOrg`で終わる） |
| 範囲 | `SCOPES` |

>[!NOTE]
>
>資格情報ページに表示されるデフォルトの範囲をコピーします。手動で追加する必要はありません。 上記の両方のAPIを追加した場合、スコープリストには両方が自動的に含まれます。

このページを開いたままにするか、これらの4つの値を安全な場所にコピーしてください。 トラックのセットアップガイドの次の手順で、CLIの環境ファイルに貼り付けます。
