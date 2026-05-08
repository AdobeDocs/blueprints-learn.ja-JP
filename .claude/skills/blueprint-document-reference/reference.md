---
source-git-commit: 83e85d946e455cde46001af0a2112637b7fe24cc
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 1%

---
# ブループリントドキュメントリファレンス – 詳細ガイド

## ドキュメントタイプ

| タイプ | 目的 | 場所/例 |
|------|---------|--------------------|
| **概要/ ハブ** | 製品または領域を紹介します。シナリオブループリントへのリンク | e.g. `overview.md`, `journey-optimizer-overview.md` |
| **シナリオの設計図** | 単一のユースケース：アーキテクチャ、ステップ、ガードレール | e.g. `real-time-lookup.md`, `journey-optimizer-journeys.md` |
| **目次** | ナビゲーション。コンテンツテンプレートとして使用しない | `help/blueprints/TOC.md` |

---

## フルセクション参照

### タイトルと説明（frontmatter）

- **title**：短く、具体的です。 製品名には`[!DNL Product Name]`を使用します（例：`[!DNL Journey Optimizer]`）。
- **説明**:1文。 この設計図が示すところと成果（例：「webとモバイルのパーソナライゼーションにおけるエッジでのリアルタイムの顧客プロファイルアクセス」）について説明します。

### 本文セクション

| セクション | 含めるタイミング | コンテンツガイダンス |
|---------|-----------------|-------------------|
| **アプリケーション** | シナリオの設計図を常に表示 | 関わり合うAdobe製品/ソリューションの一覧（例：Real-Time Customer Data Platform、データ収集） |
| **ユースケース** | 常に | このブループリントがサポートするビジネス/テクノロジーのユースケースのリスト。 |
| **前提条件** | 設定が必要な場合 | 製品、サブドメイン、SDK、設定を配置する必要があります。 設定手順については、Experience Leagueにリンクしてください。 |
| **アーキテクチャ図** | 常に | 単一のプライマリ図（SVGが望ましい）: 一貫したスタイル設定を使用：`style="width:90%; border:1px solid #4a4a4a" class="modal-image"`。 意味のある`alt` テキストを入力してください。 |
| **ガードレール** | 製品にガードレールがある場合は必ず | Experience Leagueのガードレールに関する公式ページへのリンク。 ブループリント固有の制限（TTL、レート制限など）を箇条書きとして追加します。 |
| **実装パターン** | 複数のアプローチが存在する場合 | 各パターンに名前を付けます（「パターン 1:Web SDKを使用したオーディエンスメンバーシップに基づく」）。使用するタイミングとトレードオフには箇条書きを使用します。 |
| **実装手順** | 定義されたパスを持つシナリオブループリントの場合 | 番号付きリスト： 各ステップ：アクション+手順が住んでいるExperience Leagueへのリンク。 完全な手順はコピーしないでください。 |
| **実装の考慮事項** | 重要な注意事項がある場合 | サブセクション（例：IDに関する考慮事項、属性ベースのパーソナライゼーション） 箇条書きまたは短い段落。深さについてはリンクを張ってください。 |
| **関連ドキュメント** | 常に | Experience Leagueへのグループ化されたリンク（およびオプションでdeveloper.adobe.com）。 以下の「Experience League リンクグループ」を参照してください。 |

### 概要/ハブページ

- まず、製品/エリアと、ブループリントでカバーされている内容について1～2段落から始めます。
- **ユースケース**：複数のカテゴリに`>[!BEGINTABS]` / `>[!TAB ...]` / `>[!ENDTABS]`を使用できます。
- **アーキテクチャ**:1つのメイン ダイアグラム。
- **ブループリントシナリオ**&#x200B;または&#x200B;**統合パターン**: シナリオ名、簡単な説明、およびシナリオのブループリントへのリンクを含むテーブル。
- **前提条件**、**ガードレール**、**関連ドキュメント**：上記と同様。簡潔に保ちます。

---

## Adobe Experience League — エージェントの指示

### Experience Leagueを参照するタイミング

- **製品ドキュメント**：製品の仕組み、UIの流れ、概念。
- **API**: エンドポイント、パラメーター、例（Experience Platform、Edgeなど）。
- **ガードレール**：製品またはサービスの公式ガードレール ページ。
- **チュートリアル**：ステップバイステップガイド（スキーマの作成、宛先のアクティブ化など）。
- **設定**: データストリーム、宛先、結合ポリシー、IDなど

Experience Leagueの長い手順をブループリントにペーストしないでください。 要約とリンク：

### URL パターン

| コンテンツタイプ | ベース URL | パスの例 |
|--------------|----------|--------------|
| Experience Platform docs | `https://experienceleague.adobe.com/docs/experience-platform/` | `.../profile/home.html`, `.../destinations/catalog/...` |
| Experience League （en） | `https://experienceleague.adobe.com/en/docs/` | `/en/`と同じ構造です。 |
| Journey Optimizer | `https://experienceleague.adobe.com/docs/journey-optimizer/` | `.../using/get-started/guardrails.html` |
| Web SDK | `https://experienceleague.adobe.com/docs/experience-platform/web-sdk/` | `.../home.html`, `.../commands/command-responses.html` |
| Edge Network Server API | `https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/` | `.../overview.html`, `.../guardrails.html` |
| Mobile SDK | `https://developer.adobe.com/client-sdks/` | `.../home/`, `.../edge/adobe-journey-optimizer-decisioning/` |
| タグ | `https://experienceleague.adobe.com/docs/experience-platform/tags/` | `.../home.html` |
| プラットフォームチュートリアル | `https://experienceleague.adobe.com/docs/platform-learn/tutorials/` | `.../profiles/create-merge-policies.html` |

現在のExperience League サイトに一致する正規パスを使用します（英語パスがわかっている場合は`/en/docs/`を優先します）。

### Markdownでのリンクの書式

- **説明リンクテキスト**: `[Create schemas](https://experienceleague.adobe.com/...)`は「ここをクリック」ではありません。
- **テキスト内の商品名**: Adobe スタイルごとに`[!DNL Product Name]`を使用します（例：`[!DNL Real-time Customer Profile]`）。
- **外部リンク**: テンプレートまたはパイプラインが必要な場合にのみ`{target="_blank"}`を追加します（リポジトリの既存のブループリントを確認してください）。

### 関連ドキュメント – 推奨グループ

これらのグループを適用する場合は、次のグループを使用します。

1. **宛先設定** （アクティベーション/エッジパーソナライゼーションブループリント用）
2. **SDK ドキュメント** （Web SDK、モバイル SDK、Edge Network Server API、タグ）
3. **プロファイルとセグメント化** （リアルタイム顧客プロファイル、結合ポリシー、セグメント化）
4. **チュートリアル** （プラットフォーム学習または製品固有のステップバイステップガイド）
5. **製品ドキュメント** （メイン製品ドキュメントのホームまたは主要なサブセクション）
6. **ガードレール** （ガードレール セクションにまだ存在しない場合）

例：

```markdown
## Related documentation

### Destination configurations
* [Custom Personalization Connection](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization)
* [Activate audiences to edge personalization destinations](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)

### SDK documentation
* [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html)
* [Edge Network Server API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html)

### Profile and segmentation
* [Real-time Customer Profile](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html)
* [Profile Guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
```

---

## リポジトリと目次

- **ブループリントコンテンツパス**: `help/blueprints/` （サブフォルダーは領域別です（例：`audience-activation/`、`customer-journeys/journey-optimizer/`）。
- **Assets**: ブループリント （例：`assets/`、`images/`）または共有フォルダー（例：`experience-platform/assets/`）に配置します。
- **目次**: ブループリントページを追加、名前変更、または移動する際に`help/blueprints/TOC.md`を編集します。 フロントマター（`user-guide-title`、`breadcrumb-title`、`user-guide-description`、`product`、`mini-toc-levels`、`role`）と`+`階層を保持します。

---

## このリポジトリの参照例

- **シナリオの設計図（長いフォーム）**: `help/blueprints/audience-activation/real-time-lookup.md`
- **タブとテーブルを含む概要/ハブ**: `help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md`
- **ガードレール中心**: `help/blueprints/experience-platform/guardrails.md`
- **ナビゲーション**: `help/blueprints/TOC.md`、`help/blueprints/overview.md`

これらのパターンを、セクションの順序、フロントマター、ダイアグラムの配置、Experience League リンクの使用状況に使用します。
