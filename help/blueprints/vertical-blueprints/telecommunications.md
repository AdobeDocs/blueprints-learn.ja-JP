---
title: 通信業界 – トリガーメッセージのためのJourney Optimizer
description: 顧客の長期ロイヤリティに対する効率的なオンボーディングと併せ、顧客に合わせてリアルタイムの契約を提供します。
solution: Journey Optimizer
kt: 9486
exl-id: fa4a6569-3972-4b97-91f1-7ca8ffd3c5b3
source-git-commit: cf7721ea01579182fdb200aad448be6fc94b34cf
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 85%

---

# 通信業界のビジネス課題

このブループリントを実装する前に、通信会社の「新しい行を追加」メールキャンペーンは、ユーザーがコンバージョンしたかどうかに依存し、7 日間の待機期間後にのみチェックしました。 これらの条件を満たすと、追加のタッチポイントが開始されます。

この制限は、現在の状態の 7 日間の待機期間よりも早い行を追加したいユーザーに対して、よりタイムリーなフォローアップを開始するために解決する必要がありました。

## アドビのアプローチ

* Adobe Journey Optimizer で使用するデータソースとして、変換に失敗して新しい行を追加したユーザーを識別する Adobe Analytics データが含まれます。
* Adobe Journey Optimizer は、ルールを使用して、顧客がアカウントに新しい行を追加することによって変換するように促すように設計された、カスタマイズされた「放棄」メッセージを受信するタイミングを設定します。

## 提供されるビジネスバリュー

| 目標 | 戦術 | 解放されたバリュー |
|---|---|---|
| **キャンペーンのコンバージョン率の向上&#x200B;**<br></br>**年間アカウント収益の増加**</ul> | <ul><li>行の追加に関心を示しはしたたが、まだコンバージョンに至っていないユーザーに対して、ほぼリアルタイムで新しいセグメントを作成します。</li><li>コンバータに関心はあるが、まだコンバージョンに至っていない顧客に対して、第 2 のタッチポイントを使用してフォローアップを推進します。 </li><li>テスト戦略を使用して、ジャーニーのパフォーマンスを測定し、電子メールによるコンバージョンを最適化します。</li></ul> | <ul><li><strong>高品質で関連性の高いエクスペリエンス：</strong> ジャーニーオーケストレーションを導入することで、顧客はより関連性の高いメッセージを体験し、メールリストの頻繁な変更を回避できます。</li><li><strong>大規模な Journey Orchestration：</strong>パーソナライズされた、よりタイムリーなジャーニーを作成して、コンバージョンと総収入を増やすことができます。</li></ul> |

## プライマリブループリント：Experience Cloudアプリケーションを使用したオーディエンスとアクティベーション

### 説明

<ul><li>ストリーミングデータ、顧客プロファイル、セグメント化の中央ハブとしての Adobe Experience Platform と、ストリーミングジャーニーオーケストレーションとメッセージ配信のための Journey Orchestration を使用して、トリガーされるメッセージとストリーミングメッセージングを実行します</li></ul>

### Experience Cloud アプリケーション

<ul><li>Adobe Journey Optimizer</li></ul>

### ブループリントアーキテクチャ

<a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=ja"><img alt="顧客の長期ロイヤリティに対する効率的なオンボーディングを提供しながら、顧客に合わせてリアルタイムの契約を提供する通信業の画像" src="https://experienceleague.adobe.com/docs/blueprints-learn/assets/ajo-architecture.svg"/></a>
