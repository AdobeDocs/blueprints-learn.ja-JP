---
title: パススルーマッピングの修正
description: 検証する前に、ターゲットフィールドの割り当ての重複や不一致など、誤ったAI/ML パススルーマッピングを特定して修正します。
doc-type: article
solution: Experience Platform
exl-id: b06cc091-661e-4ff4-b6e5-f16bc5128b6b
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---


# パススルーマッピングの修正

## 特定のマッピングをドロップ

必要なソースデータの一部は、計算フィールドを使用して処理する必要があります。  これらの問題に対処するには、マッピングからこれらを削除し、マッピングを再検証します。

1. マッピングから次のソースデータをドロップします。
   - birth\_date
   - 倉庫
   - sms\_optIn
1. 「検証」ボタンをクリックして、マッピングを再検証します

![&#x200B; フィールドを削除した後にマッピングを再検証するために使用される「検証」ボタン &#x200B;](assets/fix-passthrough-mappings-re-validate-mappings-using-validate-button.png "検証ボタンを使用してマッピングを再検証")

>[!NOTE]
>
>「検証」をクリックした後も、エラーが表示される場合があります



## 誤ったマッピング例

AIやマシンラーニングによるレコメンデーションが有効であるものの、時には間違っていることがあります。  レコメンデーションを調べると、修正が必要なエラーが見つかる場合があります

>[!NOTE]
>
>以下は、独自のサンドボックスに表示される無効なマッピングの例です。 また、他のエラーが表示されることもあります。

## マッピングの重複

このシナリオでは、AI/MLの推薦者が2つの異なるソースフィールドを同じターゲットフィールド **person.name.lastName**&#x200B;にマッピングしたことがわかります



![同じターゲットフィールド person.name.lastName](assets/fix-passthrough-mappings-person-lastname-mapped-twice.png "person.name.lastNameにマッピングされた2つの異なるソースフィールドは、このマッピングで2回マッピングされます")

![plan_name フィールドを含むパススルーマッピングの例を複製](assets/fix-passthrough-mappings-plan-name-duplicate-mapping.png)



## 不正なマッピング

このマッピングは正しく見えますが、詳しく確認すると、**email**&#x200B;は&#x200B;**emailFormat**&#x200B;と同じではありません

![電子メールがemailFormat](assets/fix-passthrough-mappings-email-mapped-incorrectly.png "ではなく誤ってマッピングされている場所のマッピングは正しくマッピングされているようですが、要件に従って正しくありません")

これは、**email\_optIn**&#x200B;が間違った同意オブジェクトに誤ってマッピングされている場所です

間違った同意オブジェクトに誤ってマッピングされた![email_optIn](assets/fix-passthrough-mappings-email-optin-wrong-consent-object.png "email_optInは正しくマッピングされているようですが、要件に従って正しくありません")



## パススルーマッピングの修正

間違ったターゲットフィールドを誤って指しているパススルーマッピングを修正するには、次の手順を実行します。

### 例

1. 無効なマッピングから開始し、ターゲットフィールドボックスをクリックします。 例えば、以下のマッピングでは、フィールド **person.name.lastName**&#x200B;が正しくマッピングされておらず、**planName**&#x200B;にマッピングされています
1. 右側に表示されるターゲットスキーマパネルで、適切なターゲットフィールドを選択し、**\_devbc.plan.name**&#x200B;を選択します
1. ターゲットフィールドは、ターゲットフィールドボックスで更新されます
1. このようなエラーを修正したら、**検証** ボタンを押して、これらの種類のエラーを減らし、新しいエラーを導入していないことを確認できるようにする必要があります。



![&#x200B; マッピングリストを操作して各マッピングエラーを修正する](assets/fix-passthrough-mappings-work-through-mapping-errors.png " マッピングとマッピングエラーの修正を行う")



![&#x200B; パススルーマッピングを修正するための正しいフィールドを選択するためのターゲットスキーマパネル &#x200B;](assets/fix-passthrough-mappings-choose-correct-target-field.png "適切なターゲットフィールドを選択し、パススルー要件に一致することを確認します")

>[!WARNING]
>
>すべてのマッピングエラーを解決するまで、次の手順に進まないでください
