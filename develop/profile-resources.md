---
title: 設定檔資源
description: 描述雲端解決方案提供者設定檔的行為。
ms.assetid: 42F2959B-D70D-41A7-9A50-E22A2356A339
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9bd3f5322de7fae9a919e4bcfdd747a6bbc89e80
ms.sourcegitcommit: bea0d0cf3c1af7a75c9b150d53de53193a673fae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82119174"
---
# <a name="profile-resources"></a>設定檔資源

**適用于**

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
| purchaseOrderNumber | 字串                                                         | 公司或組織的訂單號碼。        |
| taxId               | 字串                                                         | 公司或組織的稅務識別碼。                       |
| billingCurrency     | 字串                                                         | 公司或組織所使用的貨幣。           |
| profileType         | 字串                                                         | 夥伴配置檔案類型。                                   |
| 連結               | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。            |
| 屬性          | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。       |

## <a name="legalbusinessprofile"></a>LegalBusinessProfile

描述合作夥伴的合法商務設定檔。

| 屬性               | 類型                                                           | 描述                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| companyName            | 字串                                                         | 合法的公司名稱。                                                                                                                                              |
| address                | [位址](utility-resources.md#address)                       | 公司或組織的位址。                                                                                                                          |
| primaryContact         | [Contact](utility-resources.md#contact)                       | 公司或組織的主要連絡人。                                                                                                                 |
| companyApproverAddress | [位址](utility-resources.md#address)                       | 公司核准者位址。                                                                                                                                        |
| companyApproverEmail   | 字串                                                         | 公司核准者電子郵件。                                                                                                                                          |
| vettingStatus          | 字串                                                         | 調查狀態。 這個值是在[**VettingStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus)中找到的其中一個成員名稱的字串表示。           |
| vettingSubStatus       | 字串                                                         | 調查子狀態。 這個值是在[**VettingSubStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus)中找到的其中一個成員名稱的字串表示。 |
| profileType            | 字串                                                         | 夥伴配置檔案類型。                                                                                                                                            |
| 連結                  | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。                                                                                                                     |
| 屬性             | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。                                                                                                                |

## <a name="mpnprofile"></a>MpnProfile

描述合作夥伴的 Microsoft 合作夥伴網路設定檔。

| 屬性    | 類型                                                           | 描述                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | 字串                                                         | 公司或組織名稱。                     |
| mpnId       | 字串                                                         | Microsoft 合作夥伴網路識別碼。                     |
| profileType | 字串                                                         | 夥伴配置檔案類型。                             |
| 連結       | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。      |
| 屬性  | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。 |

## <a name="organizationprofile"></a>OrganizationProfile

描述合作夥伴的組織設定檔。

| 屬性       | 類型                                                           | 描述                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | 字串                                                         | 組織的識別碼。                                                 |
| companyName    | 字串                                                         | 公司或組織的名稱。                               |
| defaultAddress | [位址](utility-resources.md#address)                       | 公司或組織的預設位址。                    |
| tenantId       | 字串                                                         | 租用戶識別碼。                                                 |
| 網域         | 字串                                                         | 公司或組織的網域。                                  |
| 電子郵件          | 字串                                                         | 取得或設定父訂用帳戶。                                  |
| 語言       | 字串                                                         | 通訊的慣用語言。                              |
| culture        | 字串                                                         | 通訊和貨幣的慣用文化特性，例如 "en-us"。 |
| profileType    | 字串                                                         | 夥伴配置檔案類型。                                              |
| 連結          | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。                       |
| 屬性     | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。                  |

## <a name="supportprofile"></a>SupportProfile

描述合作夥伴的支援設定檔。

| 屬性    | 類型                                                           | 描述                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| 電子郵件       | 字串                                                         | 與設定檔相關聯的電子郵件地址。        |
| telephone   | 字串                                                         | 與設定檔相關聯的電話號碼。         |
| 網站     | 字串                                                         | 支援網站。                                  |
| profileType | 字串                                                         | 夥伴配置檔案類型。                             |
| 連結       | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。      |
| 屬性  | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。 |

