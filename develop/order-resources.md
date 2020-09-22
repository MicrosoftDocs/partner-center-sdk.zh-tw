---
title: 訂購資源
description: 當客戶想要從供應專案清單購買訂用帳戶時，合作夥伴會進行訂單。
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9db07337a98214b4aaa93e2c8b43b84702249b77
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925877"
---
# <a name="order-resources"></a>訂購資源

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

當客戶想要從供應專案清單購買訂用帳戶時，合作夥伴會進行訂單。

>[!NOTE]
>訂單資源的速率限制為每分鐘每個租使用者識別碼500個要求。

## <a name="order"></a>單

描述夥伴的訂單。

| 屬性           | 類型                                               | 描述                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| id                 | 字串                                             | 成功建立訂單時提供的訂單識別碼。                                   |
| 替代識別碼        | 字串                                             | 訂單的易記識別碼。                                                                          |
|referenceCustomerId | 字串                                             | 客戶識別碼。 |
| billingCycle       | 字串                                             | 指出夥伴針對此訂單計費的頻率。 支援的值為在 [BillingCycleType](product-resources.md#billingcycletype) 中找到的成員名稱。 預設值為「每月」或「OneTime」（依順序建立）。 此欄位會在成功建立訂單時套用。 |
| transactionType    | 字串                                             | 唯讀。 訂單的交易類型。 支援的值為 ' UserPurchase '、' SystemPurchase ' 或 ' SystemBilling ' |
| lineItems          | [>orderlineitem](#orderlineitem)資源的陣列 | 客戶所購買供應專案的詳細清單，包括數量。        |
| currencyCode       | 字串                                             | 唯讀。 放置訂單時使用的貨幣。 在成功建立訂單時套用。           |
| currencySymbol     | 字串                                             | 唯讀。 與貨幣代碼相關聯的貨幣符號。 |
| creationDate       | Datetime                                           | 唯讀。 訂單的建立日期 (採用日期-時間格式)。 在成功建立訂單時套用。                                   |
| status             | 字串                                             | 唯讀。 訂單的狀態。  支援的值是在 [**OrderStatus**](#orderstatus)中找到的成員名稱。        |
| 連結              | [OrderLinks](utility-resources.md#resourcelinks)           | 對應至訂單的資源連結。            |
| 屬性         | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至順序的中繼資料屬性。       |

## <a name="orderlineitem"></a>OrderLineItem

訂單包含供應專案的詳細清單，而每個專案會以 >orderlineitem 表示。

| 屬性             | 類型                                      | 描述                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int                                       | 集合中的每個明細項目都會取得唯一的行號 (從 0 數到 count-1)。                                                                                                                                                 |
| offerId              | 字串                                    | 供應專案的識別碼。                                                                                                                                                                                                                       |
| subscriptionId       | 字串                                    | 訂閱的識別碼。                                                                                                                                                                                                                |
| parentSubscriptionId | 字串                                    | 選擇性。 附加供應項目中父訂用帳戶的識別碼。 僅適用於 PATCH。                                                                                                                                                     |
| friendlyName         | 字串                                    | 選擇性。 由夥伴定義之訂用帳戶的易記名稱，以協助區分。                                                                                                                                              |
| quantity             | int                                       | 授權或實例的數目。                                                                                                                                                                                |
| termDuration         | 字串                                    | 期限的 ISO 8601 標記法。 目前支援的值為 **P1M** (1 個月) 、 **P1Y** (1 年) 和 **P3Y** (3 年) 。                               |
| transactionType      | 字串                                    | 唯讀。 明細專案的交易類型。 支援的值為「new」、「更新」、「addQuantity」、「removeQuantity」、「取消」、「轉換」或「customerCredit」。 |
| partnerIdOnRecord    | 字串                                    | 當間接提供者代表間接轉銷商進行訂單時，請使用 **間接轉銷** 商的 MPN 識別碼填入此欄位， (永遠不會) 間接提供者的識別碼。 這可確保適度的獎勵。 |
| provisioningCoNtext  | 字典<字串，字串>            | 針對目錄中的某些專案布建所需的資訊。 SKU 中的 provisioningVariables 屬性會指出目錄中的特定專案需要哪些屬性。                                                                                                                                               |
| 連結                | [OrderLineItemLinks](#orderlineitemlinks) | 唯讀。 對應至訂單明細專案的資源連結。                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |續約詞彙持續時間詳細資料。                                                                           |

## <a name="renewsto"></a>RenewsTo

代表續約詞彙的持續時間詳細資料。

| 屬性              | 類型             | 必要        | 描述 |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | 字串           | No              | 續訂期限的持續時間的 ISO 8601 標記法。 目前支援的值會 **P1M** (1 個月) ，而 **P1Y** (1 年) 。 |

## <a name="orderlinks"></a>OrderLinks

表示對應至訂單的資源連結。

| 屬性           | 類型                                         | 描述                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [連結](utility-resources.md#link)            | 填入時，用來取得訂單之布建狀態的連結。       |
| self               | [連結](utility-resources.md#link)            | 用來取得訂單資源的連結。                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

表示與訂單相關聯的完整訂閱。

| 屬性           | 類型                                         | 描述                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [連結](utility-resources.md#link)            | 填入時，用來取得明細專案布建 [狀態](#orderlineitemprovisioningstatus) 的連結。       |
| sku                | [連結](utility-resources.md#link)            | 用來取得所購買之類別目錄專案的 SKU 資訊的連結。                    |
| 訂用帳戶       | [連結](utility-resources.md#link)            | 填入時，為完整訂用帳戶資訊的連結。                       |
| activationLinks    | [連結](utility-resources.md#link)            | 填入時，取得用來啟動訂用帳戶之連結的資源。             |

## <a name="orderstatus"></a>OrderStatus

[Enum/dotnet/api/system.string) ，其值會指出順序的狀態。

| 值              | 位置     | 描述                                     |
|--------------------|--------------|-------------------------------------------------|
| 未知            | 0            | 列舉初始化運算式。                               |
| 完成          | 1            | 指出訂單已完成。          |
| 暫止            | 2            | 指出訂單仍處於暫止狀態。      |
| 取消          | 3            | 指出訂單已取消。    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

代表 [>orderlineitem](#orderlineitem)的布建狀態。

| 屬性                        | 類型                                | 描述                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber                  | int                                 | 訂單明細專案的唯一行號。 值的範圍從0到計數-1。             |
| status                          | 字串                              | 訂單明細專案的布建狀態。 數值包括：</br>「已完成」：訂單的履行成功完成，且使用者將能夠使用保留</br>「未完成」：因取消而未完成</br>"PrefulfillmentPending"：您的要求仍在處理中，履行尚未完成 |
| quantityProvisioningInformation | 列出<[QuantityProvisioningStatus](#quantityprovisioningstatus)> | 訂單明細專案的數量布建狀態資訊清單。 |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

代表依數量的布建狀態。

| 屬性                           | 類型                                         | 描述                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | int                                          | 項目的數目。                                 |
| status                             | 字串                                       | 專案數目的狀態。                   |
