---
title: 產品資源
description: 代表可購買商品或服務的資源。 包含用來描述產品類型和圖形（SKU）的資源，以及用於檢查清查產品的可用性。
ms.assetid: 80C1F9B5-35FB-4DD8-B501-03467E1D75AD
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d733c956f4742a7299e847e7ff48130a6b268df6
ms.sourcegitcommit: 45094b6fb1437bca51f97e193ac2957747dbea27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82124641"
---
# <a name="products-resources"></a>產品資源

**適用于**

- 合作夥伴中心

代表可購買商品或服務的資源。 包含用來描述產品類型和圖形（SKU）的資源，以及用於檢查清查產品的可用性。

## <a name="product"></a>Products

代表可購買良好或服務。 產品本身並不是可購買專案。

| 屬性           | 類型                          | 描述                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| id                 | 字串                        | 此產品的識別碼。                                                 |
| title              | 字串                        | 產品標題。                                                       |
| description        | 字串                        | 產品描述。                                                 |
| productType        | [ItemType](#itemtype)         | 物件，描述此產品的類型分類。     |
| isMicrosoftProduct | bool                          | 指出這是否為 Microsoft 產品。                          |
| publisherName      | 字串                        | 產品的發行者名稱（如果有的話）。                          |
| 連結              | [ProductLinks](#productlinks) | 包含在產品內的資源連結。                         |

## <a name="itemtype"></a>ItemType

表示產品的類型。

| 屬性        | 類型                          | 描述                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | 字串                        | 類型識別碼。                                                                 |
| displayName     | 字串                        | 此類型的顯示名稱。                                                      |
| 類型         | [ItemType](#itemtype)         | 選擇性。 物件，描述這個專案類型的子類型分類。     |

## <a name="productlinks"></a>ProductLinks

包含[產品](#product)的連結清單。

| 屬性        | 類型                                                          | 描述                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| sku            | [連結](utility-resources.md#link)                             | 用來存取基礎 Sku 的連結。          |
| 連結           | [ResourceLinks](utility-resources.md#resourcelinks)           | 包含在此資源內的資源連結。   |

## <a name="sku"></a>SKU

代表產品下的可購買庫存單位（SKU）。 這些代表產品的不同形狀。

| 屬性               | 類型             | 描述                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| id                     | 字串           | 此 SKU 的識別碼。 此識別碼只在其父產品的內容中是唯一的。 |
| title                  | 字串           | SKU 的標題。                                                                 |
| description            | 字串           | SKU 的描述。                                                           |
| productId              | 字串           | 包含此 SKU 之父[產品](#product)的識別碼。                      |
| minimumQuantity        | int              | 允許購買的最小數量。                                            |
| maximumQuantity        | int              | 允許購買的最大數量。                                            |
| isTrial                | bool             | 指出此 SKU 是否為試用專案。                                           |
| supportedBillingCycles | 字串的陣列 | 此 SKU 支援的計費週期清單。 支援的值為在 [BillingCycleType](#billingcycletype) 中找到的成員名稱。 |
| purchasePrerequisites  | 字串的陣列 | 購買此專案之前所需的先決條件步驟或動作清單。 支援的值為：<br/>  "InventoryCheck"-表示在嘗試購買此專案之前，應該先評估該專案的清查。<br/> "AzureSubscriptionRegistration"-表示需要 Azure 訂用帳戶，且必須先註冊，才能嘗試購買此專案。  |
| inventoryVariables     | 字串的陣列 | 在此專案上執行清查檢查所需的變數清單。 支援的值為：<br/> "CustomerId"-購買的客戶識別碼。<br/> "AzureSubscriptionId"-azure 訂用帳戶的識別碼，可用於購買 Azure 保留。</br> "ArmRegionName"-要驗證清查的區域。 此值必須符合 SKU DynamicAttributes 中的 "ArmRegionName"。 |
| provisioningVariables  | 字串的陣列 | 購買此專案時，必須提供給[購物車明細專案](cart-resources.md#cartlineitem)之布建內容的變數清單。 支援的值為：<br/> 範圍-Azure 保留購買的範圍：「單一」、「共用」。<br/> 「SubscriptionId」-azure 訂用帳戶的識別碼，可用於購買 Azure 保留。<br/> 「持續時間」-Azure 保留的持續時間：「1Year」、「3Year」。  |
| dynamicAttributes      | 索引鍵/值組  | 套用至此專案之動態屬性的字典。 請注意，此字典中的屬性是動態的，而且可以變更，恕不另行通知。 您不應該針對此屬性值中的特定索引鍵建立強式相依性。    |
| 連結                  | [ResourceLinks](utility-resources.md#resourcelinks) | SKU 中包含的資源連結。                   |

## <a name="availability"></a>可用性

代表可以購買 SKU 的設定（例如國家/地區、貨幣和產業區段）。

| 屬性        | 類型                        | 描述                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| id              | 字串                        | 此可用性的識別碼。 此識別碼只在其父[產品](#product)和[SKU](#sku)的內容中是唯一的。 **注意**此識別碼會隨著時間而變更。 在抓取此值之後，您應該只在短時間範圍內依賴此值。  |
| productId       | 字串                        | 包含此可用性的[產品](#product)識別碼。           |
| skuId           | 字串                        | 包含此可用性之[SKU](#sku)的識別碼。                   |
| catalogItemId   | 字串                        | 目錄中這個專案的唯一識別碼。 這是購買父系[SKU](#sku)時，必須填入[OrderLineItem. OfferId](order-resources.md#orderlineitem)或[CartLineItem](cart-resources.md#cartlineitem)的識別碼。 **注意**此識別碼會隨著時間而變更。 在抓取此值之後，您應該只在短時間內依賴此值。 它應該只在購買時存取和使用。  |
| defaultCurrency | 字串                        | 此可用性支援的預設貨幣。                               |
| segment         | 字串                        | 此可用性的產業區段。 支援的值為：商業、教育、政府、非贏利。 |
| country         | 字串                                              | 套用此可用性的國家或地區（ISO 國家/地區代碼格式）。 |
| isPurchasable   | bool                                                | 指出此可用性是否為可購買。 |
| isRenewable     | bool                                                | 指出此可用性是否為可續訂。 |
| product      | [基礎](#product)               | 此可用性對應的產品。 |
| sku          | [限量](#sku)            | 此可用性對應的 SKU。 |
| 術語           | [詞彙](#term)資源陣列  | 適用于此可用性的詞彙集合。 |
| 連結           | [ResourceLinks](utility-resources.md#resourcelinks) | 可用性中包含的資源連結。 |

## <a name="term"></a>詞彙

表示可購買可用性的詞彙。

| 屬性              | 類型                                        | 描述                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| duration              | 字串                                      | 詞彙持續時間的 ISO 8601 標記法。 目前支援的值為 P1M （1個月）、P1Y （1年）和 P3Y （3年）。 |
| description           | 字串                                      | 詞彙的描述。           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

表示針對特定目錄專案檢查清查的要求。

| 屬性         | 類型                                                | 描述                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | [InventoryItem](#inventoryitem)的陣列            | 清查檢查將評估的目錄專案清單。                           |
| inventoryCoNtext | 索引鍵/值組                                     | 執行清查檢查所需的內容值字典。 產品的每個[SKU](#sku)都會定義執行此作業所需的值（如果有的話）。  |
| 連結            | [ResourceLinks](utility-resources.md#resourcelinks) | 清查檢查要求中包含的資源連結。                            |

## <a name="inventoryitem"></a>InventoryItem

代表清查檢查作業中的單一專案。 此資源用於指定輸入要求中的目標專案，也用來表示清查檢查作業的輸出結果。

| 屬性         | 類型                                                              | 描述                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | 字串                                                            | 具備[產品](#product)的識別碼。                            |
| skuId            | 字串                                                            | [SKU](#sku)的識別碼。 使用此資源做為清查要求的輸入時，這個值是選擇性的。 如果未提供此值，則會將產品下的所有 Sku 視為清查檢查操作的目標專案。      |
| isRestricted     | bool                                                              | 指出此專案是否有受限制的清查。            |
| 限制     | [InventoryRestriction](#inventoryrestriction)的陣列            | 針對此專案找到之任何限制的詳細資料。 只有在**isRestricted** = "true" 時，才會填入這個屬性。 |

## <a name="inventoryrestriction"></a>InventoryRestriction

表示清查限制的詳細資料。 這僅適用于清查檢查輸出結果，不適用於輸入要求。

| 屬性         | 類型                  | 描述                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | 字串                | 識別限制原因的程式碼。                                    |
| description      | 字串                | 清查限制的描述。                                               |
| properties       | 索引鍵/值組       | 屬性的字典，可提供有關限制的進一步詳細資料。           |

## <a name="billingcycletype"></a>為 billingcycletype

[列舉](https://docs.microsoft.com/dotnet/api/system.enum)值，表示計費週期的類型。

| 值              | 位置     | 說明                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Unknown            | 0            | 列舉初始化運算式。                                                                          |
| 每月            | 1            | 表示合作夥伴將按月計費。                                        |
| 每年             | 2            | 表示合作夥伴將以每年收費。                                       |
| None               | 3            | 表示不會向合作夥伴收取費用。 此值可用於試用專案。    |
| OneTime            | 4            | 表示合作夥伴將會收取一次的費用。                                       |
