---
title: Partner Center REST resources
description: This section provides definitions for the JSON elements needed to create requests and parse responses using the Partner Center REST API.
ms.assetid: E7C51D19-C6A7-4A4C-9F17-B4D39195972A
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 4be969f9bced111c3ba95f773920f4aecfc4942d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486818"
---
# <a name="partner-center-rest-resources"></a>Partner Center REST resources


**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

This section provides definitions for the JSON elements needed to create requests and parse responses using the Partner Center REST API. For more information about how to use these elements, including sample code, see the [Scenarios](scenarios.md) section and the [Partner Center samples](partner-center-samples.md) section.

## <a name="span-idin_this_sectionspan-idin_this_sectionspan-idin_this_sectionin-this-section"></a><span id="In_this_section"/><span id="in_this_section"/><span id="IN_THIS_SECTION"/>In this section


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
<td><a href="auditing-resources.md">Auditing</a></td>
<td><ul>
<li>AuditRecord</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="azure-rate-card-resources.md">Azure Rate Card</a></td>
<td><ul>
<li>AzureRateCard</li>
<li>AzureMeter</li>
<li>AzureOfferTerm</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="azure-utilization-record-resources.md">Azure Utilization Record</a></td>
<td><ul>
<li>AzureUtilizationRecord</li>
<li>AzureResource</li>
<li>AzureInstanceData</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="cart-resources.md">Cart</a></td>
<td><ul>
<li>Cart</li>
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
<td><a href="customer-resources.md">Customer</a></td>
<td><ul>
<li>客戶</li>
<li>CustomerCompanyProfile</li>
<li>CustomerBillingProfile</li>
<li>CustomerRelationshipRequest</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="customer-usage-resources.md">Customer Usage Budgeting</a></td>
<td><ul>
<li>CustomerMonthlyUsageRecord</li>
<li>CustomerUsageSummary</li>
<li>PartnerUsageSummary</li>
<li>SpendingBudget</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="entitlement-resources.md">Entitlement</a></td>
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
<td><a href="invoice-resources.md">Invoice</a></td>
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
<td><a href="license-resources.md">License</a></td>
<td><ul>
<li>授權</li>
<li>LicenseUpdate</li>
<li>LicenseAssignment</li>
<li>LicenseWarning</li>
<li>ProductSku</li>
<li>ServicePlan</li>
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
<li>優惠供應</li>
<li>OfferCategory</li>
<li>OfferLinks</li>
<li>OfferProduct</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="order-resources.md">順序</a></td>
<td><ul>
<li>順序</li>
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
<td><a href="product-resources.md">Products</a></td>
<td><ul>
<li>產品</li>
<li>ItemType</li>
<li>ProductLinks</li>
<li>Sku</li>
<li>可用性</li>
<li>InventoryCheckRequest</li>
<li>InventoryItem</li>
<li>InventoryRestriction</li>
<li>BillingCycleType</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="relationships-resources.md">Relationships</a></td>
<td><ul>
<li>PartnerRelationship</li>
<li>RelationshipRequest</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="service-costs-resources.md">ServiceCosts</a></td>
<td><ul>
<li>ServiceCostsSummary</li>
<li>ServiceCostsLineItem</li>
<li>ServiceCostsSummaryLinks</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="service-request-resources.md">ServiceRequest</a></td>
<td><ul>
<li>ServiceRequest</li>
<li>ServiceRequestContact</li>
<li>ServiceRequestNote</li>
<li>ServiceRequestOrganization</li>
<li>SupportTopic</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="subscription-resources.md">Subscription</a></td>
<td><ul>
<li>訂閱</li>
<li>SubscriptionLinks</li>
<li>SubscriptionProvisioningStatus</li>
<li>SubscriptionRegistrationStatus</li>
<li>SupportContact</li>
<li>RegisterSubscription</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="subscription-usage-resources.md">Subscription Usage</a></td>
<td><ul>
<li>SubscriptionDailyUsageRecord <em>(Obsolete)</em></li>
<li>SubscriptionMonthlyUsageRecord</li>
<li>SubscriptionUsageSummary</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="upgrade-resources.md">升級</a></td>
<td><ul>
<li>升級</li>
<li>UpgradeError</li>
<li>UpgradeResult</li>
<li>UserLicenseError</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="user-resources.md">User</a></td>
<td><ul>
<li>使用者</li>
<li>CustomerUser</li>
<li>UserCredentials</li>
<li>UserMember</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="utility-resources.md">Utility Resources</a></td>
<td><ul>
<li>Address</li>
<li>Contact</li>
<li>FieldFilter</li>
<li>FileInfo</li>
<li>Link</li>
<li>PasswordProfile</li>
<li>ResourceLinks</li>
<li>ResourceAttributes</li>
<li>SecureString</li>
<li>ValidationCode</li>
</ul></td>
</tr>
</tbody>
</table>
