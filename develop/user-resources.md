---
title: User resources
description: Describes an individual Partner Center user, their personal and account information, and the permissions they have within Partner Center.
ms.assetid: A2DEDDAB-C4DA-4ECA-931F-2054AB005973
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: edce4bb1b13550445b49979dd59b2bce0486e7fd
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486258"
---
# <a name="user-resources"></a>User resources


**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

Describes an individual Partner Center user, their personal and account information, and the permissions they have within Partner Center.

## <a name="span-iduserspan-iduserspan-iduseruser"></a><span id="User"/><span id="user"/><span id="USER"/>User


Describes an individual user.

| 屬性              | 在工作列搜尋方塊中輸入                                                           | 說明                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | 字串                                                         | The user identifier.                                                                                                                                                                                                       |
| userPrincipalName     | 字串                                                         | The user principal identifier.                                                                                                                                                                                             |
| firstName             | 字串                                                         | The first name of the user.                                                                                                                                                                                                |
| lastName              | 字串                                                         | The last name of the user.                                                                                                                                                                                                 |
| displayName           | 字串                                                         | The displayed name of the user.                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | The user's password profile.                                                                                                                                                                                               |
| phoneNumber           | 字串                                                         | The user's phone number.                                                                                                                                                                                                   |
| lastDirectorySyncTime | string in UTC date time format                                 | The last time that information for this user was synced between Azure Active Directory and on-premises Active Directory. A date time value only appears if Azure AD Connect sync is enabled. Otherwise, the value is null. |
| userDomainType        | 字串                                                         | The user domain type: "none", "managed," or "federated".                                                                                                                                                                   |
| state                 | 字串                                                         | The state of the user: "active", "inactive" (for a deleted user).                                                                                                                                                          |
| softDeletionTime      | string in UTC date time format                                 | Represents the start of the thirty day period after which data associated with a deleted user is permanently deleted and therefore unrecoverable.                                                                          |
| links                 | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links.                                                                                                                                                                                                        |
| 屬性            | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                                                                                                                                                                   |

 

## <a name="span-idcustomeruserspan-idcustomeruserspan-idcustomerusercustomeruser"></a><span id="CustomerUser"/><span id="customeruser"/><span id="CUSTOMERUSER"/>CustomerUser


Describes a customer user.

| 屬性              | 在工作列搜尋方塊中輸入                                                           | 說明                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | 字串                                                         | The location where the user intends to use the license.                                                                                                                                                                    |
| id                    | 字串                                                         | The user identifier.                                                                                                                                                                                                       |
| userPrincipalName     | 字串                                                         | The user principal identifier.                                                                                                                                                                                             |
| firstName             | 字串                                                         | The first name of the user.                                                                                                                                                                                                |
| lastName              | 字串                                                         | The last name of the user.                                                                                                                                                                                                 |
| displayName           | 字串                                                         | The displayed name of the user.                                                                                                                                                                                            |
| immutableId           | 字串                                                         | The immutable id of the user.                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | The user's password profile.                                                                                                                                                                                               |
| phoneNumber           | 字串                                                         | The user's phone number.                                                                                                                                                                                                   |
| lastDirectorySyncTime | string in UTC date time format                                 | The last time that information for this user was synced between Azure Active Directory and on-premises Active Directory. A date time value only appears if Azure AD Connect sync is enabled. Otherwise, the value is null. |
| userDomainType        | 字串                                                         | The user domain type: "none", "managed," or "federated".                                                                                                                                                                   |
| state                 | 字串                                                         | The state of the user: "active", "inactive" (for a deleted user).                                                                                                                                                          |
| softDeletionTime      | string in UTC date time format                                 | Represents the start of the thirty day period after which data associated with a deleted user is permanently deleted and therefore unrecoverable.                                                                          |
| links                 | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links.                                                                                                                                                                                                        |
| 屬性            | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                                                                                                                                                                   |

 

## <a name="span-idusercredentialsspan-idusercredentialsspan-idusercredentialsusercredentials"></a><span id="UserCredentials"/><span id="usercredentials"/><span id="USERCREDENTIALS"/>UserCredentials


Describes a user's login credentials.

| 屬性 | 在工作列搜尋方塊中輸入                                               | 說明                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | 字串                                             | 使用者的名稱。                |
| 密碼 | [SecureString](utility-resources.md#securestring) | The user's securely stored password. |

 

## <a name="span-idusermemberspan-idusermemberspan-idusermemberusermember"></a><span id="UserMember"/><span id="usermember"/><span id="USERMEMBER"/>UserMember


Describes a user's member information.

| 屬性          | 在工作列搜尋方塊中輸入                                                           | 說明                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | 字串                                                         | The displayed name for the user.   |
| userPrincipalName | 字串                                                         | The name of the user principal.    |
| roleId            | 字串                                                         | The identifier of the user's role. |
| id                | 字串                                                         | The identifier of the member.      |
| 屬性        | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.           |

 

 

 




