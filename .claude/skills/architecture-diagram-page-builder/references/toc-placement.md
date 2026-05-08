---
source-git-commit: 83e85d946e455cde46001af0a2112637b7fe24cc
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---
# TOC.md プレースメント リファレンス

スキルが新しいアーキテクチャ図ページを生成する場合、そのページがサイトナビゲーションで見つけられるように、エントリを`/help/blueprints/TOC.md`に追加する必要があります。 このドキュメントでは、そのエントリの場所と方法を正確に定義します。

## 親セクション

すべてのアーキテクチャ図ページは、TOC.mdのトップレベル `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` セクションの下にあります。 このセクションでは、いくつかのサブセクションでページをトピック別にグループ化します。

## サブスクルーマッピング

新しいページのトピックフォルダーに一致するサブセクションを選択します。

| トピックフォルダー | 目次サブセクション見出し |
| --- | --- |
| `experience-platform/` | `+ Architecture overviews{#architecture-overview}` |
| `experience-platform/deployment/` | `+ Deployment{#deployment}` （`Architecture overviews`内にネストされたサブサブセクション） |
| `audience-activation/` | `+ Audience & Profile Activation{#audience-activation}` |
| `b2b/` | `+ B2B activation & marketing{#b2b-activation}` |
| `customer-journey-analytics/` | `+ Customer Journey Analytics{#customer-journey-analytics}` |
| `customer-journeys/` | `+ Customer journeys{#customer-journeys}` |

ユーザーがこのテーブルにないトピックフォルダーを提案した場合は、それを新しいトップレベルのサブセクションとして扱い、一時停止して、作成するかどうかを確認するようにユーザーに依頼します。 新しいサブセクションを静かに発明しないでください。

## エントリ形式

```
    + [{Page title}](/help/blueprints/{topic-folder}/{filename}.md)
```

ルール：

- **インデント：**&#x200B;正確に4つのスペース、次に`+ `。 目次パーサーはこれによって異なります。タブや間隔が異なると、ナビゲーションが壊れます。
- **テキストをリンク：** ページのタイトル、`title`の正面部分と正確に一致します。 `[!DNL ...]`は、同じサブセクション内の既存の兄弟が使用している場合にのみ使用します。ローカルの規則と一致します。
- **リンクターゲット：**&#x200B;絶対パスが`/help/blueprints/`で始まります。 常に`.md`拡張子を含めます。
- **位置：**&#x200B;は、ユーザーが別の位置を指定しない限り、一致するサブセクションの最後のエントリとして追加されます。 すべての兄弟エントリの既存の順序を保持します。

## ネストされたサブセクション

`+ Architecture overviews{#architecture-overview}`には、SDK ページ用のネストされた`+ Deployment{#deployment}` ブロックが含まれています。 新しいページが`experience-platform/deployment/`未満の場合は、インデントの&#x200B;**6**&#x200B;個のスペースを含む`Deployment`内にエントリを配置します。

```
      + [{Page title}](/help/blueprints/experience-platform/deployment/{filename}.md)
```

その他のサブセクション （`Audience & Profile Activation`、`B2B activation & marketing`など） ネストされたグループ化を含めることもできます。エントリを配置する前に、セクションを調べます。 ネストされたグループが存在し、新しいページがその中に属する場合は、さらに2つのスペースをインデントします。それ以外の場合は、サブセクションの最上位レベルにエントリを配置します。

## 使用例

### 例1 — トップレベルのAEP ページ

- トピックフォルダー：`experience-platform/`
- ファイル名：`mix-modeler-integration.md`
- ページタイトル：`Adobe Mix Modeler integration with Experience Platform`

エントリ：

```
    + [Adobe Mix Modeler integration with Experience Platform](/help/blueprints/experience-platform/mix-modeler-integration.md)
```

`+ Architecture overviews{#architecture-overview}`の下に配置しました。

### 例2 - AJOジャーニーアーキテクチャ

- トピックフォルダー：`customer-journeys/`
- ファイル名：`cross-channel-journey-architecture.md`
- ページタイトル：`Cross-channel journey architecture`

エントリ：

```
    + [Cross-channel journey architecture](/help/blueprints/customer-journeys/cross-channel-journey-architecture.md)
```

`+ Customer journeys{#customer-journeys}`の下に配置しました。

### 例3 - デプロイメント SDK ページ

- トピックフォルダー：`experience-platform/deployment/`
- ファイル名：`mobile-sdk-architecture.md`
- ページタイトル：`Mobile SDK deployment architecture`

エントリ（6文字のスペースインデントに注意）:

```
      + [Mobile SDK deployment architecture](/help/blueprints/experience-platform/deployment/mobile-sdk-architecture.md)
```

`+ Architecture overviews{#architecture-overview}`内の`+ Deployment{#deployment}`の下に配置されました。

## 検証

TOC.mdを編集した後、影響を受けるサブセクションを再度読み、確認します。

1. 新しいエントリでは、インデントのスペースを4つだけ使用します（`Deployment`の下にネストされている場合は6つ）。
2. リンクターゲットは、ディスク上のファイルパス（`.md`拡張子を含む）と一致します。
3. エントリは正しいサブセクション内にグループ化され、サブセクション間でフローティングされません。
4. 既存のエントリは並べ替えまたは変更されませんでした。
