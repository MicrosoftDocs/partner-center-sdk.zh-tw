---
title: 使用者資源
description: 描述個別合作夥伴中心使用者、其個人和帳戶資訊，以及他們在合作夥伴中心內的許可權。
ms.assetid: A2DEDDAB-C4DA-4ECA-931F-2054AB005973
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d3ee186b56ab7553b21e5625579c2a00a50e4492
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414440"
---
# <a name="user-resources"></a>使用者資源


**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

描述個別合作夥伴中心使用者、其個人和帳戶資訊，以及他們在合作夥伴中心內的許可權。

## <a name="span-iduserspan-iduserspan-iduseruser"></a><span id="User"/><span id="user"/><span id="USER"/>使用者


描述個別使用者。

| 屬性              | 類型                                                           | 描述                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | string                                                         | 使用者識別碼。                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | 使用者主體識別碼。                                                                                                                                                                                             |
| firstName             | string                                                         | 使用者的名字。                                                                                                                                                                                                |
| lastName              | string                                                         | 使用者的姓氏。                                                                                                                                                                                                 |
| displayName           | string                                                         | 使用者的顯示名稱。                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | 使用者的密碼設定檔。                                                                                                                                                                                               |
| phoneNumber           | string                                                         | 使用者的電話號碼。                                                                                                                                                                                                   |
| lastDirectorySyncTime | UTC 日期時間格式的字串                                 | 最後一次此使用者的資訊已在 Azure Active Directory 與內部部署 Active Directory 之間同步處理。 只有在啟用 Azure AD Connect 同步處理時，才會顯示日期時間值。 否則，此值為 null。 |
| userDomainType        | string                                                         | 使用者網欄位型別：「無」、「受管理」或「同盟」。                                                                                                                                                                   |
| State                 | string                                                         | 使用者的狀態：「作用中」、「非作用中」（適用于已刪除的使用者）。                                                                                                                                                          |
| softDeletionTime      | UTC 日期時間格式的字串                                 | 表示與已刪除的使用者相關聯的資料永久刪除，因而無法復原的三十天期間開始。                                                                          |
| 連結                 | [ResourceLinks](utility-resources.md#resourcelinks)           | 資源連結。                                                                                                                                                                                                        |
| 屬性            | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。                                                                                                                                                                                                   |

 

## <a name="span-idcustomeruserspan-idcustomeruserspan-idcustomerusercustomeruser"></a><span id="CustomerUser"/><span id="customeruser"/><span id="CUSTOMERUSER"/>CustomerUser


描述客戶使用者。

| 屬性              | 類型                                                           | 描述                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | string                                                         | 使用者打算使用授權的位置。                                                                                                                                                                    |
| id                    | string                                                         | 使用者識別碼。                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | 使用者主體識別碼。                                                                                                                                                                                             |
| firstName             | string                                                         | 使用者的名字。                                                                                                                                                                                                |
| lastName              | string                                                         | 使用者的姓氏。                                                                                                                                                                                                 |
| displayName           | string                                                         | 使用者的顯示名稱。                                                                                                                                                                                            |
| immutableId           | string                                                         | 使用者的不彈性識別碼。                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | 使用者的密碼設定檔。                                                                                                                                                                                               |
| phoneNumber           | string                                                         | 使用者的電話號碼。                                                                                                                                                                                                   |
| lastDirectorySyncTime | UTC 日期時間格式的字串                                 | 最後一次此使用者的資訊已在 Azure Active Directory 與內部部署 Active Directory 之間同步處理。 只有在啟用 Azure AD Connect 同步處理時，才會顯示日期時間值。 否則，此值為 null。 |
| userDomainType        | string                                                         | 使用者網欄位型別：「無」、「受管理」或「同盟」。                                                                                                                                                                   |
| State                 | string                                                         | 使用者的狀態：「作用中」、「非作用中」（適用于已刪除的使用者）。                                                                                                                                                          |
| softDeletionTime      | UTC 日期時間格式的字串                                 | 表示與已刪除的使用者相關聯的資料永久刪除，因而無法復原的三十天期間開始。                                                                          |
| 連結                 | [ResourceLinks](utility-resources.md#resourcelinks)           | 資源連結。                                                                                                                                                                                                        |
| 屬性            | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。                                                                                                                                                                                                   |

 

## <a name="span-idusercredentialsspan-idusercredentialsspan-idusercredentialsusercredentials"></a><span id="UserCredentials"/><span id="usercredentials"/><span id="USERCREDENTIALS"/>UserCredentials


描述使用者的登入認證。

| 屬性 | 類型                                               | 描述                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | string                                             | 使用者的名稱。                |
| 密碼 | [SecureString](utility-resources.md#securestring) | 使用者安全儲存的密碼。 |

 

## <a name="span-idusermemberspan-idusermemberspan-idusermemberusermember"></a><span id="UserMember"/><span id="usermember"/><span id="USERMEMBER"/>UserMember


描述使用者的成員資訊。

| 屬性          | 類型                                                           | 描述                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | string                                                         | 使用者的顯示名稱。   |
| userPrincipalName | string                                                         | 使用者主體的名稱。    |
| roleId            | string                                                         | 使用者角色的識別碼。 |
| id                | string                                                         | 成員的識別碼。      |
| 屬性        | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。           |

 

 

 




