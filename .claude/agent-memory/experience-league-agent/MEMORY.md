---
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: b88e86c3ab3b344de7dbc2b207b2b107d9ea27cb
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 2%
---

# Experience League Agent Memory

## このリポジトリの主要な参照ファイル
- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/metadata.md` — リポジトレベルのメタデータの既定値
- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/help/blueprints/TOC.md` — ガイドレベルのメタデータ
- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/.cursor/skills/blueprint-document-reference/reference.md` — ブループリントのオーサリング パターン

## メタデータルール（完全な参照についてはmetadata-fields.mdを参照）
- 記事の前面記事が必要です：`title`、`description`、`exl-id`
- 記事の前面事項を強くお勧めします：`solution`
- `exl-id`は有効なUUIDである必要があります。ファイルをコピーする場合は削除または空白のままにします（システムによって自動割り当て）
- `description`が「方法を学ぶ…」を開始する必要があります。 または「詳細…」を参照してください。 Adobeのガイドラインに準拠
- SEOには最大`title`文字まで。タイトルの商品名には`[!DNL ProductName]`を使用してください
- `solution`値は大文字と小文字を区別し、承認済み列挙に一致する必要があります（metadata-fields.mdを参照）
- `thumbnail: null`または`thumbnail:` （空白）は両方とも使用されます。空でも構いません
- `kt:`はレガシーフィールド （ナレッジ記事JIRA番号）です。このリポジトリにはまだ表示されます。空白でも構いません
- TOC ファイルの使用条件：`user-guide-title`、`breadcrumb-title`、`user-guide-description`、`product`、`mini-toc-levels`、`role`
- リポジトレベル `metadata.md`では、`cloud`、`solution`、`product`、`type`、`doc-type`、`mini-toc-levels`、`git-repo`、`index`が使用されています

## このリポジトリの一般的なパターン（blueprints-learn.en）
- ほとんどのブループリントファイルには、`title`、`description`、`solution`、`exl-id`があります
- 一部の古いファイルには、`kt`、`thumbnail`もあります
- 一部のファイルは`version` （Campaign v8 ブループリント）を使用します
- 概要ページは`doc-type: overview-page`を使用しています
- `solution`には、多くの場合、複数のコンマ区切り値が含まれます。例：`Real-Time Customer Data Platform, Campaign`
- `solution`のないファイルは、`exl-id`が存在する場合でも検証に合格します

## このリポジトリで使用されているAdobe Markdown Extensions
- `>[!NOTE]`, `>[!TIP]`, `>[!IMPORTANT]`, `>[!WARNING]`, `>[!CAUTION]`
- タブ付きコンテンツの`>[!BEGINTABS]` / `>[!TAB Name]` / `>[!ENDTABS]`
- `[!DNL ProductName]` – 製品名のタグをローカライズしない
- `[!UICONTROL Label]` — UI コントロール参照
- `{zoomable="yes"}` – 画像ズーム属性
- `{width="1000"}` – 画像の幅の属性
- `{target="_blank"}` – 外部リンクのターゲット

## 詳細参照
- 完全なメタデータフィールド参照：`metadata-fields.md`
- オーサリングガイドをクロール: https://experienceleague.adobe.com/en/docs/authoring-guide-exl/using/home （2026年2月）
