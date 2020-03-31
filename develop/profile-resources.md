---
title: 設定檔資源
description: 描述雲端解決方案提供者設定檔的行為。
ms.assetid: 42F2959B-D70D-41A7-9A50-E22A2356A339
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e2f7813ef3e41c06b7575e4119a364cb4e037e9b
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416323"
---
# <a name="profile-resources"></a>設定檔資源


**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

描述雲端解決方案提供者設定檔的行為。

## <a name="span-idbillingprofilespan-idbillingprofilespan-idbillingprofilebillingprofile"></a><span id="BillingProfile"/><span id="billingprofile"/><span id="BILLINGPROFILE"/>BillingProfile


描述合作夥伴的帳單設定檔。

| 屬性            | 類型                                                           | 描述                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| 公司         | string                                                         | 帳單公司名稱。                                   |
| 位址             | [地址](utility-resources.md#address)                       | 公司或組織的帳單位址位址。 |
| primaryContact      | [Contact](utility-resources.md#contact)                       | 公司或組織的主要連絡人。        |
| purchaseOrderNumber | string                                                         | 公司或組織的訂單號碼。        |
| taxId               | string                                                         | 公司或組織的稅務識別碼。                       |
| billingCurrency     | string                                                         | 公司或組織所使用的貨幣。           |
| profileType         | string                                                         | 夥伴配置檔案類型。                                   |
| 連結               | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。            |
| 屬性          | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。       |

 

## <a name="span-idlegalbusinessprofilespan-idlegalbusinessprofilespan-idlegalbusinessprofilelegalbusinessprofile"></a><span id="LegalBusinessProfile"/><span id="legalbusinessprofile"/><span id="LEGALBUSINESSPROFILE"/>LegalBusinessProfile


描述合作夥伴的合法商務設定檔。

| 屬性               | 類型                                                           | 描述                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 公司            | string                                                         | 合法的公司名稱。                                                                                                                                              |
| 位址                | [地址](utility-resources.md#address)                       | 公司或組織的位址。                                                                                                                          |
| primaryContact         | [Contact](utility-resources.md#contact)                       | 公司或組織的主要連絡人。                                                                                                                 |
| companyApproverAddress | [地址](utility-resources.md#address)                       | 公司核准者位址。                                                                                                                                        |
| companyApproverEmail   | string                                                         | 公司核准者電子郵件。                                                                                                                                          |
| vettingStatus          | string                                                         | 調查狀態。 這個值是在[**VettingStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus)中找到的其中一個成員名稱的字串表示。           |
| vettingSubStatus       | string                                                         | 調查子狀態。 這個值是在[**VettingSubStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus)中找到的其中一個成員名稱的字串表示。 |
| profileType            | string                                                         | 夥伴配置檔案類型。                                                                                                                                            |
| 連結                  | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。                                                                                                                     |
| 屬性             | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。                                                                                                                |

 

## <a name="span-idmpnprofilespan-idmpnprofilespan-idmpnprofilempnprofile"></a><span id="MpnProfile"/><span id="mpnprofile"/><span id="MPNPROFILE"/>MpnProfile


描述合作夥伴的 Microsoft 合作夥伴網路設定檔。

| 屬性    | 類型                                                           | 描述                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | string                                                         | 公司或組織名稱。                     |
| mpnId       | string                                                         | Microsoft 合作夥伴網路識別碼。                     |
| profileType | string                                                         | 夥伴配置檔案類型。                             |
| 連結       | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。      |
| 屬性  | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。 |

 

## <a name="span-idorganizationprofilespan-idorganizationprofilespan-idorganizationprofileorganizationprofile"></a><span id="OrganizationProfile"/><span id="organizationprofile"/><span id="ORGANIZATIONPROFILE"/>OrganizationProfile


描述合作夥伴的組織設定檔。

| 屬性       | 類型                                                           | 描述                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | string                                                         | 組織的識別碼。                                                 |
| 公司    | string                                                         | 公司或組織的名稱。                               |
| defaultAddress | [地址](utility-resources.md#address)                       | 公司或組織的預設位址。                    |
| tenantId       | string                                                         | 租使用者識別碼。                                                 |
| domain         | string                                                         | 公司或組織的網域。                                  |
| 電子郵件          | string                                                         | 取得或設定父訂用帳戶。                                  |
| 語言       | string                                                         | 通訊的慣用語言。                              |
| culture (文化特性)        | string                                                         | 通訊和貨幣的慣用文化特性，例如 "en-us"。 |
| profileType    | string                                                         | 夥伴配置檔案類型。                                              |
| 連結          | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。                       |
| 屬性     | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。                  |

 

## <a name="span-idsupportprofilespan-idsupportprofilespan-idsupportprofilesupportprofile"></a><span id="SupportProfile"/><span id="supportprofile"/><span id="SUPPORTPROFILE"/>SupportProfile


描述合作夥伴的支援設定檔。

| 屬性    | 類型                                                           | 描述                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| 電子郵件       | string                                                         | 與設定檔相關聯的電子郵件地址。        |
| 電話   | string                                                         | 與設定檔相關聯的電話號碼。         |
| 網站     | string                                                         | 支援網站。                                  |
| profileType | string                                                         | 夥伴配置檔案類型。                             |
| 連結       | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至設定檔的資源連結。      |
| 屬性  | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至設定檔的中繼資料屬性。 |

 

 

 




