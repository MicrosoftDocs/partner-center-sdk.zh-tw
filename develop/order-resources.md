---
title: 訂單資源
description: 當客戶想要從供應專案清單購買訂用帳戶時，合作夥伴會進行訂單。
ms.assetid: 5CFA35FF-1C0D-461D-A942-309AFCD98395
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 13ea0368e257f437494f97979be7dd0a48efe4fa
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416438"
---
# <a name="order-resources"></a>訂單資源

適用於：

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

當客戶想要從供應專案清單購買訂用帳戶時，合作夥伴會進行訂單。

>[!NOTE]
>訂單資源的速率限制為每個租使用者識別碼每分鐘500個要求。

## <a name="order"></a>使用

描述合作夥伴的訂單。

| 屬性           | 類型                                               | 描述                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| id                 | string                                             | 成功建立訂單時所提供的訂單識別碼。                                   |
| 替代識別碼        | string                                             | 訂單的易記識別碼。                                                                          |
|referenceCustomerId | string                                             | 客戶識別碼。 |
| BillingCycle       | string                                             | 指出此訂單的夥伴計費頻率。 支援的值為在[為 billingcycletype](product-resources.md#billingcycletype)中找到的成員名稱。 預設值為「每月」或「OneTime」建立順序。 此欄位會在成功建立訂單時套用。 |
| transactionType    | string                                             | 唯讀。 訂單的交易類型。 支援的值為 ' UserPurchase '、' SystemPurchase ' 或 ' SystemBilling ' |
| lineItems          | [OrderLineItem](#orderlineitem)資源的陣列 | 客戶所購買供應專案的詳細清單，包括數量。        |
| currencyCode       | string                                             | 唯讀。 放置訂單時使用的貨幣。 已在成功建立訂單時套用。           |
| currencySymbol     | string                                             | 唯讀。 貨幣符號 assciated 與貨幣代碼。 |
| creationDate       | datetime                                           | 唯讀。 訂單的建立日期（採用日期時間格式）。 已在成功建立訂單時套用。                                   |
| status             | string                                             | 唯讀。 訂單的狀態。  支援的值為在[**OrderStatus**](#orderstatus)中找到的成員名稱。        |
| 連結              | [OrderLinks](utility-resources.md#resourcelinks)           | 對應至訂單的資源連結。            |
| 屬性         | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至順序的中繼資料屬性。       |

## <a name="orderlineitem"></a>OrderLineItem

訂單包含供應專案的詳細清單，每個專案會以 OrderLineItem 表示。

| 屬性             | 類型                                      | 描述                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int                                       | 集合中的每個明細專案都會取得唯一的行號，從0計算到計數1。                                                                                                                                                 |
| offerId              | string                                    | 供應專案的識別碼。                                                                                                                                                                                                                       |
| subscriptionId       | string                                    | 訂閱的識別碼。                                                                                                                                                                                                                |
| parentSubscriptionId | string                                    | 選擇性。 附加元件供應專案中父訂用帳戶的識別碼。 僅適用于 PATCH。                                                                                                                                                     |
| friendlyName         | string                                    | 選擇性。 合作夥伴所定義之訂用帳戶的易記名稱，以協助區分。                                                                                                                                              |
| quantity             | int                                       | 授權或實例的數目。                                                                                                                                                                                |
| termDuration         | string                                    | 詞彙持續時間的 ISO 8601 標記法。 目前支援的值為**P1M** （1個月）、 **P1Y** （1年）和**P3Y** （3年）。                               |
| transactionType      | string                                    | 唯讀。 明細專案的交易類型。 支援的值為 [新增]、[更新]、[addQuantity]、[removeQuantity]、[取消]、[轉換] 或 [customerCredit]。 |
| partnerIdOnRecord    | string                                    | 當間接提供者代表間接轉銷商下單時，將**僅限間接轉銷**商的 MPN 識別碼填入此欄位（永遠不是間接提供者的識別碼）。 這可確保適當的獎勵會計。 |
| provisioningCoNtext  | 字典 < 字串，字串 >            | 針對目錄中的某些專案布建所需的資訊。 SKU 中的 provisioningVariables 屬性會指出目錄中特定專案所需的屬性。                                                                                                                                               |
| 連結                | [OrderLineItemLinks](#orderlineitemlinks) | 唯讀。 對應至訂單明細專案的資源連結。                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |續約詞彙的持續時間詳細資料。                                                                           |

## <a name="renewsto"></a>renewsTo

表示續約詞彙的持續時間詳細資料。

| 屬性              | 類型             | 必要項        | 描述 |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | string           | 否              | 續訂詞彙之持續時間的 ISO 8601 標記法。 目前支援的值為**P1M** （1個月）和**P1Y** （1年）。 |

## <a name="orderlinks"></a>OrderLinks

表示對應至訂單的資源連結。

| 屬性           | 類型                                         | 描述                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [連結](utility-resources.md#Link)            | 填入時，用來抓取訂單布建狀態的連結。       |
| self               | [連結](utility-resources.md#Link)            | 用來抓取訂單資源的連結。                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

表示與訂單相關聯的完整訂閱。

| 屬性           | 類型                                         | 描述                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [連結](utility-resources.md#Link)            | 填入時，用來抓取行專案布建[狀態](#orderlineitemprovisioningstatus)的連結。       |
| sku                | [連結](utility-resources.md#Link)            | 用來取得已購買之類別目錄專案之 SKU 資訊的連結。                    |
| 訂閱中       | [連結](utility-resources.md#Link)            | 填入完整訂閱資訊的連結。                       |
| activationLinks    | [連結](utility-resources.md#Link)            | 填入時，為啟動訂閱的連結取得資源。             |

## <a name="orderstatus"></a>OrderStatus

具有值的[列舉](https://docs.microsoft.com/dotnet/api/system.enum)，指出訂單的狀態。

| 值              | Position     | 描述                                     |
|--------------------|--------------|-------------------------------------------------|
| 不明            | 0            | 列舉初始化運算式。                               |
| 已完成          | 1            | 表示訂單已完成。          |
| 暫止            | 2            | 表示訂單仍待決。      |
| 取消          | 3            | 表示已取消訂單。    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

表示[OrderLineItem](#orderlineitem)的布建狀態。

| 屬性                        | 類型                                | 描述                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber                  | int                                 | 訂單明細專案的唯一行號。 值的範圍從0到計數-1。             |
| status                          | string                              | 訂單明細專案的布建狀態。 值包括：</br>「已滿足」：訂單的履行成功完成，使用者將能夠使用保留專案</br>「未執行」：因取消而未完成</br>"PrefulfillmentPending"：您的要求仍在處理中，履行尚未完成 |
| quantityProvisioningInformation | 列出 <[QuantityProvisioningStatus](#quantityprovisioningstatus)> | 訂單明細專案的數量布建狀態資訊清單。 |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

代表依數量的布建狀態。

| 屬性                           | 類型                                         | 描述                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | int                                          | 項目數目。                                 |
| status                             | string                                       | 專案數的狀態。                   |
