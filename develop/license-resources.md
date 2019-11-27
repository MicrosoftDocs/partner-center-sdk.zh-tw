---
title: 授權資源
description: 描述與授權相關的資源。
ms.assetid: 20592E06-8A87-41F4-B8B0-6F9200556FDA
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 625209f834a7d89fbf288b7a1430624cb99485b1
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486928"
---
# <a name="license-resources"></a>授權資源


**適用于**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

描述與授權相關的資源。

## <a name="span-idlicensespan-idlicensespan-idlicenselicense"></a><span id="License"/><span id="license"/><span id="LICENSE"/>授權


描述使用者授權。

>[!NOTE]
>由世紀營運的合作夥伴中心不支援。

 

| 屬性     | 類型                                                           | 描述                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | ServicePlan 資源的陣列                                 | 對應至授權的服務方案集合 |
| productSKU   | ProductSku                                                     | 對應至授權之產品的 sku。        |
| 屬性   | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至授權的中繼資料屬性。          |

 

## <a name="span-idlicenseupdatespan-idlicenseupdatespan-idlicenseupdatelicenseupdate"></a><span id="LicenseUpdate"/><span id="licenseupdate"/><span id="LICENSEUPDATE"/>LicenseUpdate


提供用來指派或移除使用者授權的資訊。

| 屬性         | 類型                                                           | 描述                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | 物件的陣列                                               | [LicenseAssignment](#licenseassignment)物件的陣列。 |
| licensesToRemove | 字串陣列                                               | 要移除之授權的產品 SKU 識別碼。    |
| licenseWarnings  | 物件的陣列                                               | [LicenseWarning](#licensewarning)物件的陣列。       |
| 屬性       | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。                                  |

 

## <a name="span-idlicenseassignmentspan-idlicenseassignmentspan-idlicenseassignmentlicenseassignment"></a><span id="LicenseAssignment"/><span id="licenseassignment"/><span id="LICENSEASSIGNMENT"/>LicenseAssignment


提供授權更新作業所需的資訊。

| 屬性      | 類型             | 描述                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | 字串陣列 | 要從可用性中排除給使用者的服務方案識別碼。 |
| skuId         | 字串           | 授權的產品 SKU 識別碼。                                |

 

## <a name="span-idlicensewarningspan-idlicensewarningspan-idlicensewarninglicensewarning"></a><span id="LicenseWarning"/><span id="licensewarning"/><span id="LICENSEWARNING"/>LicenseWarning


包含在授權更新作業期間發生的警告資訊。

| 屬性     | 類型             | 描述                                         |
|--------------|------------------|-----------------------------------------------------|
| code         | 字串           | 警告碼。                                   |
| 訊息      | 字串           | 警告訊息。                                |
| servicePlans | 字串陣列 | 與警告相關聯的服務方案名稱。 |

 

## <a name="span-idproductskuspan-idproductskuspan-idproductskuproductsku"></a><span id="ProductSku"/><span id="productsku"/><span id="PRODUCTSKU"/>ProductSku


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
<td>name</td>
<td>字串</td>
<td>使用者主體識別碼。</td>
</tr>
<tr class="odd">
<td>skuPartNumber</td>
<td>字串</td>
<td>產品的 SKU 元件編號名稱。 例如，針對 Office 365 方案 E3，此值為 &quot;EnterprisePack&quot;。 如果識別碼無法使用，這可以用來取代識別碼。</td>
</tr>
<tr class="even">
<td>目標</td>
<td>字串</td>
<td>產品的目標型別。 這會識別產品是否適用于 &quot;的使用者&quot; 或 &quot;的租使用者&quot;。</td>
</tr>
<tr class="odd">
<td>licenseGroupId</td>
<td>字串</td>
<td>透過群組識別碼識別管理 productSku 授權的授權或服務。 產品會在授權群組底下隔離，以提供更好的管理能力。
<p>&quot;group1&quot;-其授權可由 Azure Active Directory （AAD）管理的所有產品。</p>
<p>&quot;group2&quot;-Minecraft 產品授權。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idserviceplanspan-idserviceplanspan-idserviceplanserviceplan"></a><span id="ServicePlan"/><span id="serviceplan"/><span id="SERVICEPLAN"/>ServicePlan


識別產品 SKU 內可部署的服務。 產品可以有許多服務方案。

| 屬性         | 類型   | 描述                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | 字串 | 服務方案識別碼。                                                                                      |
| displayName      | 字串 | 服務方案的當地語系化顯示名稱。                                                                  |
| serviceName      | 字串 | 服務名稱。                                                                                                 |
| capabilityStatus | 字串 | 服務方案的服務方案狀態。                                                                      |
| 目標       | 字串 | 服務方案的目標型別。 這會識別產品是否適用于「使用者」或「租使用者」。 |

 

## <a name="span-idsubscribedskuspan-idsubscribedskuspan-idsubscribedskusubscribedsku"></a><span id="SubscribedSku"/><span id="subscribedsku"/><span id="SUBSCRIBEDSKU"/>SubscribedSku


描述租使用者所擁有的訂閱產品。

| 屬性         | 類型                                                           | 描述                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | 整數                                                        | 可供指派的單位數。 這會計算為總單位-耗用單位。 |
| activeUnits      | 整數                                                        | 要指派的作用中單位數。                                                        |
| consumedUnits    | 整數                                                        | 耗用的單位數。                                                                     |
| suspendedUnits   | 整數                                                        | 已暫停的單位數。                                                                    |
| totalUnits       | 整數                                                        | 總單位數。 這是以作用中和警告單位的總和來計算。         |
| warningUnits     | 整數                                                        | 警告單位的數目。                                                                      |
| productSku       | ProductSku                                                     | 產品 sku。                                                                                  |
| servicePlans     | ServicePlan 資源的陣列                                 | 產品的服務方案集合。                                                     |
| capabilityStatus | 字串                                                         | 產品的 sku 狀態。                                                                      |
| 屬性       | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至資源的中繼資料屬性。                                            |

 

 

 



