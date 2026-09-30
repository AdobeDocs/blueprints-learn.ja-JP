---
title: Edge オーディエンスの作成
description: Edgeで評価されたオーディエンスを構築し、公開します。それぞれに対応するバッチを使用して、リアルタイムのイベントに対する対応を比較できます。
doc-type: article
solution: Experience Platform
exl-id: 79265a8f-81dd-41a3-89c5-c6646e435328
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%
---

# Edge オーディエンスの作成

このオーディエンスは、ペイロード（ページビューなど）がクライアント（Web SDKなど）からEdgeに送信される場合に、オーディエンスを選定するために使用されます。

>[!NOTE]
>
>通常、Edgeでオーディエンスを評価します。これにより、Personalizationでオーディエンスを有効にできます。 EdgeでPersonalizationを実行していない場合は、ハブでのストリーミングとしてオーディエンスを評価することができます。

## オーディエンスを作成

1. 左側のパネルで「オーディエンス」をクリックします
1. 次に、画面の右上隅にある「オーディエンスを作成」をクリックします
1. 「Build Rule」をクリックして



「オーディエンスを作成」ボタンと「ルールを作成」オプションが強調表示された![&#x200B; オーディエンスページ &#x200B;](assets/create-edge-audience-create-audience-step-1.png)



![新しいオーディエンスを作成するために開いたルール キャンバスを作成](assets/create-edge-audience-create-audience-step-2.png)



## オーディエンスをルールに変換

1. **Audiences**&#x200B;に移動し、**Experience Platform** フォルダーをクリックします
1. **dep: Any Event Streaming （within the hour）**&#x200B;という名前のオーディエンスをキャンバスにドラッグ&amp;ドロップ

   ![Depをドラッグする：任意のイベントストリーミング（1時間以内）のオーディエンスをルールビルダーキャンバスにドラッグします](assets/create-edge-audience-drag-audience-to-canvas.png)



1. 下の&#x200B;**アイコン**&#x200B;の表示をクリックし、**変換**&#x200B;をクリックして、オーディエンスをキャンバス内の一連のルールに変換します

![&#x200B; オーディエンスを一連のルールに変換するために使用されるキャンバス内の変換アイコン &#x200B;](assets/create-edge-audience-convert-to-rules-icon.png)

## イベントルールを更新

イベントルールに次の変更を加えます（イベントを展開する必要がある場合があります）

1. In Last
1. 15
1. 分

![過去15分間にトリガーに設定されたイベントルール &#x200B;](assets/create-edge-audience-update-event-rules.png)

## セグメントを公開

1. セグメント名を&#x200B;**Any Event Edge （15分以内）**&#x200B;に更新します
1. Edgeへの評価方法の更新
1. セグメントを公開

![公開前のEdgeの評価方法を示すセグメントの詳細](assets/create-edge-audience-publish-segment.png)

## バッチ評価セグメントを作成

作成したエッジセグメントと同じ手順を繰り返しますが、代わりに次の情報を使用します。

>[!NOTE]
>
>Edgeにイベントが渡されても、一括評価として保存されたオーディエンスは、ストリーミング方式で評価されないことがわかります。

イベントルール：

- In Last
- 1
- 日



セグメントの詳細：

- 名前 – > **任意のイベントバッチ（1日以内）**
- 評価方法 – > バッチ
