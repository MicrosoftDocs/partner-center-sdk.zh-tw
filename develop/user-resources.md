---
title: 使用者資源
description: 描述個別合作夥伴中心使用者、其個人和帳戶資訊，以及他們在合作夥伴中心內的許可權。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c88b9b65dfb925712ff85fb42d34251cca6e0b5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86093549"
---
# <a name="user-resources"></a>使用者資源

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

描述個別合作夥伴中心使用者、其個人和帳戶資訊，以及他們在合作夥伴中心內的許可權。

## <a name="user"></a>使用者

描述個別使用者。

| 屬性              | 類型                                                           | 描述                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | 字串                                                         | 使用者識別碼。                                                                                                                                                                                                       |
| userPrincipalName     | 字串                                                         | 使用者主體識別碼。                                                                                                                                                                                             |
| firstName             | 字串                                                         | 使用者的名字。                                                                                                                                                                                                |
| lastName              | 字串                                                         | 使用者的姓氏。                                                                                                                                                                                                 |
| displayName           | 字串                                                         | 使用者的顯示名稱。                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | 使用者的密碼設定檔。                                                                                                                                                                                               |
| phoneNumber           | 字串                                                         | 使用者的電話號碼。                                                                                                                                                                                                   |
| lastDirectorySyncTime | UTC 日期時間格式的字串                                 | 最後一次此使用者的資訊已在 Azure Active Directory 與內部部署 Active Directory 之間同步處理。 只有在啟用 Azure AD Connect 同步處理時，才會顯示日期時間值。 否則，此值為 null。 |
| userDomainType        | 字串                                                         | 使用者網欄位型別：「無」、「受管理」或「同盟」。                                                                                                                                                                   |
| state                 | 字串                                                         | 使用者的狀態：「作用中」、「非作用中」（適用于已刪除的使用者）。                                                                                                                                                          |
| softDeletionTime      | UTC 日期時間格式的字串                                 | 表示與已刪除的使用者相關聯的資料永久刪除，因而無法復原的三十天期間開始。                                                                          |
| 連結                 | [ResourceLinks](utility-resources.md#resourcelinks)           | 資源連結。                                                                                                                                                                                                        |
| 屬性            | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。                                                                                                                                                                                                   |

## <a name="customeruser"></a>CustomerUser

描述客戶使用者。

| 屬性              | 類型                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | 字串                                                         | 使用者打算使用授權的位置。                                                                                                                                                                    |
| id                    | 字串                                                         | 使用者識別碼。                                                                                                                                                                                                       |
| userPrincipalName     | 字串                                                         | 使用者主體識別碼。                                                                                                                                                                                             |
| firstName             | 字串                                                         | 使用者的名字。                                                                                                                                                                                                |
| lastName              | 字串                                                         | 使用者的姓氏。                                                                                                                                                                                                 |
| displayName           | 字串                                                         | 使用者的顯示名稱。                                                                                                                                                                                            |
| immutableId           | 字串                                                         | 使用者的不彈性識別碼。                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | 使用者的密碼設定檔。                                                                                                                                                                                               |
| phoneNumber           | 字串                                                         | 使用者的電話號碼。                                                                                                                                                                                                   |
| lastDirectorySyncTime | UTC 日期時間格式的字串                                 | 最後一次此使用者的資訊已在 Azure Active Directory 與內部部署 Active Directory 之間同步處理。 只有在啟用 Azure AD Connect 同步處理時，才會顯示日期時間值。 否則，此值為 null。 |
| userDomainType        | 字串                                                         | 使用者網欄位型別：「無」、「受管理」或「同盟」。                                                                                                                                                                   |
| state                 | 字串                                                         | 使用者的狀態：「作用中」、「非作用中」（適用于已刪除的使用者）。                                                                                                                                                          |
| softDeletionTime      | UTC 日期時間格式的字串                                 | 表示與已刪除的使用者相關聯的資料永久刪除，因而無法復原的三十天期間開始。                                                                          |
| 連結                 | [ResourceLinks](utility-resources.md#resourcelinks)           | 資源連結。                                                                                                                                                                                                        |
| 屬性            | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。                                                                                                                                                                                                   |

## <a name="usercredentials"></a>UserCredentials

描述使用者的登入認證。

| 屬性 | 類型                                               | 描述                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | 字串                                             | 使用者的名稱。                |
| 密碼 | [SecureString](utility-resources.md#securestring) | 使用者安全儲存的密碼。 |

## <a name="usermember"></a>UserMember

描述使用者的成員資訊。

| 屬性          | 類型                                                           | Description                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | 字串                                                         | 使用者的顯示名稱。   |
| userPrincipalName | 字串                                                         | 使用者主體的名稱。    |
| roleId            | 字串                                                         | 使用者角色的識別碼。 |
| id                | 字串                                                         | 成員的識別碼。      |
| 屬性        | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。           |

