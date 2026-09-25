---
source-git-commit: c766cd3153efce4635089d008daf3eb426eb7a24
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%
---
# TOC.md プレースメント リファレンス

スキルが新しいアーキテクチャ図ページを生成する場合、そのページがサイトナビゲーションで見つけられるように、エントリを`/help/blueprints/TOC.md`に追加する必要があります。 このドキュメントでは、そのエントリの場所と方法を正確に定義します。

## 親セクション

すべてのアーキテクチャ図ページは、TOC.mdのトップレベル `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` セクションの下にあります。 このセクションでは、いくつかのサブセクションでページをトピック別にグループ化します。

これらのサブセクションのフォルダー名、目次アンカー、目次ラベルは、`../../architecture-diagram-category-builder/references/naming-conventions.md`の命名規則に従う必要があります。新しいカテゴリが必要になった場合は、そのファイルを参照してください（このカテゴリではなく、`architecture-diagram-category-builder` スキルを使用してください）。

## サブスクルーマッピング

新しいページのトピックフォルダーに一致するサブセクションを選択します。

| トピックフォルダー | 目次サブセクション見出し |
| --- | --- |
| `architecture-diagrams/architecture-overviews/` | `+ Architecture overviews{#architecture-overviews}` |
| `architecture-diagrams/audience-profile-activation/` | `+ Audience & Profile Activation{#audience-profile-activation}` |
| `architecture-diagrams/b2b-activation-marketing/` | `+ B2B activation & marketing{#b2b-activation-marketing}` |
| `architecture-diagrams/customer-insights/` | `+ Customer Insights{#customer-insights}` |
| `architecture-diagrams/customer-journeys/` | `+ Customer journeys{#customer-journeys}` |

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

`+ Architecture overviews{#architecture-overviews}`にはネストされたグループ化がありません。`architecture-diagrams/architecture-overviews/`の下のすべてのページ （SDK デプロイメントページを含む、`websdk.md`、`appsdk.md`など）は、同じ4つのスペースのインデントレベルに配置されています。 その他のサブセクション （`Audience & Profile Activation`、`B2B activation & marketing`など） ネストされたグループ化が含まれている可能性があります。エントリを配置する前に、セクションを調べます。 ネストされたグループが存在し、新しいページがその中に属する場合は、さらに2つのスペースをインデントします。それ以外の場合は、サブセクションの最上位レベルにエントリを配置します。

## 使用例

### 例1 — トップレベルのAEP ページ

- トピックフォルダー：`architecture-diagrams/architecture-overviews/`
- ファイル名：`mix-modeler-integration.md`
- ページタイトル：`Adobe Mix Modeler integration with Experience Platform`

エントリ：

```
    + [Adobe Mix Modeler integration with Experience Platform](/help/blueprints/architecture-diagrams/architecture-overviews/mix-modeler-integration.md)
```

`+ Architecture overviews{#architecture-overviews}`の下に配置しました。

### 例2 - AJOジャーニーアーキテクチャ

- トピックフォルダー：`architecture-diagrams/customer-journeys/`
- ファイル名：`cross-channel-journey-architecture.md`
- ページタイトル：`Cross-channel journey architecture`

エントリ：

```
    + [Cross-channel journey architecture](/help/blueprints/architecture-diagrams/customer-journeys/cross-channel-journey-architecture.md)
```

`+ Customer journeys{#customer-journeys}`の下に配置しました。

### 例3 - SDKのデプロイメントページ

- トピックフォルダー：`architecture-diagrams/architecture-overviews/`
- ファイル名：`mobile-sdk-architecture.md`
- ページタイトル：`Mobile SDK deployment architecture`

エントリ（他のアーキテクチャ概要ページと同じ4つのスペースインデント）:

```
    + [Mobile SDK deployment architecture](/help/blueprints/architecture-diagrams/architecture-overviews/mobile-sdk-architecture.md)
```

`+ Architecture overviews{#architecture-overviews}`の下に配置しました。

## 検証

TOC.mdを編集した後、影響を受けるサブセクションを再度読み、確認します。

1. 新しいエントリでは、インデントのスペースを4つだけ使用します（サブセクション固有のグループ化の下にネストされている場合は6つ、例：`Audience & Profile Activation` RTCDPのグループ化）。
2. リンクターゲットは、ディスク上のファイルパス（`.md`拡張子を含む）と一致します。
3. エントリは正しいサブセクション内にグループ化され、サブセクション間でフローティングされません。
4. 既存のエントリは並べ替えまたは変更されませんでした。
