---
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---
# Experience League Agent Memory

## このリポジトリ内の主要な参照ファイル- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/metadata.md` - リポジトリレベルのメタデータのデフォルト- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/help/blueprints/TOC.md` - ガイドレベルのメタデータ- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/.cursor/skills/blueprint-document-reference/reference.md` - ブループリントオーサリングパターン

## メタデータルール（詳しくは metadata-fields.md を参照してください）- 記事前面の必須事項：`title`、`description`、`exl-id`- 記事の前面の内容を強く推奨：`solution`- `exl-id` は有効な UUID である必要があります。ファイルをコピーする場合は、削除するか空白のままにします（システムによって自動割り当て済み）- `description` は、「方法を学ぶ」から始める必要があります。 または「詳細情報…」 Adobeごとのガイドライン- SEO の場合 `title` 最大 60 文字。タイトルの製品名には `[!DNL ProductName]` を使用します- 値 `solution`、大文字と小文字が区別され、承認済みの列挙に一致する必要があります（metadata-fields.md を参照）- `thumbnail: null` または `thumbnail:` （空白）の両方が使用されます。空を指定することもできます- `kt:` はレガシーフィールド（サポート情報記事の JIRA 番号）です。このリポジトリに引き続き表示されます。空白でも構いません- TOC ファイルで使用：`user-guide-title`、`breadcrumb-title`、`user-guide-description`、`product`、`mini-toc-levels`、`role`- リポジトリレベルの `metadata.md` は次を使用します：`cloud`、`solution`、`product`、`type`、`doc-type`、`mini-toc-levels`、`git-repo`、`index`

## このリポジトリの一般的なパターン（blueprints-learn.en）- ほとんどのブループリントファイルには、`title`、`description`、`solution`、`exl-id` があります- 一部の古いファイルには、`kt`、`thumbnail` も含まれます。- 一部のファイルでは `version` （Campaign v8 ブループリント）が使用されます- 概要ページでの `doc-type: overview-page` の使用- `solution` には多くの場合、複数のコンマ区切り値が含まれています。例：`Real-Time Customer Data Platform, Campaign`- `exl-id` が存在する場合、`solution` のないファイルは引き続き検証に合格します

## このリポジトリで使用されるAdobe Markdown 拡張機能- `>[!NOTE]`, `>[!TIP]`, `>[!IMPORTANT]`, `>[!WARNING]`, `>[!CAUTION]`- タブ付きコンテンツの `>[!BEGINTABS]`/`>[!TAB Name]`/`>[!ENDTABS]`- `[!DNL ProductName]` – 製品名のタグをローカライズしない- `[!UICONTROL Label]` — UI コントロール参照- `&lbrace;zoomable="yes"&rbrace;` – 画像ズーム属性- `&lbrace;width="1000"&rbrace;` – 画像の幅の属性- `&lbrace;target="_blank"&rbrace;` – 外部リンクターゲット

## 詳細参照- 完全なメタデータフィールド参照：`metadata-fields.md`- オーサリングガイドのクロール: https://experienceleague.adobe.com/en/docs/authoring-guide-exl/using/home（2026 年 2 月）
