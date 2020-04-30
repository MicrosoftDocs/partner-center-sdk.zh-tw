---
title: 服務成本資源
description: 描述與客戶購買之服務相關的資源。
ms.assetid: 2916B7F3-06D5-4DC1-A137-CD8270258CDB
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e61ef7e2d6c72938a365d28774a90b993c5d3e7b
ms.sourcegitcommit: 59ac8346af04aa34f5d342002909d0b203654bfe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81666301"
---
# <a name="service-costs-resources"></a>服務成本資源

**適用於：**

- 合作夥伴中心

描述與客戶購買之服務相關的資源。

## <a name="servicecostssummary"></a>ServiceCostsSummary

**ServiceCostsSummary**包含摘要，可匯總指定客戶在計費期間所購買的所有服務。

| 屬性 | 類型 | 描述 |
| -------- | ---- | ----------- |
| 詳細資料 | [ServiceCostsSummaryDetail](#servicecostssummarydetail)物件的陣列 | 服務成本摘要詳細資料清單，以發票類型區分。|
| 連結 | [ResourceLinks](utility-resources.md#resourcelinks) | 資源連結。 |
| 屬性 | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。 |

> [!IMPORTANT]
> **下表中的欄位已被取代。** 若要取出週期性和一次性服務成本摘要，請改用 [**詳細資料**] 欄位。 [**詳細資料**] 欄位會在上表中說明。 請參閱**details**欄位對應的資料值，但不參考根層級的欄位。

| 屬性 | 類型 | 描述 |
| -------- | ---- | ----------- |
| billingStartDate | date | 計費週期的開始。 |
| billingEndDate | date | 計費週期結束。 |
| pretaxTotal | double | 客戶所有成本的預先稅總計。 |
| tax  | double | 客戶購買的所有專案所產生的總稅額。 |
| afterTaxTotal | double | 客戶購買之所有專案的淨總成本。 |
| currencyCode | 字串 | 代表成本所使用的貨幣。 |
| currencySymbol | 字串 | 成本所使用的貨幣符號。 |
| customerId | 字串 | 進行購買之客戶的識別碼。 |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**ServiceCostsSummaryDetail**描述的服務成本摘要會匯總指定客戶在計費期間（從週期性或一次性發票）購買的所有服務。

| 屬性 | 類型 | 描述 |
| -------- | ---- | ----------- |
| invoiceType | 字串 | 已產生「服務成本摘要」的 invoiceType。 |
| summary | [ServiceCostsSummary](#servicecostssummary) | 客戶在一個發票類型下匯總的服務成本摘要。 |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**ServiceCostLineItem**描述客戶所購買的單一專案。

> [!IMPORTANT]
> 下列屬性*僅適用于*產品為*一次性購買*的服務成本明細專案： **productId**、 **productName**、 **skuId**、 **skuName**、 **availabilityId**、 **publisherId**、 **publisherName**、 **termAndBillingCycle**、 **discountDetails**。 這些屬性不適*用於*產品為*週期性購買*的服務明細專案。 例如，這些屬性*不適*用於以訂用帳戶為基礎的 Office 365 和 Azure。

| 屬性                 | 類型                           | 描述                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| startDate                | UTC 日期時間格式的字串 | 費用的開始日期。                                       |
| endDate                  | UTC 日期時間格式的字串 | 費用的結束日期。                                         |
| subscriptionFriendlyName | 字串                         | 訂用帳戶的易記名稱。                              |
| subscriptionId           | 字串                         | 訂用帳戶識別碼。                                         |
| orderId                  | 字串                         | 訂單識別碼。                                                |
| offerId                  | 字串                         | 供應項目識別碼。                                                |
| offerName                | 字串                         | 供應專案名稱。                                                      |
| resellerMPNId            | 字串                         | 僅用於2層合作夥伴案例。 參考 MPN 識別碼。 |
| chargeType               | 字串                         | 相關聯的收費類型。                                          |
| quantity                 | number                         | 使用或購買的單位數量。                             |
| unitPrice                | number                         | 每個單位的價格。                                                  |
| pretaxTotal              | number                         | 此專案在稅金之前的總費用。                         |
| tax                      | number                         | 此專案產生的總稅金費用。                         |
| afterTaxTotal            | number                         | 此專案的淨總成本。                                    |
| currencyCode             | 字串                         | 代表成本所使用的貨幣。                          |
| currencySymbol           | 字串                         | 成本所使用的貨幣符號。                              |
| customerId               | 字串                         | 進行購買之客戶的識別碼。                          |
| customerName             | 字串                         | 進行購買的客戶名稱。                        |
| invoiceNumber            | 字串                         | 這個明細專案所屬的發票號碼。                   |
| productId                | 字串                         | 產品識別碼。                                              |
| skuId                    | 字串                         | Sku 識別碼。                                                  |
| availabilityId           | 字串                         | 可用性識別碼。                                         |
| productName              | 字串                         | 產品名稱。                                                    |
| skuName                  | 字串                         | Sku 名稱。                                                        |
| publisherName            | 字串                         | 發行者名稱。                                                  |
| publisherId              | 字串                         | 發行者識別碼。                                            |
| termAndBillingCycle      | 字串                         | 詞彙和計費週期。                                          |
| discountDetails          | 字串                         | 折扣詳細資料。                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| 屬性             | 類型                               | 描述                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [連結](utility-resources.md#link) | 要取出明細專案的 URI。 |
| self                 | [連結](utility-resources.md#link) | 自我 URI。                       |
