---
title: 客戶資源
description: 代表客戶或轉銷商的客戶資源。
ms.assetid: C7EC2657-62F2-43B3-B171-2F74498D45E0
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 458c2a3d888cadb4d45dd059a3865c8f1f43cc2e
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412275"
---
# <a name="customer-resources"></a>客戶資源

適用於：

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

## <a name="customer"></a>客戶

**客戶**資源代表客戶或轉銷商。 最廣泛的是，客戶資源可以是任何想要與 Microsoft 和 Microsoft 轉銷商合作的人員、員工或組織。 客戶也有公司設定檔和帳單設定檔。

>[!NOTE]
>客戶資源的速率限制為每個租**使用者**識別碼每分鐘500個要求。

| 屬性              | 類型                                                             | 描述                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | string                                                           | 客戶識別碼。                                                                                                                             |
| commerceId            | string                                                           | 商務識別碼。                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | 公司或組織的其他相關資訊。                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | 用於計費的其他資訊。                                                                                                     |
| relationshipToPartner | string                                                           | 定義合作夥伴用於此客戶的授權方案： [無]、[轉售商]、[advisor]、[新聞訂閱] 或 [microsoft\_支援]。 |
| allowDelegatedAccess  | 布林值                                                          | 合作夥伴是否已被此客戶授與委派的系統管理員許可權。 只有在依識別碼取得客戶時，才可以使用此屬性，而不是依清單。                                                         |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | 使用者認證。                                                                                                                        |
| customDomains         | 字串的陣列                                                 | 客戶的自訂網域清單。                                                                                                        |
| associatedPartnerId   | string                                                           | 與此客戶帳戶相關聯的間接轉售商。 此值只能由間接 CSP 合作夥伴設定。                              |
| 連結                 | [ResourceLinks](utility-resources.md#resourcelinks)             | 設定檔中包含的資源連結。                                                                                             |
| 屬性            | [ResourceAttributes](utility-resources.md#resourceattributes)   | 對應至設定檔的中繼資料屬性。                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

**CustomerCompanyProfile**資源是公司或組織的其他相關資訊。

| 屬性    | 類型                                                           | 描述                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | string                                                         | Azure AD 的客戶租使用者識別碼。 這也稱為 MicrosoftID。 |
| domain      | string                                                         | 客戶的名稱，例如 contoso.onmicrosoft.com。                             |
| 公司 | string                                                         | 公司或組織的名稱。                                          |
| 連結       | [ResourceLinks](utility-resources.md#resourcelinks)           | 設定檔中包含的資源連結。                                  |
| 屬性  | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。                             |

## <a name="customerbillingprofile"></a>CustomerBillingProfile

**CustomerBillingProfile**資源是用來向客戶收費的額外資訊。

| 屬性       | 類型                                                           | 描述                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | string                                                         | 設定檔識別碼。                                                                                                                                |
| firstName      | string                                                         | 客戶公司的帳單連絡人名字。 這是將會導向發票和其他帳單通訊的人員。 |
| lastName       | string                                                         | 帳單連絡人的姓氏。                                                                                                                  |
| 電子郵件          | string                                                         | 帳單連絡人的電子郵件地址                                                                                                                    |
| culture (文化特性)        | string                                                         | 其慣用的通訊和貨幣文化特性，例如 "en-us"。                                                                               |
| 語言       | string                                                         | 其慣用的通訊語言。                                                                                                            |
| 公司    | string                                                         | 公司或組織的名稱。                                                                                                               |
| defaultAddress | [地址](utility-resources.md#address)                       | 計費連絡人的傳送目標位址。                                                                                   |
| 連結          | [ResourceLinks](utility-resources.md#resourcelinks)           | 設定檔中包含的資源連結。                                                                                                       |
| 屬性     | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

**CustomerRelationshipRequest**資源包含客戶用來與夥伴建立轉銷商關係的 URL。

| 屬性   | 類型                                                           | 描述                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| URL        | string                                                         | 客戶用來與夥伴建立關聯性的 URL。 |
| 屬性 | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至關聯性要求的中繼資料屬性。       |