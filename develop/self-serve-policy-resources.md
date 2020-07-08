---
title: 自助服務原則資源
description: 合作夥伴會為客戶設定自助服務原則。
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04daf6aaeb69153c4139941188f53dbab8979969
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095844"
---
# <a name="selfservepolicy-resource"></a>SelfServePolicy 資源

**適用於：**

- 合作夥伴中心

合作夥伴會為客戶設定自助服務原則。

## <a name="selfservepolicy"></a>SelfServePolicy

描述購物車。

| 屬性              | 類型             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | 字串           | 成功建立自助原則時所提供的自助原則識別碼。     |
| SelfServeEntity       | SelfServeEntity  | 要授與存取權的自助實體。                                                     |
| 授與者               | 授與者          | 授與存取權的授與者。                                                                    |
| 權限           | 許可權陣列| [許可權](#permission)資源的陣列。                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

代表要授與許可權的實體。

| 屬性             | 類型|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | 字串                           | 要授與存取權的實體，接受的值： Customer。                                 |
| TenantID             | 字串                           | 被授與存取權之實體的租使用者識別碼。                                   |

## <a name="grantor"></a>授與者

表示授與許可權的授權者。

| 屬性             | 類型|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType          | 字串                           | 授與者授與存取權，可接受的值： BillToPartner。                               |
| TenantID             | 字串                           | 授與存取權之實體的租使用者識別碼。                                       |


## <a name="permission"></a>權限

代表自助服務原則中的許可權。

| 屬性             | 類型|描述|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| 資源             | 字串                           | 正在授與資源存取權： AzureReservedInstances。                          |
| 動作               | 字串                           | 正在授與的動作存取權：購買                                           |
