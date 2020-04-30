---
title: 授權資源
description: 描述與授權相關的資源。
ms.assetid: 20592E06-8A87-41F4-B8B0-6F9200556FDA
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 60ef6082517fc0f5daa524ddb2da8f9e11e4be06
ms.sourcegitcommit: 45094b6fb1437bca51f97e193ac2957747dbea27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82124720"
---
# <a name="license-resources"></a>授權資源

**適用于**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

描述與授權相關的資源。

## <a name="license"></a>授權

描述使用者授權。

>[!NOTE]
>由世紀營運的合作夥伴中心不支援。

| 屬性     | 類型                                                           | 描述                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | ServicePlan 資源的陣列                                 | 對應至授權的服務方案集合 |
| productSKU   | ProductSku                                                     | 對應至授權之產品的 sku。        |
| 屬性   | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至授權的中繼資料屬性。          |

## <a name="licenseupdate"></a>LicenseUpdate

提供用來指派或移除使用者授權的資訊。

| 屬性         | 類型                                                           | 描述                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | 物件的陣列                                               | [LicenseAssignment](#licenseassignment)物件的陣列。 |
| licensesToRemove | 字串的陣列                                               | 要移除之授權的產品 SKU 識別碼。    |
| licenseWarnings  | 物件的陣列                                               | [LicenseWarning](#licensewarning)物件的陣列。       |
| 屬性       | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。                                  |

## <a name="licenseassignment"></a>LicenseAssignment

提供授權更新作業所需的資訊。

| 屬性      | 類型             | 描述                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | 字串的陣列 | 要從可用性中排除給使用者的服務方案識別碼。 |
| skuId         | 字串           | 授權的產品 SKU 識別碼。                                |

## <a name="licensewarning"></a>LicenseWarning

包含在授權更新作業期間發生的警告資訊。

| 屬性     | 類型             | 說明                                         |
|--------------|------------------|-----------------------------------------------------|
| code         | 字串           | 警告碼。                                   |
| 訊息      | 字串           | 警告訊息。                                |
| servicePlans | 字串的陣列 | 與警告相關聯的服務方案名稱。 |

## <a name="productsku"></a>ProductSku

描述產品詳細資料。

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>類型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>id</td>
<td>字串</td>
<td>產品識別碼。</td>
</tr>
<tr class="even">
<td>NAME</td>
<td>字串</td>
<td>使用者主體識別碼。</td>
</tr>
<tr class="odd">
<td>skuPartNumber</td>
<td>字串</td>
<td>產品的 SKU 元件編號名稱。 例如，針對 Office 365 方案 E3，此值為<code>EnterprisePack</code>。 如果識別碼無法使用，這個屬性可以用來取代識別碼。</td>
</tr>
<tr class="even">
<td>targetType</td>
<td>字串</td>
<td>產品的目標型別。 這個屬性會識別產品是否適用于<code>User</code>或。 <code>Tenant</code></td>
</tr>
<tr class="odd">
<td>licenseGroupId</td>
<td>字串</td>
<td>透過群組識別碼識別管理 productSku 授權的授權或服務。 產品會在授權群組底下隔離，以提供更好的管理能力。
<p><code>group1</code>-其授權可由 AZURE ACTIVE DIRECTORY （AAD）管理的所有產品。</p>
<p><code>group2</code>- Minecraft 產品授權。</p></td>
</tr>
</tbody>
</table>

## <a name="serviceplan"></a>服務方案

識別產品 SKU 內可部署的服務。 產品可以有許多服務方案。

| 屬性         | 類型   | 描述                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | 字串 | 服務方案識別碼。                                                                                      |
| displayName      | 字串 | 服務方案的當地語系化顯示名稱。                                                                  |
| serviceName      | 字串 | 服務名稱。                                                                                                 |
| capabilityStatus | 字串 | 服務方案的服務方案狀態。                                                                      |
| targetType       | 字串 | 服務方案的目標型別。 這個屬性會識別產品是否適用于「使用者」或「租使用者」。 |

## <a name="subscribedsku"></a>SubscribedSku

描述租使用者所擁有的訂閱產品。

| 屬性         | 類型                                                           | 描述                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | integer                                                        | 可供指派的單位數。 此值的計算方式為單位-已耗用單位總數。 |
| activeUnits      | integer                                                        | 要指派的作用中單位數。                                                        |
| consumedUnits    | integer                                                        | 耗用的單位數。                                                                     |
| suspendedUnits   | integer                                                        | 已暫停的單位數。                                                                    |
| totalUnits       | integer                                                        | 總單位數。 這個值是以作用中和警告單位的總和來計算。         |
| warningUnits     | integer                                                        | 警告單位數目。                                                                      |
| productSku       | ProductSku                                                     | 產品 sku。                                                                                  |
| servicePlans     | ServicePlan 資源的陣列                                 | 產品的服務方案集合。                                                     |
| capabilityStatus | 字串                                                         | 產品的 sku 狀態。                                                                      |
| 屬性       | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至資源的中繼資料屬性。                                            |
