---
title: 權利資源
description: 描述與權利相關的資源。
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 428ac6f8b4d67894092119a6246279045a04dac0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927301"
---
# <a name="entitlement-resources"></a>權利資源

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

## <a name="entitlement"></a>Entitlement

此資源代表客戶有權使用的產品，因為合作夥伴是從類別目錄購買專案。

| 屬性 | 類型 | 描述 |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | 產生權利的訂單參考。 |
| productId | 字串 | 產品的識別碼。 |
| skuID | 字串 | SKU 的識別碼。 |
| quantity | int | 權利的數量 (排除未履行/傳輸的權利) 。 |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | 權利數量詳細資料的清單 (每個數量) 的專案數目和狀態。 |
| entitlementType | 字串 | 權利的類型。  (在 SDK 1.8 中從 [EntitlementType](#entitlementtype) 更新為字串。 )  |
| entitledArtifacts | IEnumerable<[成品](#artifact)> | 與權利相關聯的成品清單。 |
| IncludedEntitlements | IEnumerable<[權利](#artifact)> | 權利清單，因為從目錄購買 ProductId/SkuId，所以會以隱含方式納入。 |
| ExpiryDate | UTC 日期時間格式的字串  | 權利到期日 (（如果適用) ）。 |

## <a name="referenceorder"></a>ReferenceOrder

權利的順序參考。

| 屬性 | 類型 | 描述 |
|----------|------|-------------|
| id | 字串 | 參考之順序的識別碼。 |
| lineItemId | 字串 | 參考之訂單明細專案的識別碼。 |
| 替代識別碼 | 字串 | 參考之訂單明細專案的替代識別碼。 |

## <a name="quantitydetail"></a>QuantityDetail

表示權利數量的詳細資料。

| 屬性 | 類型 | 描述 |
|----------|------|-------------|
| quantity | int | 項目的數目。 |
| status | 字串 | 數量的狀態。 |

## <a name="entitlementtype"></a>EntitlementType

> [!IMPORTANT]
> SDK v1.0 中已淘汰

[列舉](/dotnet/api/system.enum)值，表示權利類型。

| 值 | 描述 |
|-------|-------------|
| 軟體 | 表示與軟體相關的權利類型。 |
| VirtualMachineReservedInstance | 表示與 Azure 保留的虛擬機器執行個體相關的權利類型。 |

## <a name="artifact"></a>構件

與權利相關聯的成品。

| 屬性 | 類型 | 描述 |
|----------|------|-------------|
| artifactType | 字串 | 成品的類型。  (已從 SDK 1.8 版中的 [ArtifactType](#artifacttype) 更新為字串)  |
| dynamicAttributes | 字典 &lt; 字串，物件&gt; | 包含 artifacttype 特定值的動態屬性。 例如，當 artifactType = "reservedinstance" 時，此屬性會包含 "reservationType" = "virtualmachines" 或 "reservationType" = "sqldatabases"，表示虛擬機器保留實例或 Azure SQL 保留實例。 從 SDK v1.0 開始 (提供)  |

## <a name="artifacttype"></a>ArtifactType

> [!IMPORTANT]
> SDK v1.0 中已淘汰

具有值的 [列舉](/dotnet/api/system.enum) ，指出權利成品的類型。

| 值                          | 描述                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | 表示成品輔助 Azure 保留的虛擬機器執行個體的抓取。 |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

與 Azure 保留實例權利相關聯的成品。 它繼承自成品[類別。](#artifact)

| 屬性   | 類型                           | 描述                                        |
|------------|--------------------------------|----------------------------------------------------|
| link       | [連結](./utility-resources.md#link) | 取得所有相關成品詳細資料的連結。   |
| Id | 字串                         | Azure 保留訂單或資源的識別碼。 |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

代表叫用 Azure 保留實例成品連結時所傳回的實體。

|   屬性   |           類型           |                          描述                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     type     |          字串          |                     成品的類型。                     |
| reservations | IEnumerable<Reservation> | 指出 Azure 資源或保留訂單識別碼。 |

## <a name="reservation"></a>保留

代表個別的保留。

| 屬性          | 類型                           | 描述                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | 字串                         | 保留的識別碼。                                         |
| scopeType         | 字串                         | 與虛擬機器保留相關聯的範圍類型。 |
| displayName       | 字串                         | 保留的顯示名稱。                               |
| appliedScopes     | IEnumerable                    | 與保留相關聯之已套用的範圍清單。  (只有在未共用 scopeType 時才可使用。 )  |
| quantity          | int                            | 保留中的虛擬機器數目。                 |
| expiryDateTime    | UTC 日期時間格式的字串 | 保留的到期日。                                |
| effectiveDateTime | UTC 日期時間格式的字串 | 保留的生效日期。                             |
| provisioningState | 字串                         | 保留的布建狀態。                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> SDK v1.0 中已淘汰

與 Azure 保留的虛擬機器實例權利相關聯的成品。 它繼承自成品[類別。](#artifact)

| 屬性   | 類型                              | 描述                                        |
|------------|-----------------------------------|----------------------------------------------------|
| link       | [連結](utility-resources.md#link) | 取得所有相關成品詳細資料的連結。   |
| Id | 字串                            | Azure 保留訂單或資源的識別碼。 |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> SDK v1.0 中已淘汰

表示叫用 Azure 保留的虛擬機器實例成品連結時所傳回的實體。

| 屬性                    | 類型                                                                 | 描述           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| type                        | [ArtifactType](#artifacttype)                                        | 成品的類型。 |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | 指出 Azure 資源或保留訂單識別碼。 |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> SDK v1.0 中已淘汰

代表個別的虛擬機器保留。

|     屬性      |              類型              |                                                描述                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             字串             |                                         保留的識別碼。                                         |
|     scopeType     |             字串             |                     與虛擬機器保留相關聯的範圍類型。                     |
|    displayName    |             字串             |                                    保留的顯示名稱。                                    |
|   appliedScopes   |      IEnumerable<string>       | 與保留相關聯之已套用的範圍清單。  (只有在未共用 scopeType 時才可使用。 )  |
|     quantity      |              int               |                             保留中的虛擬機器數目。                             |
|  expiryDateTime   | UTC 日期時間格式的字串 |                                    保留的到期日。                                     |
| effectiveDateTime | UTC 日期時間格式的字串 |                                   保留的生效日期。                                   |
| provisioningState |             字串             |                                 保留的布建狀態。                                 |
