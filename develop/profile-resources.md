---
title: 設定檔資源
description: 描述雲端解決方案提供者設定檔的行為。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef14eb0307dae0d58dc9903a867ec3bee4ebb323
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925825"
---
# <a name="profile-resources"></a>設定檔資源

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

描述雲端解決方案提供者設定檔的行為。

## <a name="billingprofile"></a>BillingProfile

描述合作夥伴的帳單設定檔。

| 屬性            | 類型                                                           | 描述                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| companyName         | 字串                                                         | 帳單公司名稱。                                   |
| address             | [位址](utility-resources.md#address)                       | 公司或組織的帳單位址位址。 |
| primaryContact      | [Contact](utility-resources.md#contact)                       | 公司或組織的主要連絡人。        |
| purchaseOrderNumber | 字串                                                         | 公司或組織的採購單號碼。        |
| taxId               | 字串                                                         | 公司或組織的稅務識別碼。                       |
| billingCurrency     | 字串                                                         | 公司或組織所使用的貨幣。           |
| profileType         | 字串                                                         | 夥伴配置檔案類型。                                   |
| 連結               | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應于設定檔的資源連結。            |
| 屬性          | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應于設定檔的中繼資料屬性。       |

## <a name="legalbusinessprofile"></a>>legalbusinessprofile

描述合作夥伴的法律商務設定檔。

| 屬性               | 類型                                                           | 描述                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| companyName            | 字串                                                         | 合法的公司名稱。                                                                                                                                              |
| address                | [位址](utility-resources.md#address)                       | 公司或組織的位址。                                                                                                                          |
| primaryContact         | [Contact](utility-resources.md#contact)                       | 公司或組織的主要連絡人。                                                                                                                 |
| companyApproverAddress | [位址](utility-resources.md#address)                       | 公司核准者位址。                                                                                                                                        |
| companyApproverEmail   | 字串                                                         | 公司核准者電子郵件。                                                                                                                                          |
| vettingStatus          | 字串                                                         | 調查狀態。 這個值是 [**VettingStatus**/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus) 中找到的其中一個成員名稱的字串表示。           |
| vettingSubStatus       | 字串                                                         | 調查的子狀態。 這個值是 [**VettingSubStatus**/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus) 中找到的其中一個成員名稱的字串表示。 |
| profileType            | 字串                                                         | 夥伴配置檔案類型。                                                                                                                                            |
| 連結                  | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應于設定檔的資源連結。                                                                                                                     |
| 屬性             | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應于設定檔的中繼資料屬性。                                                                                                                |

## <a name="mpnprofile"></a>>mpnprofile

描述夥伴的 Microsoft 合作夥伴網路設定檔。

| 屬性    | 類型                                                           | 描述                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | 字串                                                         | 公司或組織名稱。                     |
| mpnId       | 字串                                                         | Microsoft 合作夥伴網路識別碼。                     |
| profileType | 字串                                                         | 夥伴配置檔案類型。                             |
| 連結       | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應于設定檔的資源連結。      |
| 屬性  | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應于設定檔的中繼資料屬性。 |

## <a name="organizationprofile"></a>OrganizationProfile

描述夥伴的組織設定檔。

| 屬性       | 類型                                                           | 描述                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | 字串                                                         | 組織的識別碼。                                                 |
| companyName    | 字串                                                         | 公司或組織的名稱。                               |
| defaultAddress | [位址](utility-resources.md#address)                       | 公司或組織的預設位址。                    |
| tenantId       | 字串                                                         | 租用戶識別碼。                                                 |
| 網域         | 字串                                                         | 公司或組織的網域。                                  |
| 電子郵件          | 字串                                                         | 取得或設定父訂用帳戶。                                  |
| 語言       | 字串                                                         | 慣用的通訊語言。                              |
| culture        | 字串                                                         | 通訊和貨幣的慣用文化特性，例如 "en-us"。 |
| profileType    | 字串                                                         | 夥伴配置檔案類型。                                              |
| 連結          | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應于設定檔的資源連結。                       |
| 屬性     | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應于設定檔的中繼資料屬性。                  |

## <a name="supportprofile"></a>>supportprofile

描述合作夥伴的支援設定檔。

| 屬性    | 類型                                                           | 描述                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| 電子郵件       | 字串                                                         | 與設定檔相關聯的電子郵件地址。        |
| telephone   | 字串                                                         | 與設定檔相關聯的電話號碼。         |
| 網站     | 字串                                                         | 支援網站。                                  |
| profileType | 字串                                                         | 夥伴配置檔案類型。                             |
| 連結       | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應于設定檔的資源連結。      |
| 屬性  | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應于設定檔的中繼資料屬性。 |

