---
title: 訂單資源
description: 當客戶想要從供應專案清單購買訂用帳戶時，合作夥伴會進行訂單。
ms.assetid: 5CFA35FF-1C0D-461D-A942-309AFCD98395
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0d6b42414c12c299d9205e6abfa1aadc98fc530e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488268"
---
# <a name="order-resources"></a>訂單資源

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

當客戶想要從供應專案清單購買訂用帳戶時，合作夥伴會進行訂單。

>[!NOTE]
>訂單資源的速率限制為每個租使用者識別碼每分鐘500個要求。

## <a name="order"></a>順序

描述合作夥伴的訂單。

| 屬性           | 類型                                               | 描述                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| id                 | 字串                                             | 成功建立訂單時所提供的訂單識別碼。                                   |
| 替代識別碼        | 字串                                             | 訂單的易記識別碼。                                                                          |
|ReferenceCustomerId | 字串                                             | 客戶識別碼。 |
| billingCycle       | 字串                                             | 指出此訂單的夥伴計費頻率。 支援的值為在[為 billingcycletype](product-resources.md#billingcycletype)中找到的成員名稱。 預設值為「每月」或「OneTime」建立順序。 此欄位會在成功建立訂單時套用。 |
| transactionType    | 字串                                             | 唯讀。 訂單的交易類型。 支援的值為 ' UserPurchase '、' SystemPurchase ' 或 ' SystemBilling ' |
| LineItems          | [OrderLineItem](#orderlineitem)資源的陣列 | 客戶所購買供應專案的詳細清單，包括數量。        |
| currencyCode       | 字串                                             | 唯讀。 放置訂單時使用的貨幣。 已在成功建立訂單時套用。           |
| currencySymbol     | 字串                                             | 唯讀。 貨幣符號 assciated 與貨幣代碼。 |
| CreationDate       | datetime                                           | 唯讀。 訂單的建立日期（採用日期時間格式）。 已在成功建立訂單時套用。                                   |
| status             | 字串                                             | 唯讀。 訂單的狀態。  支援的值為在[**OrderStatus**](#orderstatus)中找到的成員名稱。        |
| 相關              | [OrderLinks](utility-resources.md#resourcelinks)           | 對應至訂單的資源連結。            |
| 屬性         | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至順序的中繼資料屬性。       |

## <a name="orderlineitem"></a>OrderLineItem

訂單包含供應專案的詳細清單，每個專案會以 OrderLineItem 表示。

| 屬性             | 類型                                      | 描述                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| LineItemNumber       | 整數                                       | 集合中的每個明細專案都會取得唯一的行號，從0計算到計數1。                                                                                                                                                 |
| offerId              | 字串                                    | 供應專案的識別碼。                                                                                                                                                                                                                       |
| 訂閱       | 字串                                    | 訂閱的識別碼。                                                                                                                                                                                                                |
| ParentSubscriptionId | 字串                                    | 選用。 附加元件供應專案中父訂用帳戶的識別碼。 僅適用于 PATCH。                                                                                                                                                     |
| friendlyName         | 字串                                    | 選用。 合作夥伴所定義之訂用帳戶的易記名稱，以協助區分。                                                                                                                                              |
| quantity             | 整數                                       | 授權或實例的數目。                                                                                                                                                                                |
| termDuration         | 字串                                    | 詞彙持續時間的 ISO 8601 標記法。 目前支援的值為**P1M** （1個月）、 **P1Y** （1年）和**P3Y** （3年）。                               |
| transactionType      | 字串                                    | 唯讀。 明細專案的交易類型。 支援的值為 [新增]、[更新]、[addQuantity]、[removeQuantity]、[取消]、[轉換] 或 [customerCredit]。 |
| partnerIdOnRecord    | 字串                                    | 當間接提供者代表間接轉銷商下單時，將**僅限間接轉銷**商的 MPN 識別碼填入此欄位（永遠不是間接提供者的識別碼）。 這可確保適當的獎勵會計。 |
| provisioningCoNtext  | 字典 < 字串，字串 >            | 針對目錄中的某些專案布建所需的資訊。 SKU 中的 provisioningVariables 屬性會指出目錄中特定專案所需的屬性。                                                                                                                                               |
| 相關                | [OrderLineItemLinks](#orderlineitemlinks) | 唯讀。 對應至訂單明細專案的資源連結。                                                                                                                                                                                |
| RenewsTo             | 物件的陣列                          | [RenewsTo](#renewsto)資源的陣列。                                                                            |

## <a name="renewsto"></a>RenewsTo

表示訂單明細專案中包含的一個專案。

| 屬性              | 類型             | 必要        | 描述 |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | 字串           | 否              | 續訂詞彙之持續時間的 ISO 8601 標記法。 目前支援的值為**P1M** （1個月）和**P1Y** （1年）。 |

## <a name="orderlinks"></a>OrderLinks

表示對應至訂單的資源連結。

| 屬性           | 類型                                         | 描述                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [連結](utility-resources.md#Link)            | 填入時，用來抓取訂單布建狀態的連結。       |
| 供電               | [連結](utility-resources.md#Link)            | 用來抓取訂單資源的連結。                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

表示與訂單相關聯的完整訂閱。

| 屬性           | 類型                                         | 描述                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [連結](utility-resources.md#Link)            | 填入時，用來抓取行專案布建[狀態](#orderlineitemprovisioningstatus)的連結。       |
| 限量                | [連結](utility-resources.md#Link)            | 用來取得已購買之類別目錄專案之 SKU 資訊的連結。                    |
| 訂閱中       | [連結](utility-resources.md#Link)            | 填入完整訂閱資訊的連結。                       |
| activationLinks    | [連結](utility-resources.md#Link)            | 填入時，為啟動訂閱的連結取得資源。             |

## <a name="orderstatus"></a>OrderStatus

具有值的[列舉](https://docs.microsoft.com/dotnet/api/system.enum)，指出訂單的狀態。

| 值              | 位置     | 描述                                     |
|--------------------|--------------|-------------------------------------------------|
| unknown            | 0            | 列舉初始化運算式。                               |
| 好          | 1            | 表示訂單已完成。          |
| 正在            | 2            | 表示訂單仍待決。      |
| 取消          | 3            | 表示已取消訂單。    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

表示[OrderLineItem](#orderlineitem)的布建狀態。

| 屬性                        | 類型                                | 描述                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| LineItemNumber                  | 整數                                 | 訂單明細專案的唯一行號。 值的範圍從0到計數-1。             |
| status                          | 字串                              | 訂單明細專案的布建狀態。 值包括：</br>「已滿足」：訂單的履行成功完成，使用者將能夠使用保留專案</br>「未執行」：因取消而未完成</br>"PrefulfillmentPending"：您的要求仍在處理中，履行尚未完成 |
| quantityProvisioningInformation | 列出 <[QuantityProvisioningStatus](#quantityprovisioningstatus)> | 訂單明細專案的數量布建狀態資訊清單。 |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

代表依數量的布建狀態。

| 屬性                           | 類型                                         | 描述                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | 整數                                          | 專案的數目。                                 |
| status                             | 字串                                       | 專案數的狀態。                   |
