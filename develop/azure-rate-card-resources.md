---
title: Azure 費率卡片資源
description: Azure 費率卡片提供 Azure 供應專案的即時價格。
ms.assetid: A42B4FFA-278E-41FF-B51E-E48C2CA70EEF
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 993489f553e0353b7b53a5c707fc69fff169b08a
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413196"
---
# <a name="azure-rate-card-resources"></a>Azure 費率卡片資源

適用於：

- 夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

Azure 費率卡片提供 Azure 供應專案的即時價格。 Azure 定價非常動態，而且經常變動。 Microsoft 會在合作夥伴中心發佈更新，但 REST API 提供最快的方式讓雲端解決方案提供者合作夥伴取得目前的價格。

若要追蹤使用方式並協助預測個別客戶的每月帳單和帳單，您可以結合費率卡片查詢以[取得 Microsoft Azure 的價格](get-prices-for-microsoft-azure.md)，取得[客戶的 Azure 使用量記錄](get-a-customer-s-utilization-record-for-azure.md)要求。

價格會依市場和貨幣而有所不同，而此 API 會將位置納入考慮。 根據預設，它會在合作夥伴中心和您的瀏覽器語言中使用您的夥伴設定檔設定，但可自訂。 如果您從單一的集中式辦公室管理多個市場的銷售，這就特別相關。

## <a name="azureratecard"></a>AzureRateCard

說明 Azure 費率卡片資源的屬性。

| 屬性      | 類型                                      | 描述                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| 貨幣      | string                                    | 提供費率的貨幣。                     |
| isTaxIncluded | 布林值                                   | 所有費率皆為稅前，因此一律會以 "false" 的形式傳回。 |
| 語言        | string                                    | 當地語系化資源資訊的文化特性。       |
| 計量        | 物件的陣列                          | [AzureMeter](#azuremeter)物件的陣列。                       |
| offerTerms    | 物件的陣列                          | [AzureOfferTerm](#azureofferterm)物件的陣列。               |
| 屬性    | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。 包含 "objectType"： "AzureRateCard"   |


### <a name="operations-on-the-azureratecard-resource"></a>AzureRateCard 資源上的作業

- [取得 Microsoft Azure 定價](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| 屬性         | 類型             | 描述                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | string           | 計量的唯一識別碼。                                                                    |
| 名稱             | string           | 計量的易記名稱。                                                                   |
| 效率            | object           | 計量費率。 索引鍵是計量數量（字串），而值則是計量速率（數位）。 |
| tags             | 字串的陣列 | 選擇性的計量標記。 此陣列可以是空的。                                                 |
| category         | string           | 資源的類別。                                                                     |
| 分類      | string           | 資源的子類別。                                                                 |
| 區內           | string           | 識別碼的區域。                                                                             |
| 單位             | string           | 數量的類型（小時、位元組等）                                                     |
| includedQuantity | 數字           | 免費包含的計量數量。                                               |
| effectiveDate    | string           | 此計量生效的日期。                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| 屬性         | 類型             | 描述                             |
|------------------|------------------|-----------------------------------------|
| 名稱             | string           | 供應專案詞彙的易記名稱。        |
| 貼現         | 數字           | 已套用的折扣（如果有的話）。           |
| excludedMeterIds | 字串的陣列 | 從供應專案排除的計量（如果有的話）。 |
| effectiveDate    | string           | 供應專案生效的日期。        |