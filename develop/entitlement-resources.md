---
title: 權利資源
description: 描述與權利相關的資源。
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d9dbba36fb8db8d040bd61d53483c56467987691
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094006"
---
# <a name="entitlement-resources"></a>權利資源

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

## <a name="entitlement"></a>Entitlement

此資源代表客戶因為從目錄中的專案購買合作夥伴，而有權使用的產品。

| 屬性 | 類型 | Description |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | 產生權利的順序參考。 |
| productId | 字串 | 產品的識別碼。 |
| skuID | 字串 | SKU 的識別碼。 |
| quantity | int | 權利的數量（不包括未履行/數目權利）。 |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | 權利數量詳細資料的清單（每個數量的專案和狀態數目）。 |
| entitlementType | 字串 | 權利的類型。 （已從 SDK 1.8 中的[EntitlementType](#entitlementtype)更新為字串）。 |
| entitledArtifacts | IEnumerable<[成品](#artifact)> | 與權利相關聯的成品清單。 |
| IncludedEntitlements | IEnumerable<[權利](#artifact)> | 權利清單，由目錄中的 ProductId/SkuId 購買結果隱含納入。 |
| ExpiryDate | UTC 日期時間格式的字串  | 權利到期日（如果適用）。 |

## <a name="referenceorder"></a>ReferenceOrder

權利的順序參考。

| 屬性 | 類型 | Description |
|----------|------|-------------|
| id | 字串 | 參考之順序的識別碼。 |
| lineItemId | 字串 | 參考之訂單明細專案的識別碼。 |
| 替代識別碼 | 字串 | 參考之訂單明細專案的替代識別碼。 |

## <a name="quantitydetail"></a>QuantityDetail

表示權利數量的詳細資料。

| 屬性 | 類型 | Description |
|----------|------|-------------|
| quantity | int | 項目數。 |
| status | 字串 | 數量的狀態。 |

## <a name="entitlementtype"></a>EntitlementType

> [!IMPORTANT]
> SDK 1.9 版中已淘汰

具有表示權利類型之值的[列舉](https://docs.microsoft.com/dotnet/api/system.enum)。

| 值 | 描述 |
|-------|-------------|
| 軟體 | 表示與軟體相關的權利類型。 |
| VirtualMachineReservedInstance | 指出與 Azure 保留的虛擬機器執行個體相關的權利類型。 |

## <a name="artifact"></a>構件

與權利相關聯的成品。

| 屬性 | 類型 | Description |
|----------|------|-------------|
| artifactType | 字串 | 成品的類型。 （從 SDK 1.8 中的[ArtifactType](#artifacttype)更新為字串） |
| dynamicAttributes | 字典 &lt; 字串，物件&gt; | 包含 artifacttype 特定值的動態屬性。 例如，當 artifactType = "reservedinstance" 時，此屬性會包含 "reservationType" = "virtualmachines" 或 "reservationType" = "sqldatabases"，表示虛擬機器保留實例或 Azure SQL 保留實例。 （從 SDK 1.9 版開始提供） |

## <a name="artifacttype"></a>ArtifactType

> [!IMPORTANT]
> SDK 1.9 版中已淘汰

具有值的[列舉](https://docs.microsoft.com/dotnet/api/system.enum)，指出權利成品的類型。

| 值                          | 描述                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | 表示成品輔助 Azure 保留的虛擬機器執行個體的抓取。 |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

與 Azure 保留實例權利相關聯的成品。 它繼承自成品[類別。](#artifact)

| 屬性   | 類型                           | Description                                        |
|------------|--------------------------------|----------------------------------------------------|
| link       | [連結](./utility-resources.md#link) | 取得所有關聯成品詳細資料的連結。   |
| resourceID | 字串                         | Azure 保留順序或資源的識別碼。 |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

表示叫用 Azure 保留實例成品連結時傳回的實體。

|   屬性   |           類型           |                          描述                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     type     |          字串          |                     成品的類型。                     |
| reservations | IEnumerable<Reservation> | 指出 Azure 資源或保留訂單識別碼。 |

## <a name="reservation"></a>保留

表示個別保留區。

| 屬性          | 類型                           | Description                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | 字串                         | 保留的識別碼。                                         |
| scopeType         | 字串                         | 與虛擬機器保留相關聯的範圍類型。 |
| displayName       | 字串                         | 保留的顯示名稱。                               |
| appliedScopes     | IEnumerable                    | 與保留相關聯的已套用範圍清單。 （只有在未共用 scopeType 時才可使用）。 |
| quantity          | int                            | 保留中的虛擬機器數目。                 |
| expiryDateTime    | UTC 日期時間格式的字串 | 保留的到期日。                                |
| effectiveDateTime | UTC 日期時間格式的字串 | 保留的生效日期。                             |
| provisioningState | 字串                         | 保留的布建狀態。                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> SDK 1.9 版中已淘汰

與 Azure 保留的虛擬機器實例權利相關聯的成品。 它繼承自成品[類別。](#artifact)

| 屬性   | 類型                              | Description                                        |
|------------|-----------------------------------|----------------------------------------------------|
| link       | [連結](utility-resources.md#link) | 取得所有關聯成品詳細資料的連結。   |
| resourceID | 字串                            | Azure 保留順序或資源的識別碼。 |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> SDK 1.9 版中已淘汰

代表在 Azure 保留的虛擬機器實例成品連結叫用時所傳回的實體。

| 屬性                    | 類型                                                                 | 描述           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| 類型                        | [ArtifactType](#artifacttype)                                        | 成品的類型。 |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | 指出 Azure 資源或保留訂單識別碼。 |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> SDK 1.9 版中已淘汰

代表個別的虛擬機器保留。

|     屬性      |              類型              |                                                Description                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             字串             |                                         保留的識別碼。                                         |
|     scopeType     |             字串             |                     與虛擬機器保留相關聯的範圍類型。                     |
|    displayName    |             字串             |                                    保留的顯示名稱。                                    |
|   appliedScopes   |      IEnumerable<string>       | 與保留相關聯的已套用範圍清單。 （只有在未共用 scopeType 時才可使用）。 |
|     quantity      |              int               |                             保留中的虛擬機器數目。                             |
|  expiryDateTime   | UTC 日期時間格式的字串 |                                    保留的到期日。                                     |
| effectiveDateTime | UTC 日期時間格式的字串 |                                   保留的生效日期。                                   |
| provisioningState |             字串             |                                 保留的布建狀態。                                 |
