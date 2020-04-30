---
title: 合作夥伴中心 REST 資源
description: 本節提供使用合作夥伴中心 REST API 建立要求和剖析回應所需之 JSON 元素的定義。
ms.assetid: E7C51D19-C6A7-4A4C-9F17-B4D39195972A
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e452681406a717ef618808b4b699cda5f6684931
ms.sourcegitcommit: f71c7fb2fef51ac7ca0a28717d5f7276bd20ec56
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/29/2020
ms.locfileid: "82559037"
---
# <a name="partner-center-rest-resources"></a>合作夥伴中心 REST 資源

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

本節提供使用合作夥伴中心 REST API 建立要求和剖析回應所需之 JSON 元素的定義。 如需如何使用這些元素的詳細資訊，包括範例程式碼，請參閱[案例](scenarios.md)一節和[合作夥伴中心範例](partner-center-samples.md)一節。

## <a name="in-this-section"></a>本節內容

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><a href="analytics-resources.md">分析</a></td>
<td><ul>
<li>PartnerLicensesDeploymentInsights</li>
<li>PartnerLicensesUsageInsights</li>
<li>CustomerLicensesDeploymentInsights</li>
<li>PartnerLicensesUsageInsights</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="auditing-resources.md">稽核</a></td>
<td><ul>
<li>AuditRecord</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="azure-rate-card-resources.md">Azure 費率卡片</a></td>
<td><ul>
<li>AzureRateCard</li>
<li>AzureMeter</li>
<li>AzureOfferTerm</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="azure-utilization-record-resources.md">Azure 使用率記錄</a></td>
<td><ul>
<li>AzureUtilizationRecord</li>
<li>Remove-azureresource</li>
<li>AzureInstanceData</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="cart-resources.md">購物車</a></td>
<td><ul>
<li>購物車</li>
<li>CartLineItem</li>
<li>CartError</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="conversions-resources.md">轉換</a></td>
<td><ul>
<li>轉換</li>
<li>ConversionError</li>
<li>ConversionResult</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="country-information-resources.md">CountryInformation</a></td>
<td><ul>
<li>CountryInformation</li>
<li>CountryValidationRules</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="customer-resources.md">客戶</a></td>
<td><ul>
<li>客戶</li>
<li>CustomerCompanyProfile</li>
<li>CustomerBillingProfile</li>
<li>CustomerRelationshipRequest</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="customer-usage-resources.md">客戶使用量預算</a></td>
<td><ul>
<li>CustomerMonthlyUsageRecord</li>
<li>Customerrelationshiprequest</li>
<li>PartnerUsageSummary</li>
<li>SpendingBudget</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="entitlement-resources.md">權利</a></td>
<td><ul>
<li>Entitlement</li>
<li>ReferenceOrder</li>
<li>EntitlementType</li>
<li>構件</li>
<li>ArtifactType</li>
<li>VirtualMachineReservedInstanceArtifact</li>
<li>VirtualMachineReservedInstanceArtifactDetails</li>
<li>VirtualMachineReservation</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="invoice-resources.md">發票</a></td>
<td><ul>
<li>Invoice</li>
<li>InvoiceDetail</li>
<li>InvoiceLineItem</li>
<li>InvoiceSummary</li>
<li>InvoiceSummaryDetail</li>
<li>InvoiceSummaries</li>
<li>LicenseBasedLineItem</li>
<li>UsageBasedLineItem</li>
<li>InvoiceStatement</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="license-resources.md">授權</a></td>
<td><ul>
<li>授權</li>
<li>LicenseUpdate</li>
<li>LicenseAssignment</li>
<li>LicenseWarning</li>
<li>ProductSku</li>
<li>服務方案</li>
<li>SubscribedSku</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="managed-service-resources.md">ManagedService</a></td>
<td><ul>
<li>ManagedService</li>
<li>ManagedServiceLinks</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="offer-resources.md">供應項目</a></td>
<td><ul>
<li>產品</li>
<li>OfferCategory</li>
<li>OfferLinks</li>
<li>OfferProduct</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="order-resources.md">訂單</a></td>
<td><ul>
<li>單</li>
<li>OrderLineItem</li>
<li>OrderLinks</li>
<li>OrderLineItemLinks</li>
<li>OrderStatus</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="profile-resources.md">設定檔</a></td>
<td><ul>
<li>BillingProfile</li>
<li>LegalBusinessProfile</li>
<li>MpnProfile</li>
<li>OrganizationProfile</li>
<li>SupportProfile</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="product-resources.md">產品</a></td>
<td><ul>
<li>Products</li>
<li>ItemType</li>
<li>ProductLinks</li>
<li>SKU</li>
<li>可用性</li>
<li>InventoryCheckRequest</li>
<li>InventoryItem</li>
<li>InventoryRestriction</li>
<li>為 billingcycletype</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="relationships-resources.md">人際關係</a></td>
<td><ul>
<li>PartnerRelationship</li>
<li>RelationshipRequest</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="self-serve-policy-resources.md">SelfServePolicy</a></td>
<td><ul>
<li>ServiceCostsSummary</li>
<li>ServiceCostsLineItem</li>
<li>ServiceCostsSummaryLinks</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="service-costs-resources.md">ServiceCosts</a></td>
<td><ul>
<li>ServiceCostsSummary</li>
<li>ServiceCostsLineItem</li>
<li>ServiceCostsSummaryLinks</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="service-request-resources.md">ServiceRequest</a></td>
<td><ul>
<li>ServiceRequest</li>
<li>ServiceRequestContact</li>
<li>ServiceRequestNote</li>
<li>ServiceRequestOrganization</li>
<li>SupportTopic</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="subscription-resources.md">訂閱帳戶</a></td>
<td><ul>
<li>訂用帳戶</li>
<li>SubscriptionLinks</li>
<li>SubscriptionProvisioningStatus</li>
<li>SubscriptionRegistrationStatus</li>
<li>SupportContact</li>
<li>RegisterSubscription</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="subscription-usage-resources.md">訂用帳戶使用方式</a></td>
<td><ul>
<li>SubscriptionDailyUsageRecord <em>（已過時）</em></li>
<li>SubscriptionMonthlyUsageRecord</li>
<li>SubscriptionUsageSummary</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="upgrade-resources.md">升級</a></td>
<td><ul>
<li>升級</li>
<li>UpgradeError</li>
<li>UpgradeResult</li>
<li>UserLicenseError</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="user-resources.md">使用者</a></td>
<td><ul>
<li>User</li>
<li>CustomerUser</li>
<li>UserCredentials</li>
<li>UserMember</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="utility-resources.md">公用程式資源</a></td>
<td><ul>
<li>位址</li>
<li>連絡人</li>
<li>FieldFilter</li>
<li>FileInfo</li>
<li>連結</li>
<li>PasswordProfile</li>
<li>ResourceLinks</li>
<li>ResourceAttributes</li>
<li>SecureString</li>
<li>ValidationCode</li>
</ul></td>
</tr>
</tbody>
</table>
