---
title: 產品升級資源
description: 您可以使用與 Azure 方案的合作夥伴中心產品升級相關的多個資源。 其中包括 ProductUpgradeRequest、ProductUpgradesEligibility、ProductUpgradesStatus、UpgradesLineItem、UpgradeProduct 和 ErrorDetails。
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: bcdf8e0413bcccc7fa9641b16266adf93a14808b
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416338"
---
# <a name="product-upgrade-resources"></a>產品升級資源

適用於：

- 夥伴中心

您可以使用下列資源，取得從 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶到 Azure 方案之合作夥伴中心產品升級的相關資訊。

## <a name="productupgraderequest"></a>ProductUpgradeRequest

**ProductUpgradesRequest**資源會提供產品升級要求物件的相關資訊。

| 屬性 | 類型 | 描述 |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| Id           | string                                       | 識別客戶的 GUID 格式字串。 |
| productFamily        | string                                       | 為其要求升級的產品系列。 |
| 屬性           | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。 |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility

**ProductUpgradesEligibility**資源會提供客戶升級產品之資格的相關資訊。

| 屬性 | 類型 | 描述 |
|----------------------|--------------------------------------------- |----------------------------------------------------------------|
| Id           | string                                       | 識別客戶的 GUID 格式字串。 |          | productFamily        | string                                       | 為其要求升級的產品系列。 |
| isEligible           | bool                                         | Bool 值指出客戶是否符合要求的升級資格。 |
| upgradeId            | string                                       | 如果指定家族的產品升級已準備就緒，則為升級識別碼。 |
| reason               | string                                       | 客戶不符合產品升級資格的原因。 |
| productFamily        | string                                       | 為其要求升級的產品系列。 |
| 屬性           | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。  

## <a name="productupgradesstatus"></a>ProductUpgradesStatus

**ProductUpgradesStatus**資源會提供產品升級狀態的相關資訊。

| 屬性 | 類型 | 描述 |
|---------------------|----------------------------------------------------------------|-----------------------------------------------|
| Id                  | string                                                         | 識別升級的 GUID 格式字串。 |
| productFamily       | string                                                         | 為其要求升級的產品系列。
| status              | string                                                         | 產品升級的狀態。
| lineItems           | [UpgradesLineItem](#upgradeslineitem)資源的陣列       | 物件的陣列，針對屬於要求主體一部分的每個明細專案，提供升級詳細資料的資訊。
| errorDetails        | [ErrorDetails](#errordetails)資源                         | 要求升級的錯誤詳細資料。
| 屬性          | [ResourceAttributes](utility-resources.md#resourceattributes)  | 中繼資料屬性。 |

## <a name="upgradeslineitem"></a>UpgradesLineItem

**UpgradesLineItem**資源會針對要求的每個明細專案，描述產品升級詳細資料的狀態。

| 屬性 | 類型 | 描述 |
|-----------------|-----------------------------------------------------|--------------------------------------------------------------|
| sourceProduct   | [UpgradeProduct](#upgradeproduct)物件            | 要升級之來源產品的資訊。 |
| targetProduct   | [UpgradeProduct](#upgradeproduct)物件            | 升級後的目標產品資訊。 |
| upgradedDate    | UTC 日期時間格式的字串                      | 訂閱的升級日期。 |
| status          | string                                              | 產品升級的狀態。 |
| errorDetails    | [ErrorDetails](#errordetails)資源              | 要求升級的錯誤詳細資料。 |
| 屬性      | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。  |

## <a name="upgradeproduct"></a>UpgradeProduct

**UpgradeProduct**資源會提供所升級產品的相關資訊。

| 屬性 | 類型 |描述 |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| id                   | string                                       | 可識別產品的 GUID 格式字串。 |
| 名稱                 | string                                       | 要升級之產品的易記名稱。 |  
| 屬性           | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。 |

## <a name="errordetails"></a>ErrorDetails

**ErrorDetails**資源會提供升級程式期間發生之錯誤的詳細資料。

| 屬性 | 類型 | 描述 |
|-------------------------|----------------------------------------------|-------------------------------------------------------------|
| code                    | string                                       | 產品升級失敗時的錯誤碼。 |
| message                 | string                                       | 產品升級失敗時的錯誤訊息。 |
| 屬性              | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。 |
