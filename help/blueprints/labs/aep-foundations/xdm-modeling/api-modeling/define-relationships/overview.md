---
hold: true
title: 関係の定義
description: 関係記述子が、APIを介してXDM スキーマレジストリの顧客スキーマをルックアップスキーマにリンクする方法について説明します。
doc-type: overview-page
solution: Experience Platform
exl-id: be672c84-09ac-4941-b40e-da7bd3fd6704
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 関係の定義

## 関係記述子

あるスキーマから別のスキーマへの関係を作成するには、スキーマレジストリに関係記述子を作成する必要があります。 スキーマ記述子の本文の例を次に示します。

1対1の記述子

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:destinationSchema": "https://ns.adobe.com/devbc/schemas/6470f71181cf87aa39c2c2c43824eaa15f523652f7f88ff7",
  "xdm:destinationVersion": 1
}
```

参照ID記述子

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/6470f71181cf87aa39c2c2c43824eaa15f523652f7f88ff7",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:identityNamespace": "planID"
}
```

## 目標

顧客アカウントスキーマの関係IDを作成します。 次のセクションの手順を実行した後、スキーマは次のようになります。

関係と参照ID記述子を示す![顧客アカウントスキーマ ](assets/overview-schema-with-relationship-identities.png)
