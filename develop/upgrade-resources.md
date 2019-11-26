---
title: Upgrade resources
description: Describes the resources used to upgrade a user from a source subscription to a target subscription.
ms.assetid: 869007B3-D6D4-4E79-B4F0-445CA5D88D2C
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b085e6598ce9585e0bcea72724817b0b76b589a1
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486278"
---
# <a name="upgrade-resources"></a>Upgrade resources


**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

Describes the resources used to upgrade a user from a source subscription to a target subscription.

## <a name="span-idupgradespan-idupgradespan-idupgradeupgrade"></a><span id="Upgrade"/><span id="upgrade"/><span id="UPGRADE"/>Upgrade


Describes the behavior of an individual upgrade resource.

| 屬性      | 在工作列搜尋方塊中輸入                   | 說明                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | 優惠供應                  | The offer of the target subscription.                                                        |
| UpgradeType   | 字串                 | The type of upgrade: "none", "upgrade\_only", or "upgrade\_with\_license\_transfer".         |
| IsEligible    | boolean                | Identifies if the upgrade can be performed.                                                  |
| 數量      | 整數                | The quantify of the new offer to be purchased. Defaults to the source subscription quantity. |
| UpgradeErrors | array of UpgradeErrors | Reasons the upgrade cannot be performed, if applicable.                                      |
| 屬性    | ResourceAttributes     | The metadata attributes corresponding to the upgrade.                                        |

 

## <a name="span-idupgradeerrorspan-idupgradeerrorspan-idupgradeerrorupgradeerror"></a><span id="UpgradeError"/><span id="upgradeerror"/><span id="UPGRADEERROR"/>UpgradeError


Describes a reason why an upgrade cannot be performed.

| 屬性          | 在工作列搜尋方塊中輸入               | 說明                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 程式碼              | 字串             | The error code associated with the issue: "other", "delegated\_admin\_permissions\_disabled", "subscription\_status\_not\_active", "conflicting\_service\_types", "concurrency\_conflicts", "user\_context\_required", "subscription\_add\_ons\_present", "subscription\_does\_not\_have\_any\_upgrade\_paths", "subscription\_target\_offer\_not\_found", or "subscription\_not\_provisioned". |
| 說明       | 字串             | Friendly text describing the error.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | 字串             | Additional details regarding the error.                                                                                                                                                                                                                                                                                                                                                         |
| 屬性        | ResourceAttributes | The metadata attributes corresponding to the error.                                                                                                                                                                                                                                                                                                                                             |

 

## <a name="span-idupgraderesultspan-idupgraderesultspan-idupgraderesultupgraderesult"></a><span id="UpgradeResult"/><span id="upgraderesult"/><span id="UPGRADERESULT"/>UpgradeResult


Describes a the result of the subscription upgrade process.

| 屬性             | 在工作列搜尋方塊中輸入                        | 說明                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | 字串                      | The identifier of the source subscription.                                           |
| TargetSubscriptionID | 字串                      | The identifier of the target subscription.                                           |
| UpgradeType          | 字串                      | The type of upgrade: "none", "upgrade\_only", or "upgrade\_with\_license\_transfer". |
| UpgradeErrors        | array of UpgradeErrors      | Errors encountered while attemption to perform the upgrade, if applicable.           |
| LicenseErrors        | array of UserLicenseErrrors | Errors encountered while attempted to migrate user licenses, if applicable.          |
| 屬性           | ResourceAttributes          | The metadata attributes corresponding to the license.                                |

 

## <a name="span-iduserlicenseerrorspan-iduserlicenseerrorspan-iduserlicenseerroruserlicenseerror"></a><span id="UserLicenseError"/><span id="userlicenseerror"/><span id="USERLICENSEERROR"/>UserLicenseError


Describes errors arising from failed user license transfer.

| 屬性     | 在工作列搜尋方塊中輸入                   | 說明                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | 字串                 | The unique identified of the user object.                                 |
| 名稱         | 字串                 | 使用者的名稱。                                                     |
| 電子郵件        | 字串                 | The email of the user.                                                    |
| 錯誤       | array of ServiceFaults | A list of exceptions thrown when trying to perform user license transfer. |
| 屬性   | ResourceAttributes     | The metadata attributes corresponding to the license.                     |

 

 

 




