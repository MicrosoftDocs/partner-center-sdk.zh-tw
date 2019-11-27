---
title: 設定檔資源
description: 描述雲端解決方案提供者設定檔的行為。
ms.assetid: 42F2959B-D70D-41A7-9A50-E22A2356A339
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3449aeb3695a9f286f37668d3f0862dc7b5cfa9f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486758"
---
# <a name="profile-resources"></a>設定檔資源


**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

描述雲端解決方案提供者設定檔的行為。

## <a name="span-idbillingprofilespan-idbillingprofilespan-idbillingprofilebillingprofile"></a><span id="BillingProfile"/><span id="billingprofile"/><span id="BILLINGPROFILE"/>BillingProfile


描述合作夥伴的帳單設定檔。

| 屬性            | 類型                                                           | 描述                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| 公司         | 字串                                                         | 帳單公司名稱。                                   |
| 位址             | [應對](utility-resources.md#address)                       | 公司或組織的帳單位址位址。 |
| primaryContact      | [連絡人](utility-resources.md#contact)                       | 公司或組織的主要連絡人。        |
| purchaseOrderNumber | 字串                                                         | 公司或組織的訂單號碼。        |
| taxId               | 字串                                                         | 公司或組織的稅務識別碼。                       |
| billingCurrency     | 字串                                                         | 公司或組織所使用的貨幣。           |
| profileType         | 字串                                                         | 夥伴配置檔案類型。                                   |
| 相關               | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。            |
| 屬性          | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。       |

 

## <a name="span-idlegalbusinessprofilespan-idlegalbusinessprofilespan-idlegalbusinessprofilelegalbusinessprofile"></a><span id="LegalBusinessProfile"/><span id="legalbusinessprofile"/><span id="LEGALBUSINESSPROFILE"/>LegalBusinessProfile


描述合作夥伴的合法商務設定檔。

| 屬性               | 類型                                                           | 描述                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 公司            | 字串                                                         | 合法的公司名稱。                                                                                                                                              |
| 位址                | [應對](utility-resources.md#address)                       | 公司或組織的位址。                                                                                                                          |
| primaryContact         | [連絡人](utility-resources.md#contact)                       | 公司或組織的主要連絡人。                                                                                                                 |
| companyApproverAddress | [應對](utility-resources.md#address)                       | 公司核准者位址。                                                                                                                                        |
| companyApproverEmail   | 字串                                                         | 公司核准者電子郵件。                                                                                                                                          |
| vettingStatus          | 字串                                                         | 調查狀態。 這個值是在[**VettingStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus)中找到的其中一個成員名稱的字串表示。           |
| vettingSubStatus       | 字串                                                         | 調查子狀態。 這個值是在[**VettingSubStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus)中找到的其中一個成員名稱的字串表示。 |
| profileType            | 字串                                                         | 夥伴配置檔案類型。                                                                                                                                            |
| 相關                  | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。                                                                                                                     |
| 屬性             | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。                                                                                                                |

 

## <a name="span-idmpnprofilespan-idmpnprofilespan-idmpnprofilempnprofile"></a><span id="MpnProfile"/><span id="mpnprofile"/><span id="MPNPROFILE"/>MpnProfile


描述合作夥伴的 Microsoft 合作夥伴網路設定檔。

| 屬性    | 類型                                                           | 描述                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | 字串                                                         | 公司或組織名稱。                     |
| mpnId       | 字串                                                         | Microsoft 合作夥伴網路識別碼。                     |
| profileType | 字串                                                         | 夥伴配置檔案類型。                             |
| 相關       | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。      |
| 屬性  | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。 |

 

## <a name="span-idorganizationprofilespan-idorganizationprofilespan-idorganizationprofileorganizationprofile"></a><span id="OrganizationProfile"/><span id="organizationprofile"/><span id="ORGANIZATIONPROFILE"/>OrganizationProfile


描述合作夥伴的組織設定檔。

| 屬性       | 類型                                                           | 描述                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | 字串                                                         | 組織的識別碼。                                                 |
| 公司    | 字串                                                         | 公司或組織的名稱。                               |
| defaultAddress | [應對](utility-resources.md#address)                       | 公司或組織的預設位址。                    |
| tenantId       | 字串                                                         | 租使用者識別碼。                                                 |
| domain         | 字串                                                         | 公司或組織的網域。                                  |
| 電子郵件          | 字串                                                         | 取得或設定父訂用帳戶。                                  |
| language       | 字串                                                         | 通訊的慣用語言。                              |
| 區域        | 字串                                                         | 通訊和貨幣的慣用文化特性，例如 "en-us"。 |
| profileType    | 字串                                                         | 夥伴配置檔案類型。                                              |
| 相關          | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。                       |
| 屬性     | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。                  |

 

## <a name="span-idsupportprofilespan-idsupportprofilespan-idsupportprofilesupportprofile"></a><span id="SupportProfile"/><span id="supportprofile"/><span id="SUPPORTPROFILE"/>SupportProfile


描述合作夥伴的支援設定檔。

| 屬性    | 類型                                                           | 描述                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| 電子郵件       | 字串                                                         | 與設定檔相關聯的電子郵件地址。        |
| 電話   | 字串                                                         | 與設定檔相關聯的電話號碼。         |
| 網站     | 字串                                                         | 支援網站。                                  |
| profileType | 字串                                                         | 夥伴配置檔案類型。                             |
| 相關       | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。      |
| 屬性  | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。 |

 

 

 




