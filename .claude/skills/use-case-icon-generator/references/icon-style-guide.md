---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 3%

---
# ユースケースアイコンのスタイルガイド

## 概要

ユースケースアイコンは、ユースケースカタログテーブルで視覚的な識別子として機能します。 ネイティブの 1024 x 1024 解像度の画質を維持しながら、40 ピクセルのディスプレイ幅ですぐに認識できる必要があります。

## 技術仕様

| プロパティ | 値 |
| --- | --- |
| ディメンション | 1024 x 1024 ピクセル |
| 書式設定 | PNG （8 ビット RGBまたは RGBA） |
| ファイルサイズ | 900 KB - 1.4 MB （標準） |
| 表示サイズ | カタログテーブルの幅 40 px |
| 名前付け | `icon-{kebab-case-name}.png` |
| ストレージパス | `/help/blueprints/industry-use-cases/assets/use-case-icons/{industry}/` |

## ビジュアルスタイルガイドライン

### 構成
- **単一の中心的な件名** – 各アイコンには、ユースケースの概念を表す明確な視覚的隠喩を 1 つ使用する必要があります
- **中央揃えの構成** - メインサブジェクトは、バランスの取れた空白を中心にする必要があります
- **テキストなし** - テキストは 40 ピクセルで判読できません。完全に視覚的隠喩に依存します
- **複雑なシーンなし** – 複数要素のコンポジション、多数のオブジェクトを含む背景、または物語のシーンは避けます
- **太字のシルエット** - アイコンの形状は、小さなシルエットでも認識できるはずです

### カラーとトーン
- **クリーンでモダンなパレット** — プロフェッショナルな企業に適したカラーを使用します。
- **業界の団結** – 同じ業界内のアイコンは、一緒に属しているように感じる必要があります
- **高コントラスト** – 背景から被写体を際立たせる
- **ネオンや彩度が高すぎる色を避ける** — パレットを洗練され、プロフェッショナルな状態に保ちます

### スタイル
- **モダンでプロフェッショナル** - クリーンなライン、洗練された仕上げ
- **一貫したレンダリング** – すべてのアイコンが同じデザインシステムから取得されているように表示されます
- **3D またはフラットは許容されます** – ただし、業界の業界内では一貫性があります
- **写実的な表現を避ける** – 一貫性を保つために好まれるイラストやレンダリングのスタイル
- **ブランドロゴや商標画像なし** – 一般的な視覚的隠喩を使用します。

### 小型読み取り検査
ファイナライズする前に、画像を 40 ピクセルに精神的に拡大・縮小します。
- 主要主題を特定できますか？
- 前景と背景の間には十分なコントラストがありますか？
- 視覚的なノイズに変わる細かい部分はありますか？
- アクセシビリティの場合に、図形は色なしで明確に読み取れますか？

## 業種別の視覚的隠喩の例

### 小売
| ユースケース | 視覚的隠喩 |
| --- | --- |
| 放棄されたカート | アイテムを含む買い物かご |
| 製品レコメンデーション | ギフトボックスまたはキュレートされた製品 |
| クロスセルのアップセル | 接続された買い物かご |
| ウェルカムシリーズ | ウェルカムカードまたはギフト |
| 価格の下落 | 下矢印の付いた価格タグ |

### 自動車用
| ユースケース | 視覚的隠喩 |
| --- | --- |
| サービスリマインダー | レンチまたはサービスカレンダー |
| 車両購入 | キー付き車 |
| 下取り | 車の交換矢印 |
| コネクテッドカー | デジタル接続車 |

### ヘルスケア
| ユースケース | 視覚的隠喩 |
| --- | --- |
| 予定リマインダー | 聴診器付きカレンダー |
| 薬剤の遵守 | ピルボトルまたは処方箋 |
| 予防ケア | ヘルスシンボル付きシールド |

### 金融サービス
| ユースケース | 視覚的隠喩 |
| --- | --- |
| リード育成 | 成長期チャートまたは苗 |
| チャーンの防止 | シールドまたは保持シンボル |
| ライフステージ | ライフマイルストーンタイムライン |

### B2B
| ユースケース | 視覚的隠喩 |
| --- | --- |
| ABM | 建物のあるターゲット |
| リードスコアリング | 採点ゲージまたは温度計 |
| 契約の更新 | 更新記号を含むドキュメント |

### 旅行およびホスピタリティ
| ユースケース | 視覚的隠喩 |
| --- | --- |
| 買い物かご放棄 | スーツケースまたは予約 |
| ロイヤルティプログラム | ロイヤルティカードまたはスターバッジ |
| 予約のリマインダー | 飛行機/ホテル付きカレンダー |

### 保険
| ユースケース | 視覚的隠喩 |
| --- | --- |
| ポリシーの更新 | 更新の矢印付きドキュメント |
| 請求プロセス | チェックマーク付きクリップボード |
| クロスセル | 接続されたポリシードキュメント |

### メディアとエンターテイメント
| ユースケース | 視覚的隠喩 |
| --- | --- |
| 新しいコンテンツ | 再生ボタンまたはスポットライト |
| Content Recommendations | キュレートされたプレイリストまたは星付きコンテンツ |
| 購読チャーン | 破損したサブスクリプションカード |

### 通信
| ユースケース | 視覚的隠喩 |
| --- | --- |
| プランの最適化 | ギア付きシグナル バー |
| デバイスのアップグレード | 電話（上向き矢印） |
| チャーンの防止 | 信号付きシールド |

## 画像生成プロンプトテンプレート

このテンプレートを出発点として使用し、ユースケースごとに件名と詳細をカスタマイズします。

```
A clean, modern icon illustration of {visual metaphor} representing {use case concept}. Professional corporate design style with bold shapes and clean lines. Single centered subject on a {solid/gradient} background. High contrast, vibrant but refined color palette. No text, no fine details, no complex backgrounds. The icon must be clearly recognizable when scaled down to 40 pixels. Square format, 1024x1024 pixels.
```

### プロンプトのカスタマイズのヒント

- **内容を具体的に説明してください** – 「買い物かご」よりも、「カラフルなギフトボックスが 2 つ入った真っ赤な買い物かご」の方が適切です。
- **背景の処理を指定**— 「ソフトブルーのグラデーション背景で」または「微妙な影のきれいな白い背景で」
- **ライティングに言及** — 「ソフトスタジオ照明」または「穏やかなアンビエントグロー」により、一貫性を実現
- **スタイル修飾子の追加** - 「ミニマリスト」、「ジオメトリック」、「アイソメトリック」、「フラットデザイン」のいずれかで、美的な雰囲気を演出します。
- **サポートされている場合、負のプロンプトを含める** – 「テキストなし、透かし、境界線なし、写実的な要素なし」

## 既存のアイコン インベントリ

### 業界別

**小売（9 つのアイコン）:**
アイコン放棄された買い物かご，アイコン在庫緊急度，アイコン価格低下，アイコン製品レコメンデーション，アイコンのカテゴリページ，アイコンようこそシリーズ，アイコン補充，アイコン購入後，アイコンのクロス販売 – アップセル

**自動車用（12 アイコン）:**
icon-service-reminders、icon-recall-notifications、icon-test-drive、icon-model-launch、icon-trade-in、icon-parts-accessories、icon-warranty、icon-connected-car、icon-dealer-network、icon-vehicle-purchase、icon-financing、icon-owner-loyalty

**金融サービス（6 つのアイコン）:**
icon-lead-nurturing, icon-account-dashboard, icon-product-recommendation, icon-churn-prevention, icon-life-stage

**ヘルスケア（4 つのアイコン）:**
icon-appointment-reminder, icon-post-visit, icon-preventive-care, icon-medication-adstruction

**保険（3 つのアイコン）:**
icon-policy-renewal, icon-claims-process, icon-cross-sell

**メディアとエンターテインメント（3 つのアイコン）:**
icon-new-content, icon-content-recommendations, icon-subscription-churn

**通信機能（3 つのアイコン）:**
icon-plan-optimization, icon-device-upgrade, icon-churn-prevention

**旅行・ホスピタリティ（12 アイコン）:**
icon-cart-abandonment, icon-booking-reminders, icon-seasonalized-campaigns, icon-personalized-homepage, icon-high-intent, icon-post-booking-upsell, icon-win-back, icon-dynamic-itinerary, icon-recently-browsed, icon-group-booking, icon-exit-intent, icon-loyalty-program

**B2B （11 アイコン）:**
icon-webinar-demo, icon-abm, icon-lead-scoring, icon-content-personalization, icon-event-registration, icon-trial-conversion, icon-customer-onboarding, icon-competitive-replacement, icon-case-study, icon-contract-renewal, icon-upsell-expansion
