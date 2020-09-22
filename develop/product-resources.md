---
title: 產品資源
description: 代表可購買商品或服務的資源。 包含用來描述產品類型和圖形 (SKU) 的資源，以及在清查中檢查產品可用性的資源。
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6a3cfacd3654e85a9824759295f97792ff740d85
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925847"
---
# <a name="products-resources"></a>產品資源

**適用於**

- 合作夥伴中心

代表可購買商品或服務的資源。 包含用來描述產品類型和圖形 (SKU) 的資源，以及在清查中檢查產品可用性的資源。

## <a name="product"></a>產品

代表可購買良好或服務。 產品本身並不是可購買專案。

| 屬性           | 類型                          | 描述                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| id                 | 字串                        | 此產品的識別碼。                                                 |
| title              | 字串                        | 產品標題。                                                       |
| description        | 字串                        | 產品描述。                                                 |
| productType        | [ItemType](#itemtype)         | 描述此產品)  (s 類型分類的物件。     |
| isMicrosoftProduct | bool                          | 指出這是否為 Microsoft 產品。                          |
| publisherName      | 字串                        | 產品發行者的名稱（如果有的話）。                          |
| 連結              | [ProductLinks](#productlinks) | 產品中包含的資源連結。                         |

## <a name="itemtype"></a>ItemType

表示產品的類型。

| 屬性        | 類型                          | 描述                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | 字串                        | 類型識別碼。                                                                 |
| displayName     | 字串                        | 此類型的顯示名稱。                                                      |
| 亞         | [ItemType](#itemtype)         | 選擇性。 物件，描述此專案類型的子類型分類。     |

## <a name="productlinks"></a>ProductLinks

包含 [產品](#product)連結的清單。

| 屬性        | 類型                                                          | 描述                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| sku            | [連結](utility-resources.md#link)                             | 用來存取基礎 Sku 的連結。          |
| 連結           | [ResourceLinks](utility-resources.md#resourcelinks)           | 此資源內包含的資源連結。   |

## <a name="sku"></a>SKU

代表產品下 (SKU) 的可購買庫存單位。 這些代表產品的不同形狀。

| 屬性               | 類型             | 描述                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| id                     | 字串           | 此 SKU 的識別碼。 此識別碼只在其父產品的內容中是唯一的。 |
| title                  | 字串           | SKU 的標題。                                                                 |
| description            | 字串           | SKU 的描述。                                                           |
| productId              | 字串           | 包含此 SKU 之父 [產品](#product) 的識別碼。                      |
| minimumQuantity        | int              | 允許購買的最小數量。                                            |
| maximumQuantity        | int              | 允許購買的最大數量。                                            |
| isTrial                | bool             | 指出此 SKU 是否為試用專案。                                           |
| supportedBillingCycles | 字串陣列 | 此 SKU 支援的計費週期清單。 支援的值為在 [BillingCycleType](#billingcycletype) 中找到的成員名稱。 |
| purchasePrerequisites  | 字串陣列 | 購買此專案之前所需的先決條件步驟或動作清單。 支援的值為：<br/>  "InventoryCheck"-表示應先評估專案的清查，再嘗試購買此專案。<br/> "AzureSubscriptionRegistration"-表示需要 Azure 訂用帳戶，而且必須在嘗試購買此專案之前註冊。  |
| inventoryVariables     | 字串陣列 | 在此專案上執行清查檢查所需的變數清單。 支援的值為：<br/> "CustomerId"-購買的客戶識別碼。<br/> "AzureSubscriptionId"-將用於 Azure 保留購買的 Azure 訂用帳戶識別碼。</br> "ArmRegionName"-要驗證清查的區域。 此值必須符合 SKU DynamicAttributes 中的 "ArmRegionName"。 |
| provisioningVariables  | 字串陣列 | 購買此專案時，必須提供至 [購物車明細專案](cart-resources.md#cartlineitem) 的布建內容中的變數清單。 支援的值為：<br/> 範圍-Azure 保留購買的範圍：「單一」、「共用」。<br/> 「SubscriptionId」-azure 訂用帳戶的識別碼，此訂用帳戶將用於購買 Azure 保留。<br/> 「持續時間」-Azure 保留的持續時間： "1Year"、"3Year"。  |
| dynamicAttributes      | 成對的索引鍵/值  | 適用于這個專案的動態屬性字典。 請注意，此字典中的屬性是動態的，而且可以變更而不另行通知。 您不應該針對此屬性值中現有的特定索引鍵建立強式相依性。    |
| 連結                  | [ResourceLinks](utility-resources.md#resourcelinks) | 包含在 SKU 中的資源連結。                   |

## <a name="availability"></a>可用性

代表可供購買 (的 SKU，例如國家/地區、貨幣和產業區段) 。

| 屬性        | 類型                        | 描述                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| id              | 字串                        | 此可用性的識別碼。 只有在其父 [產品](#product) 和 [SKU](#sku)的內容中，此識別碼是唯一的。 **注意** 此識別碼會隨著時間而變更。 在抓取此值之後，您應該只會在短時間範圍內依賴此值。  |
| productId       | 字串                        | 包含此可用性之 [產品](#product) 的識別碼。           |
| skuId           | 字串                        | 包含此可用性的 [SKU](#sku) 識別碼。                   |
| catalogItemId   | 字串                        | 目錄中這個專案的唯一識別碼。 這是在購買父[SKU](#sku)時，必須填入[>orderlineitem. OfferId](order-resources.md#orderlineitem)或[CARTLINEITEM. CatalogItemId](cart-resources.md#cartlineitem)屬性的識別碼。 **注意** 此識別碼會隨著時間而變更。 在抓取此值之後，您應該只會在短時間內依賴此值。 它應該只在購買時存取及使用。  |
| defaultCurrency | 字串                        | 此可用性支援的預設貨幣。                               |
| segment         | 字串                        | 此可用性的產業區段。 支援的值為：商業、教育、政府、非贏利。 |
| country         | 字串                                              | 國家或地區 (的 ISO 國家/地區代碼格式) 此可用性適用的位置。 |
| isPurchasable   | bool                                                | 指出此可用性是否可購買。 |
| isRenewable     | bool                                                | 指出此可用性是否可再生。 |
| product      | [產品](#product)               | 此可用性所對應的產品。 |
| sku          | [Sku](#sku)            | 此可用性對應的 SKU。 |
| terms           | [詞彙](#term)資源陣列  | 適用于此可用性的條款集合。 |
| 連結           | [ResourceLinks](utility-resources.md#resourcelinks) | 可用性內所含的資源連結。 |

## <a name="term"></a>詞彙

代表可購買可用性的詞彙。

| 屬性              | 類型                                        | 描述                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| duration              | 字串                                      | 期限的 ISO 8601 標記法。 目前支援的值為 P1M (1 個月) 、P1Y (1 年) 和 P3Y (3 年) 。 |
| description           | 字串                                      | 詞彙的描述。           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

表示針對特定類別目錄專案檢查清查的要求。

| 屬性         | 類型                                                | 描述                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | [InventoryItem](#inventoryitem)的陣列            | 清查檢查將評估的類別目錄專案清單。                           |
| inventoryCoNtext | 成對的索引鍵/值                                     |  (s) 執行清查檢查所需的內容值字典。 如果需要任何) 來執行這項作業，產品的每個 [SKU](#sku) 都會定義 (的值。  |
| 連結            | [ResourceLinks](utility-resources.md#resourcelinks) | 清查檢查要求內所含的資源連結。                            |

## <a name="inventoryitem"></a>InventoryItem

代表清查檢查作業中的單一專案。 此資源是用來指定輸入要求中的目標專案，也用來代表清查檢查作業的輸出結果。

| 屬性         | 類型                                                              | 描述                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | 字串                                                            | 需要 ([產品](#product)的識別碼) 。                            |
| skuId            | 字串                                                            | [SKU](#sku)的識別碼。 使用此資源做為清查要求的輸入時，此值是選擇性的。 如果未提供此值，則會將產品下的所有 Sku 視為清查檢查作業的目標專案。      |
| isRestricted     | bool                                                              | 指出是否找到此專案有受限制的清查。            |
| 限制     | [InventoryRestriction](#inventoryrestriction)的陣列            | 針對此專案找到之任何限制的詳細資料。 只有在 **isRestricted** = "true" 時，才會填入這個屬性。 |

## <a name="inventoryrestriction"></a>InventoryRestriction

代表清查限制的詳細資料。 這僅適用于清查檢查輸出結果，而非輸入要求。

| 屬性         | 類型                  | 描述                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | 字串                | 識別限制原因的程式碼。                                    |
| description      | 字串                | 清查限制的描述。                                               |
| properties       | 成對的索引鍵/值       | 屬性的字典，可提供有關限制的進一步詳細資料。           |

## <a name="billingcycletype"></a>>billingcycletype

[Enum/dotnet/api/system.string) 具有指出計費週期類型的值。

| 值              | 位置     | 描述                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Unknown            | 0            | 列舉初始化運算式。                                                                          |
| 每月            | 1            | 指出夥伴將按月計費。                                        |
| 每年             | 2            | 指出將每年向夥伴收費。                                       |
| 無               | 3            | 表示不會向夥伴收費。 此值可用於試用專案。    |
| 一次性            | 4            | 表示夥伴將會收取一次的費用。                                       |
