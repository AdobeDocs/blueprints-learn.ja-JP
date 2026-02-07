---
source-git-commit: dfa21942ecf2a1db06df6f6cc945f5572811ca93
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 2%

---
# ブループリントドキュメントの参照 – 詳細なガイド

## ドキュメントタイプ

| タイプ | 目的 | 場所/例 |
|------|---------|--------------------|
| **概要/ ハブ** | 製品またはエリアを紹介します（シナリオブループリントへのリンク） | 例：`overview.md`、`journey-optimizer-overview.md` |
| **シナリオのブループリント** | 単一のユースケース：アーキテクチャ、手順、ガードレール | 例：`real-time-lookup.md`、`journey-optimizer-journeys.md` |
| **TOC** | ナビゲーション：コンテンツテンプレートとして使用しない | `help/blueprints/TOC.md` |

&#x200B;---

## セクション全体のリファレンス

### タイトルと説明（frontmatter）

- **タイトル**：短い、具体的。 製品名には `[!DNL Product Name]` を使用します（例：`[!DNL Journey Optimizer]`）。
- **説明**:1 つの文。 ブループリントの表示内容と結果（「Web およびモバイルパーソナライゼーション用のエッジでのリアルタイム顧客プロファイルアクセス」など）を説明します。

### 本文セクション

| セクション | 組み込むタイミング | コンテンツガイダンス |
|---------|-----------------|-------------------|
| **アプリケーション** | シナリオブループリントで常に使用 | 関係するAdobeの製品およびソリューション（Real-time Customer Data Platform、Data Collection など）の箇条書き。 |
| **ユースケース** | Always | このブループリントがサポートするビジネス/技術的なユースケースの箇条書き。 |
| **前提条件** | 設定が必要な場合 | 所定の場所に配置する必要がある製品、サブドメイン、SDK、設定。 設定手順については、Experience Leagueへのリンクを参照してください。 |
| **アーキテクチャ図** | Always | 1 つの 1 次図（SVG推奨）。 一貫したスタイル設定を使用：`style="width:90%; border:1px solid #4a4a4a" class="modal-image"`。 意味のある `alt` テキストを指定します。 |
| **ガードレール** | 製品にガードレールがある場合は常に実行 | Experience Leagueの公式ガードレールページへのリンク。 ブループリント固有の制限（TTL、レート制限など）を箇条書きとして追加します。 |
| **実装パターン** | 複数のアプローチがある場合 | 各パターンに名前を付けます（例：「パターン 1:Web SDKを使用したオーディエンスメンバーシップベース」）。使用するタイミングとトレードオフに箇条書きを使用します。 |
| **実装手順** | パスが定義されたシナリオブループリントの場合 | 番号付きリスト 各ステップ：アクション +手順が存在するExperience Leagueへのリンク。 完全なプロシージャはコピーしないでください。 |
| **実装に関する考慮事項** | 重要な注意点がある場合 | サブセクション（ID に関する考慮事項、属性ベースのパーソナライゼーションなど）。 箇条書きまたは短い段落。リンクして深さを指定します。 |
| **関連ドキュメント** | Always | Experience League（およびオプションでdeveloper.adobe.com）へのグループリンク。 以下の「Experience League リンクグループ」を参照してください。 |

### 概要/ハブページ

- 製品/エリアの 1～2 の段落から始め、ブループリントがカバーするもの。
- **ユースケース**：複数のカテゴリに対して `>[!BEGINTABS]` / `>[!TAB ...]` / `>[!ENDTABS]` を使用できます。
- **アーキテクチャ**:1 つのメイン図。
- **ブループリントシナリオ** または **統合パターン**：シナリオ名、短い説明およびシナリオのブループリントへのリンクを含むテーブル。
- **前提条件**、**ガードレール**、**関連ドキュメント**：上記と同じ、簡潔にしてください。

&#x200B;---

## Adobe Experience League - エージェントの指示

### Experience Leagueを参照するタイミング

- **製品ドキュメント**：製品の仕組み、UI フロー、概念。
- **API**：エンドポイント、パラメーター、例（Experience Platform、Edgeなど）。
- **ガードレール**：製品またはサービスの公式ガードレールページ。
- **チュートリアル**：ステップバイステップガイド（スキーマの作成、宛先のアクティブ化など）。
- **設定**：データストリーム、宛先、結合ポリシー、ID など。

Experience Leagueの長いプロシージャをブループリントに貼り付けないでください。 要約してリンクします。

### URL パターン

| コンテンツタイプ | ベース URL | サンプル パス |
|--------------|----------|--------------|
| Experience Platform ドキュメント | `https://experienceleague.adobe.com/docs/experience-platform/` | `.../profile/home.html`, `.../destinations/catalog/...` |
| Experience League（en） | `https://experienceleague.adobe.com/ja/docs/` | 上記と同じ構造で、`/en/` を使用します。 |
| Journey Optimizer | `https://experienceleague.adobe.com/docs/journey-optimizer/` | `.../using/get-started/guardrails.html` |
| Web SDK | `https://experienceleague.adobe.com/docs/experience-platform/web-sdk/` | `.../home.html`, `.../commands/command-responses.html` |
| Edge Network Server API | `https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/` | `.../overview.html`, `.../guardrails.html` |
| Mobile SDK | `https://developer.adobe.com/client-sdks/` | `.../home/`, `.../edge/adobe-journey-optimizer-decisioning/` |
| タグ | `https://experienceleague.adobe.com/docs/experience-platform/tags/` | `.../home.html` |
| Platform チュートリアル | `https://experienceleague.adobe.com/docs/platform-learn/tutorials/` | `.../profiles/create-merge-policies.html` |

現在のExperience League サイトに一致する正規パスを使用します（英語のパスが分かっている場合はよ `/en/docs/` 優先されます）。

### Markdown でのリンクの書式設定

- **説明リンクテキスト**:「ここをクリック」しませ `[Create schemas](https://experienceleague.adobe.com/ja...)`。
- **テキスト内の商品名**:Adobeスタイルごとに `[!DNL Product Name]` を使用します（例：`[!DNL Real-time Customer Profile]`）。
- **外部リンク**：テンプレートまたはパイプラインで必要な場合にのみ `{target="_blank"}` を追加します（リポジトリで既存のブループリントを確認します）。

### 関連ドキュメント – 推奨グループ

これらのグループは適用時に使用します。

1. **宛先設定** （アクティベーション/エッジパーソナライゼーションブループリント用）
2. **SDK ドキュメント** （Web SDK、Mobile SDK、Edge Network Server API、タグ）
3. **プロファイルとセグメント化** （リアルタイム顧客プロファイル、結合ポリシー、セグメント化）
4. **チュートリアル** （プラットフォーム学習または製品固有のステップバイステップガイド）
5. **製品ドキュメント** （メインの製品文書ホームまたは主要サブセクション）
6. **ガードレール** （「ガードレール」セクションにまだ入っていない場合）

例：

```markdown
## Related documentation

### Destination configurations
* [Custom Personalization Connection](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/personalization/custom-personalization)
* [Activate audiences to edge personalization destinations](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)

### SDK documentation
* [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html?lang=ja)
* [Edge Network Server API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)

### Profile and segmentation
* [Real-time Customer Profile](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=ja)
* [Profile Guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
```

&#x200B;---

## リポジトリと目次

- **ブループリントコンテンツのパス**:`help/blueprints/` （エリア別のサブフォルダーを含む（例：`audience-activation/`、`customer-journeys/journey-optimizer/`）。
- **Assets**：ブループリントと共同配置します（例：`assets/`、`images/`）。または共有フォルダーに配置します（例：`experience-platform/assets/`）。
- **TOC**：ブループリントページの追加、名前変更、移動の際に `help/blueprints/TOC.md` を編集します。 フロントマター（`user-guide-title`、`breadcrumb-title`、`user-guide-description`、`product`、`mini-toc-levels`、`role`）と `+` 階層を保持します。

&#x200B;---

## このリポジトリ内の参照の例

- **シナリオのブループリント（長い形式）**:`help/blueprints/audience-activation/real-time-lookup.md`
- **タブとテーブルを使用した概要/ハブ**:`help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md`
- **ガードレールに焦点を当てた**:`help/blueprints/experience-platform/guardrails.md`
- **ナビゲーション**:`help/blueprints/TOC.md`、`help/blueprints/overview.md`

これらを、セクションの順序、最前線、図の配置、Experience League リンクの使用のパターンとして使用します。
