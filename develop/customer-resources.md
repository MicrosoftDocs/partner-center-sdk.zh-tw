---
title: Customer resources
description: Customer resources that represent a customer or reseller.
ms.assetid: C7EC2657-62F2-43B3-B171-2F74498D45E0
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 09dd70431b34ad5c63820931113a71908b24acd0
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489698"
---
# <a name="customer-resources"></a>Customer resources

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

## <a name="customer"></a>客戶

The **Customer** resource represents a customer or reseller. Most broadly, a customer resouce can be any person, employee, or organization that wishes to do business with Microsoft and Microsoft's resellers. Customers also have a company profile and a billing profile.

>[!NOTE]
>The **Customer** resource has a rate limit of 500 requests per minute per tenant identifier.

| 屬性              | 在工作列搜尋方塊中輸入                                                             | 說明                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | 字串                                                           | The customer ID.                                                                                                                             |
| commerceId            | 字串                                                           | The commerce ID.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | Additional information about the company or organization.                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | Additional information used for billing.                                                                                                     |
| relationshipToPartner | 字串                                                           | Defines the licensing program that the partner uses for this customer: "none", "reseller", "advisor", "syndication" or "microsoft\_support". |
| allowDelegatedAccess  | boolean                                                          | Whether the partner has been granted delegated admin privileges by this customer.                                                            |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | The user credentials.                                                                                                                        |
| customDomains         | array of strings                                                 | List of custom domains of a customer.                                                                                                        |
| associatedPartnerId   | 字串                                                           | The indirect reseller associated to this customer account. This value can be set only by indirect CSP partners.                              |
| links                 | [ResourceLinks](utility-resources.md#resourcelinks)             | The resource links contained within the profile.                                                                                             |
| 屬性            | [ResourceAttributes](utility-resources.md#resourceattributes)   | The metadata attributes corresponding to the profile.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

The **CustomerCompanyProfile** resource is additional information about the company or organization.

| 屬性    | 在工作列搜尋方塊中輸入                                                           | 說明                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | 字串                                                         | The customer's tenant identifier for Azure AD. This is also called a MicrosoftID. |
| domain      | 字串                                                         | The customer's name, such as contoso.onmicrosoft.com.                             |
| companyName | 字串                                                         | The name of the company or organization.                                          |
| links       | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links contained within the profile.                                  |
| 屬性  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                             |

## <a name="customerbillingprofile"></a>CustomerBillingProfile

The **CustomerBillingProfile** resource is additional information used for billing the customer.

| 屬性       | 在工作列搜尋方塊中輸入                                                           | 說明                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | 字串                                                         | The profile identifier.                                                                                                                                |
| firstName      | 字串                                                         | The first name of the billing contact at the customer's company. This is the person that invoices and other billing communication will be directed to. |
| lastName       | 字串                                                         | The last name of the billing contact.                                                                                                                  |
| 電子郵件          | 字串                                                         | The billing contact's email address                                                                                                                    |
| culture        | 字串                                                         | Their preferred culture for communication and currency, such as "en-us".                                                                               |
| language       | 字串                                                         | Their preferred language for communication.                                                                                                            |
| companyName    | 字串                                                         | The name of the company or organization.                                                                                                               |
| defaultAddress | [Address](utility-resources.md#address)                       | The address that bills are sent to, where the billing contact works.                                                                                   |
| links          | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links contained within the profile.                                                                                                       |
| 屬性     | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

The **CustomerRelationshipRequest** resource contains the URL used by the customer to establish a reseller relationship with a partner.

| 屬性   | 在工作列搜尋方塊中輸入                                                           | 說明                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| URL        | 字串                                                         | The URL used by the customer to establish a relationship with a partner. |
| 屬性 | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the relationship request.       |