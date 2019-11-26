---
title: Profile resources
description: Describes the behavior of a Cloud Solution Provider's profiles.
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
# <a name="profile-resources"></a>Profile resources


**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

Describes the behavior of a Cloud Solution Provider's profiles.

## <a name="span-idbillingprofilespan-idbillingprofilespan-idbillingprofilebillingprofile"></a><span id="BillingProfile"/><span id="billingprofile"/><span id="BILLINGPROFILE"/>BillingProfile


Describes a partner's billing profile.

| 屬性            | 在工作列搜尋方塊中輸入                                                           | 說明                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| companyName         | 字串                                                         | The billing company name.                                   |
| 位址             | [Address](utility-resources.md#address)                       | The billing address address of the company or organization. |
| primaryContact      | [Contact](utility-resources.md#contact)                       | The primary contact for the company or organization.        |
| purchaseOrderNumber | 字串                                                         | The company or organization's purchase order number.        |
| taxId               | 字串                                                         | The company or organization's tax Id.                       |
| billingCurrency     | 字串                                                         | The currency used by the company or organization.           |
| profileType         | 字串                                                         | The partner profile type.                                   |
| links               | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.            |
| 屬性          | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.       |

 

## <a name="span-idlegalbusinessprofilespan-idlegalbusinessprofilespan-idlegalbusinessprofilelegalbusinessprofile"></a><span id="LegalBusinessProfile"/><span id="legalbusinessprofile"/><span id="LEGALBUSINESSPROFILE"/>LegalBusinessProfile


Describes a partner's legal business profile.

| 屬性               | 在工作列搜尋方塊中輸入                                                           | 說明                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| companyName            | 字串                                                         | The legal company name.                                                                                                                                              |
| 位址                | [Address](utility-resources.md#address)                       | The address of the company or organization.                                                                                                                          |
| primaryContact         | [Contact](utility-resources.md#contact)                       | The primary contact for the company or organization.                                                                                                                 |
| companyApproverAddress | [Address](utility-resources.md#address)                       | The company approver address.                                                                                                                                        |
| companyApproverEmail   | 字串                                                         | The company approver email.                                                                                                                                          |
| vettingStatus          | 字串                                                         | The vetting status. This value is the string representation of the one of the member names found in [**VettingStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus).           |
| vettingSubStatus       | 字串                                                         | The vetting sub-status. This value is the string representation of the one of the member names found in [**VettingSubStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus). |
| profileType            | 字串                                                         | The partner profile type.                                                                                                                                            |
| links                  | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.                                                                                                                     |
| 屬性             | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                                                                                                                |

 

## <a name="span-idmpnprofilespan-idmpnprofilespan-idmpnprofilempnprofile"></a><span id="MpnProfile"/><span id="mpnprofile"/><span id="MPNPROFILE"/>MpnProfile


Describes a partner's Microsoft Partner Network profile.

| 屬性    | 在工作列搜尋方塊中輸入                                                           | 說明                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | 字串                                                         | The company or organization name.                     |
| mpnId       | 字串                                                         | The Microsoft Partner Network Id.                     |
| profileType | 字串                                                         | The partner profile type.                             |
| links       | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.      |
| 屬性  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile. |

 

## <a name="span-idorganizationprofilespan-idorganizationprofilespan-idorganizationprofileorganizationprofile"></a><span id="OrganizationProfile"/><span id="organizationprofile"/><span id="ORGANIZATIONPROFILE"/>OrganizationProfile


Describes a partner's organization profile.

| 屬性       | 在工作列搜尋方塊中輸入                                                           | 說明                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | 字串                                                         | The organization's Id.                                                 |
| companyName    | 字串                                                         | The name of the company or organization.                               |
| defaultAddress | [Address](utility-resources.md#address)                       | The default address of the company or organization.                    |
| tenantId       | 字串                                                         | The tenant identifier.                                                 |
| domain         | 字串                                                         | The company or organization's domain.                                  |
| 電子郵件          | 字串                                                         | Gets or sets the parent subscription.                                  |
| language       | 字串                                                         | The preferred language for communication.                              |
| culture        | 字串                                                         | The preferred culture for communication and currency, such as "en-us". |
| profileType    | 字串                                                         | The partner profile type.                                              |
| links          | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.                       |
| 屬性     | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                  |

 

## <a name="span-idsupportprofilespan-idsupportprofilespan-idsupportprofilesupportprofile"></a><span id="SupportProfile"/><span id="supportprofile"/><span id="SUPPORTPROFILE"/>SupportProfile


Describes a partner's support profile.

| 屬性    | 在工作列搜尋方塊中輸入                                                           | 說明                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| 電子郵件       | 字串                                                         | The email address associated with the profile.        |
| 電話   | 字串                                                         | The phone number associated with the profile.         |
| 網站     | 字串                                                         | The support website.                                  |
| profileType | 字串                                                         | The partner profile type.                             |
| links       | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.      |
| 屬性  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile. |

 

 

 




