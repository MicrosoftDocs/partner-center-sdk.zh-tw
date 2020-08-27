---
title: 購物車資源
description: 當客戶想要從供應專案清單購買訂用帳戶時，合作夥伴會在購物車中放入訂單。
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3aea428064654077ae67974132ec05918edfee65
ms.sourcegitcommit: a8fe6268fed2162843e7c92dca41c3919b25647d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/26/2020
ms.locfileid: "88937888"
---
# <a name="cart-resources"></a>購物車資源

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

當客戶想要從供應專案清單購買訂用帳戶時，合作夥伴會進行訂單。

## <a name="cart"></a>購物車

描述購物車。

| 屬性              | 類型             | 描述                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | 字串           | 成功建立購物車時所提供的購物車識別碼。                               |
| creationTimeStamp     | Datetime         | 購物車的建立日期（以日期時間格式）。 在成功建立購物車時申請。      |
| lastModifiedTimeStamp | Datetime         | 購物車上次更新的日期（以日期時間格式）。 在成功建立購物車時申請。 |
| expirationTimeStamp   | Datetime         | 購物車將到期的日期（以日期時間格式）。 在成功建立購物車時申請。          |
| lastModifiedUser      | 字串           | 上次更新購物車的使用者。 在成功建立購物車時申請。                          |
| lineItems             | 物件的陣列 | [CartLineItem](#cartlineitem)資源的陣列。                                                   |
| status                | 字串           | 購物車的狀態。 可能的值為「作用中」 (可以更新/提交) 和「已排序」 (已經) 提交。 |

## <a name="cartlineitem"></a>CartLineItem

代表購物車中包含的一個專案。

| 屬性             | 類型                             | 描述                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | 字串                           | 購物車明細專案的唯一識別碼。 在成功建立購物車時申請。                                                                   |
| catalogItemId        | 字串                           | 目錄專案識別碼。                                                                                                                          |
| friendlyName         | 字串                           | 選擇性。 由夥伴定義之專案的易記名稱，以協助區分。                                                                 |
| quantity             | int                              | 授權或實例的數目。                                                                                                                  |
| currencyCode         | 字串                           | 貨幣代碼。                                                                                                                                    |
| billingCycle         | Object                           | 針對目前期間設定的計費週期類型。                                                                                                 |
| termDuration         | 字串                           | 期限的 ISO 8601 標記法。 目前支援的值為 P1M (1 個月) 、P1Y (1 年) 和 P3Y (3 年) 。                                |
| 參與者         | 物件字串組的清單      | PartnerId on Record 的集合，會在購買時) 記錄 (MPNID。                                                                                          |
| provisioningCoNtext  | 字典<字串，字串>       | 布建購買的專案時所使用的其他內容。 若要判斷特定專案需要哪些值，請參閱 SKU 的 provisioningVariables 屬性。 |
| orderGroup           | 字串                           | 用來指出哪些專案可以依相同順序提交的群組。                                                                          |
| addonItems           | **CartLineItem**物件的清單 | 附加元件購物車明細專案的集合。 這些專案將會針對由根購物車明細專案購買所產生的基本訂用帳戶購買。 |
| error                | Object                           | 如果發生錯誤，則在建立購物車之後套用。                                                                                                    |
| renewsTo             | 物件的陣列                 | [RenewsTo](#renewsto)資源的陣列。                                                                            |

## <a name="renewsto"></a>RenewsTo

代表購物車明細專案中包含的一個專案。

| 屬性              | 類型             | 必要        | 描述 |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | 字串           | No              | 續訂期限的持續時間的 ISO 8601 標記法。 目前支援的值會 **P1M** (1 個月) ，而 **P1Y** (1 年) 。 |

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱 [合作夥伴中心錯誤碼](error-codes.md)。

## <a name="carterror"></a>CartError

表示在購物車建立之後發生的錯誤。

| 屬性         | 類型                                   | 描述                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [合作夥伴中心錯誤碼](error-codes.md) | 購物車錯誤的類型。                                                                       |
| errorDescription | 字串                                 | 錯誤描述，包括有關支援的值、預設值或限制的任何附注。 |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

代表購物車結帳的結果。

| 屬性    | 類型                                              | 描述                     |
|-------------|---------------------------------------------------|---------------------------------|
| 訂單      | [Order](order-resources.md#order)物件的清單。         | 訂單的集合。       |
| orderErrors | [OrderError](#ordererror)物件的清單。 | 訂單錯誤的集合。 |

## <a name="ordererror"></a>OrderError

表示在建立訂單時，購物車簽出期間發生的錯誤。

| 屬性     | 類型   | 描述                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | 字串 | 具有錯誤之訂單的訂單群組識別碼。 |
| code         | int    | 錯誤碼。                                 |
| description  | 字串 | 錯誤的描述。                   |
