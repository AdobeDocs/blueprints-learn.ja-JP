---
title: ID フィールドをマーク
description: XDM スキーマレジストリ APIを使用して、ID記述子がスキーマフィールドをプライマリ IDまたは非プライマリ IDとしてマークする方法について説明します。
doc-type: overview-page
solution: Experience Platform
exl-id: f6498584-0f4d-4baf-86b5-b00cc78e2ba7
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%
---

# ID フィールドをマーク

## ID記述子

フィールドをIDとしてマークするには、スキーマレジストリにID記述子を作成する必要があります。 スキーマ記述子の本文の例を次に示します。

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/customerID",
  "xdm:namespace": "customerID",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": true
}
```

- **@type** ->常に`xdm:descriptorIdentity`に設定
- フィールドが存在するスキーマの&#x200B;**xdm\:sourceSchema** -> `$id`
- **xdm\:sourceVersion** ->常に1
- スキーマ内のフィールドの&#x200B;**xdm\:sourceProperty** -> パス
- **xdm\:namespace** -> フィールドを格納するID名前空間コード
- **xdm\:property** ->常に`xdm:code`
- **xdm\:isPrimary** -> プライマリ IDが`true`の場合は`false`


## 目標

顧客アカウントスキーマのプライマリ IDと非プライマリ IDの両方を作成します。 次のセクションの手順を実行した後、スキーマは次のようになります。

![ プライマリ ID記述子と非プライマリ ID記述子を作成した後の顧客アカウントスキーマ ](assets/overview-schema-with-primary-and-non-primary-identities.png)
