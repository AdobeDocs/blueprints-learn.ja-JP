---
hold: true
title: Postman インストール
description: Postmanをインストールし、コレクション、環境、ワークスペースインターフェイスに慣れてから、後のラボでAPI呼び出しを行います。
doc-type: article
solution: Experience Platform
exl-id: c277edb5-f758-4955-bcd7-b15a9b9ab949
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Postman インストール

## 目標

このラボの最後には、Postmanをインストールし、基本的なワークスペースと環境を設定して、今後のラボで必要なAPI呼び出しを行えるようにします。

> [!IMPORTANT]
>
>このコースでは、さまざまなラボにPostmanが必要です。  既にPostmanをインストールしている場合でも、環境ファイルとAPI コレクションがインストールされ、適切に設定されていることを確認するには、このラボを完了する必要があります。



## Postmanのインストール

Postman web サイトに移動し、Postman アプリをダウンロードするか、Web バージョンを利用します – > [https://www.postman.com/download/](https://www.postman.com/download/)

![Postman web サイトのPostman ダウンロードページ ](assets/postman-installation-postman-download.png)

## Postman ワークスペースの作成（オプション）

Postman *を初めて利用する*&#x200B;場合、これが初めてのインストールであれば、新しいワークスペースを作成する必要はありません。 最初の起動時に、ログインせずに続行することを選択し、ワークスペースを必要としない軽量クライアントを使用します。

*すでにPostman*&#x200B;を使い慣れており、インストールしている場合は、既にサインインしていて、複数のワークスペースを持っている可能性があります。 そのような場合は、*このbootcamp*&#x200B;のワークスペースを新しく作成することをお勧めします。 手順については、[Postman Web サイトを参照してください。](https://learning.postman.com/docs/collaborating-in-postman/using-workspaces/create-workspaces/)

## Postmanインターフェイス

Postmanを開き、アプリケーションのいくつかの領域をすばやく確認します。 Experience Platformを利用する上で本当に必要なのは、アプリケーションのいくつかの重要な領域に集中することだけです。

![ サイドバー、ヘッダー、メイン作業領域のラベルが付いたPostman インターフェイスの概要](assets/postman-installation-interface-overview.png "Postman インターフェイス ")

## サイドバー

サイドバーを利用すれば、さまざまなPostman要素をすばやく移動できます。 ラボでは、以下の2つの項目のみを使用します。

**コレクション** – 保存されたリクエストのグループ。外部の場所から読み込むことも、自分で作成することもできます。

**Environments** - Postman リクエストで参照できる一連の変数。 Experience Platformでは、Postman環境はIMS組織内のAdobe サンドボックスと同義と考えることができます。PostmanのEnvironmentの関数を使用して



## ヘッダー

ワークスペース：作業をさまざまなグループ（プロジェクト、チームなど）に整理できます



## 主な作業空間

主なワークエリアは、Postmanで作業する際に作業の大部分を行う場所です。 すべてのAPI リクエストは、メインワークエリア内の特定のタブに公開されます。

**右側のサイドバー** – 選択した現在のタブに基づいて、ツールへの追加アクセスを提供します。 例としては、リクエスト、コメント、コードスニペットなどの機能に関するドキュメントが記載されています。

**環境セレクター** - APIを操作する際に、事前設定済みの変数にアクセスするために、異なる環境をすばやく切り替えることができます。 Experience Platformを使用する場合は、割り当てられたIMS組織内の特定のAEP サンドボックスを使用する場合に、これを活用します。



## フッター

Postman アプリケーションの最下部には、作成した呼び出しのログをすばやく確認できる一連の関数、検索と置換のクイックアクセス、その他のさまざまな関数があります。



## まとめ

これで、Postmanがインストールされ、UIの基本的な機能を理解できるようになりました
