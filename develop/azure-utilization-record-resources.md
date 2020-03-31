---
title: Azure 使用率記錄資源
description: Azure 使用率記錄包含 Azure 訂用帳戶資源使用量的詳細資料。
ms.assetid: 4C1EEEB3-DB25-4D61-BFED-C4AB5D3BB5CF
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: afe4b00109c1c5058e062281a721fb8f1117b926
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413125"
---
# <a name="azure-utilization-record-resources"></a>Azure 使用率記錄資源

適用於：

- 夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

Azure 使用率記錄包含 Azure 訂用帳戶資源使用量的詳細資料。 如果您是雲端服務提供者合作夥伴，且擁有客戶 Azure 訂用帳戶的計費關係，您可以使用此 REST API 提供可擴充的方式來追蹤訂用帳戶所產生的使用量，以便在結尾傳送發票給您的客戶每個計費週期的。

若要追蹤使用方式並協助預測個別客戶的每月帳單和帳單，您可以結合費率卡片查詢以[取得 Microsoft Azure 的價格](get-prices-for-microsoft-azure.md)，取得[客戶的 Azure 使用量記錄](get-a-customer-s-utilization-record-for-azure.md)要求。

價格會依市場和貨幣而有所不同，而此 API 會將位置納入考慮。 根據預設，它會在合作夥伴中心和您的瀏覽器語言中使用您的夥伴設定檔設定，但可自訂。 如果您從單一的集中式辦公室管理多個市場的銷售，這就特別相關。

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

說明 Azure 使用率記錄資源的屬性。

| 屬性       | 類型                                      | 必要項 | 描述                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | string                                    | 是      | 使用量匯總時間範圍的開頭。 回應會依據耗用量時間分組（當實際使用資源時，其會回報給計費系統）。 |
| usageEndTime   | string                                    | 是      | 使用量匯總時間範圍的結尾。 回應會依據耗用量時間分組（當實際使用資源時，其會回報給計費系統）。   |
| 資源       | object                                    | 是      | 包含[remove-azureresource](#azureresource)物件。                                                                                                                                     |
| quantity       | 數字                                    | 是      | Remove-azureresource 使用的數量[。](#azureresource)                                                                                                                           |
| 單位           | string                                    | 否       | 數量的類型（小時、位元組等）這個屬性是選擇性的                                                                                                                     |
| infoFields     | object                                    | 是      | 實例層級詳細資料的索引鍵/值組。 這個物件可能是空的。                                                                                                                    |
| instanceData   | object                                    | 否       | 包含[AzureInstanceData](#azureinstancedata)物件，其中包含實例層級詳細資料的索引鍵/值組。 這個屬性是選擇性的，而且可能不會包含在內。                  |
| 屬性     | [ResourceAttributes](utility-resources.md#resourceattributes) | 是      | 中繼資料屬性。 包含 "objectType"： "AzureUtilizationRecord"                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>AzureUtilizationRecord 資源上的作業

- [取得客戶的 Azure 使用率記錄](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>Remove-azureresource

說明 Azure 資源的屬性。

| 屬性    | 類型   | 必要項 | 描述                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | string | 是      | Azure 資源的唯一識別碼。 也稱為 resourceID 或資源 GUID。 |
| 名稱        | string | 否       | 所耗用資源的易記名稱。 這個屬性為選擇性。            |
| category    | string | 否       | 已使用資源的類別。 這個屬性為選擇性。                   |
| 分類 | string | 否       | 已使用資源的子類別。 這個屬性為選擇性。               |
| 區內      | string | 否       | 已使用資源的區域。 這個屬性為選擇性。                     |

## <a name="azureinstancedata"></a>AzureInstanceData

說明 Azure 實例資料資源的屬性。

| 屬性       | 類型             | 必要項 | 描述                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| ResourceUri    | string           | 是      | 完整的 Azure 資源識別碼，包含資源群組和實例名稱。                   |
| 位置       | string           | 是      | 執行服務的區域。                                                                               |
| partNumber     | object           | 是      | 唯一命名空間，用來識別商用 marketplace 協力廠商使用的資源。 這可能是空字串。 |
| orderNumber    | 數字           | 是      | 唯一命名空間，用來識別商用 marketplace 的協力廠商訂單。 這可能是空字串。          |
| tags           | 字串的陣列 | 否       | 使用者所指定的資源標記。 這個屬性是選擇性的，而且可能不會包含在內。                            |
| additionalInfo | 字串的陣列 | 否       | Azure 資源的其他資料。 這個屬性是選擇性的，而且可能不會包含在內。                          |