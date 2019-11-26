---
title: Invoice resources
description: Multiple invoice-related resources are available through the Partner Center APIs. These resources are related to invoice and line item details.
ms.assetid: FDD151CC-3473-46DF-A422-265DCBC8A498
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 1eb6175538bd4175e4ba1ff8a5641bdce3b0fa36
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486938"
---
# <a name="invoice-resources"></a>Invoice resources

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

The following invoice-related resources are available through the Partner Center APIs.

## <a name="invoice"></a>Invoice

| 屬性 | 在工作列搜尋方塊中輸入 | 說明 |
| -------- | ---- | ----------- |
| id | 字串 | The invoice identifier. |
| invoiceDate | string in UTC date-time format | The date the invoice was generated. |
| billingPeriodStartDate | string in UTC date-time format | Billing period start date in UTC. |
| billingPeriodEndDate | string in UTC date-time format   | Billing period end date in UTC. |
| totalCharges | 數目 | The total charges. Includes charges for transactions and any adjustments.     |
| paidAmount | 數目  | The amount paid by the partner. Negative if a payment was received.  |
| currencyCode | 字串  | A code that indicates the currency used for all invoice item amounts and totals. |
| currencySymbol  | 字串 | The currency symbol used for all invoice item amounts and totals. |
| pdfDownloadLink | 字串  | A link to download the invoice in PDF format. This link is not returned as part of the search results, and is populated only if the invoice is accessed by ID. This link auto-expires in 30 minutes. |
| invoiceDetails  | array of [InvoiceDetail](#invoicedetail) objects  | The invoice details.  |
| amendments      | array of [Invoice](#invoice) objects   | The amendments to this invoice.  |
| documentType    | 字串 | The document type of the invoice: "Credit Note", "Invoice". |
| amendsOf        | 字串 | The reference number of the document of which this document is an amendment.  |
| invoiceType     | 字串  | The type of invoice: "recurring", "one\_time".   |
| links           | [ResourceLinks](utility-resources.md#resourcelinks)  | The resource links.  |
| 屬性      | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.  |

## <a name="invoicedetail"></a>InvoiceDetail

An invoice contains a collection of billed items, and each item is represented by an InvoiceDetail resource.

| 屬性            | 在工作列搜尋方塊中輸入                                                           | 說明                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | 字串                                                         | The type of invoice detail: "none", "usage\_line\_items", "billing\_line\_items". |
| billingProvider     | 字串                                                         | The billing provider: "none", "office", "azure" or "azure\_data\_market".         |
| links               | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links.                                                               |
| 屬性          | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

Each individual charge within an invoice is represented as an InvoiceLineItem.

| 屬性            | 在工作列搜尋方塊中輸入                                                           | 說明                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | 字串                                                         | The type of invoice line item: "none", "usage\_line\_items", "billing\_line\_items". |
| billingProvider     | 字串                                                         | The billing provider: "none", "office", "azure" or "azure\_data\_market".            |
| 屬性          | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                             |

## <a name="invoicesummary"></a>InvoiceSummary

Describes a summary of the balance and total charges of an invoice.

| 屬性                 | 在工作列搜尋方塊中輸入                                                           | 說明                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| balanceAmount            | 數目                                                         | The balance of the invoice. This is the total amount of unpaid bills. |
| currencyCode             | 字串                                                         | A code that indicates the currency used for the balance amount.       |
| currencySymbol           | 字串                                                         | The currency symbol used.                                             |
| accountingDate           | string in UTC date-time format                                 | The date the balance amount was last updated.                         |
| firstInvoiceCreationDate | string in UTC date-time format                                 | The date the first invoice for the customer was created.              |
| lastPaymentDate          | string in UTC date-time format                                 | The date of the last payment.                                         |
| lastPaymentAmount        | 數目                                                         | The amount of the last payment.                                       |
| latestInvoiceDate        | string in UTC date-time format                                 | The date the last invoice for the customer was created.               |
| details                  | array of [InvoiceSummaryDetail](#invoicesummarydetail) objects | The invoice summary detail.                                           |
| links                    | [ResourceLinks](utility-resources.md#resourcelinks)            | The resource links.                                                   |
| 屬性               | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

Represent a summary of the individual details for an invoice type (for example, recurring, one\_time).

| 屬性            | 在工作列搜尋方塊中輸入                                                           | 說明                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType         | 字串                                                         | The type of invoice: "recurring", "one\_time".                                       |
| summary             | [InvoiceSummary](#invoicesummary) object                       | The summary of the invoice per invoice type.                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

Represent a collection of type [InvoiceSummary](#invoicesummary) that contain the individual details for an invoice type per currency.  

| 屬性            | 在工作列搜尋方塊中輸入                                                           | 說明                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | array of [InvoiceSummary](#invoicesummary) objects             | The summary of the invoice per invoice type per currency.                            |

## <a name="licensebasedlineitem"></a>LicenseBasedLineItem

Represents an invoice billing line item for licensed based subscriptions.

| 屬性                 | 在工作列搜尋方塊中輸入                                                           | 說明                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| amount                   | 字串                                                         | Gets or sets the total amount. Total amount = unit price * quantity.  |
| 屬性               | 字串                                                         | Gets the attributes.                                                  |
| billingCycleType         | 字串                                                         | Gets or sets the billing cycle type.                                  |
| billingProvider          | 字串                                                         | Gets the billing provider.                                            |
| chargeEndDate            | string in UTC date-time format                                 | Gets or sets the end date for the charge.                             |
| chargeStartDate          | string in UTC date-time format                                 | Gets or sets the start date for the charge.                           |
| chargeType               | 字串                                                         | Gets or sets the type of charge.                                      |
| currency                 | 字串                                                         | Gets or sets the currency used for this line item.                    |
| customerId               | 字串                                                         | Gets or sets the customer unique identifier in the Microsoft billing platform.  |
| customerName             | string in UTC date-time format                                 | Gets or sets the customer name.                                       |
| domainName               | 字串                                                         | Gets or sets domain name.                                             |
| durableOfferId           | 字串                                                         | Gets or sets the durable offer unique identifier.                     |
| invoiceLineItemType      | 字串                                                         | Gets the type of invoice line item.                                   |
| mpnId                    | 數目                                                         | Gets or sets the MPN ID associated to this line item. For direct resellers, this is the MPN Id of the reseller. For indirect resellers, this is the MPN ID of the Value Added Reseller (VAR).                                   |
| offerId                  | 字串                                                         | Gets or sets the offer unique identifier.                             |
| offerName                | 字串                                                         | Gets or sets the offer name.                                          |
| orderId                  | 字串                                                         | Gets or sets the order unique identifier.                             |
| partnerId                | 字串                                                         | Gets or sets the partner Azure active directory tenant ID.            |
| quantity                 | 數目                                                         | Gets or sets the number of units associated with this line item.      |
| subscriptionDescription  | 字串                                                         | Gets or sets the subscription description.                            |
| subscriptionEndDate      | string in UTC date-time format                                 | Gets or sets the date when subscription expires.                      |
| subscriptionId           | 字串                                                         | Gets or sets the subscription unique identifier.                      |
| subscriptionName         | 字串                                                         | Gets or sets the subscription name.                                   |
| subscriptionStartDate    | string in UTC date-time format                                 | Gets or sets the date when the subscription starts.                   |
| subtotal                 | 數目                                                         | Gets or sets the amount after discount.                               |
| syndicationPartnerSubscriptionNumber | 字串                                             | Gets or sets the syndication partner subscription number.             |
| tax                      | 數目                                                         | Gets or sets the taxes charged.                                       |
| tier2MpnId               | 數目                                                         | Gets or sets the MPN ID of the Tier 2 partner associated to this line item. |
| totalForCustomer         | 數目                                                         | Gets or sets the total amount after discount and tax.                 |
| totalOtherDiscount       | 數目                                                         | Gets or sets the discount associated with this purchase.              |
| unitPrice                | 數目                                                         | Gets or sets the unit price.                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

Represents an invoice billing line item for usage based subscriptions.

| 屬性                 | 在工作列搜尋方塊中輸入                                                           | 說明                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| 屬性               | 字串                                                         | Gets the attributes.                                                  |
| billingCycleType         | 字串                                                         | Gets or sets the billing cycle type.                                  |
| billingProvider          | 字串                                                         | Gets the billing provider.                                            |
| chargeEndDate            | string in UTC date-time format                                 | Gets or sets the end date for the charge.                             |
| chargeStartDate          | string in UTC date-time format                                 | Gets or sets the start date for the charge.                           |
| chargeType               | 字串                                                         | Gets or sets the type of charge.                                      |
| consumedQuantity         | 數目                                                         | Gets or sets the total units consumed.                                |
| consumptionDiscount      | 字串                                                         | Gets or sets the discount on consumption.                             |
| consumptionPrice         | 字串                                                         | Gets or sets the price of quantity consumed.                          |
| currency                 | 字串                                                         | Gets or sets the currency associated with the prices.                 |
| customerName             | 字串                                                         | Gets or sets the customer name.                                       |
| customerId               | 字串                                                         | Gets or sets the customer unique identifier.                          |
| detailLineItemId         | 數目                                                         | Gets or sets the detail line item ID. Uniquely identifies the line items for cases where calculation is different for units consumed. Example: Total consumed = 1338, 1024 is charged with one rate, 314 is charge with a different rate.        |
| domainName               | 字串                                                         | Gets or sets domain name.                                             |
| includedQuantity         | 數目                                                         | Gets or sets the units included in the order.                         |
| invoiceLineItemType      | 字串                                                         | Gets the type of invoice line item.                                   |
| invoiceNumber            | 字串                                                         | Gets or sets the invoice number.                                      |
| listPrice                | 數目                                                         | Gets or sets the price of each unit.                                  |
| mpnId                    | 數目                                                         | Gets or sets the MPN ID associated to this line item. For direct resellers, this is the MPN ID of the reseller. For indirect resellers, this is the MPN ID of the Value Added Reseller (VAR).                                   |
| orderId                  | 字串                                                         | Gets or sets the order unique identifier.                             |
| overageQuantity          | 數目                                                         | Gets or sets the quantity consumed above allowed usage.               |
| partnerBillableAccountId | 字串                                                         | Gets or sets the partner billable account ID.                         |
| partnerId                | 字串                                                         | Gets or sets the partner Azure active directory tenant ID.            |
| partnerName              | 字串                                                         | Gets or sets the partner's name.                                      |
| postTaxEffectiveRate     | 數目                                                         | Gets or sets the effective price after taxes.                         |
| postTaxTotal             | 數目                                                         | Gets or sets the total charges after tax. Pretax Charges + Tax Amount |
| preTaxCharges            | 數目                                                         | Gets or sets the price charged before taxes.                          |
| preTaxEffectiveRate      | 數目                                                         | Gets or sets the effective price before taxes.                        |
| region                   | 字串                                                         | Gets or sets the region associated with the resource instance.        |
| resourceGuid             | 字串                                                         | Gets or sets the resource identifier.                                 |
| resourceName             | 字串                                                         | Gets or sets the resource name. Example: Database (GB/month).         |
| serviceName              | 字串                                                         | Gets or sets the service name. Example: Azure Data Service.           |
| serviceType              | 字串                                                         | Gets or sets the service type. Example: Azure SQL Azure DB.           |
| sku                      | 字串                                                         | Gets or sets the service SKU.                                         |
| subscriptionDescription  | 字串                                                         | Gets or sets the subscription description.                            |
| subscriptionId           | 字串                                                         | Gets or sets the subscription unique identifier.                      |
| subscriptionName         | 字串                                                         | Gets or sets the subscription name.                                   |
| taxAmount                | 數目                                                         | Gets or sets the amount of tax charged.                               |
| tier2MpnId               | 數目                                                         | Gets or sets the MPN ID of the Tier 2 partner associated to this line item. |
| 單位                     | 字串                                                         | Gets or sets the unit of measure for Azure usage.                     |

## <a name="invoicestatement"></a>InvoiceStatement

Represents the operations available on an invoice statement in application/pdf.

| 屬性                 | 在工作列搜尋方塊中輸入                                                           | 說明                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | 物件                                                         | ByteArrayContent with contentType = application/pdf.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

Represents an invoice billing line item for licensed-based subscriptions.

| 屬性 | 在工作列搜尋方塊中輸入 | 說明 |
| --- | --- | --- |
| PartnerId | 字串 | Gets or sets the partner tenant ID. |
| CustomerId | 字串 | Gets or sets the customer tenant ID. |
| CustomerName | 字串 | Gets or sets the customer name. |
| CustomerDomainName | 字串 | Gets or sets the customer domain name. |
| CustomerCountry | 字串 | Gets or sets the customer country. |
| InvoiceNumber | 字串 | Gets or sets the invoice number. |
| MpnId | 字串 | Gets or sets the MPN ID associated to this line item. |
| ResellerMpnId | 整數 | Gets or sets the order unique identifier. |
| OrderDate | DateTime | Gets or sets the date when order created. |
| ProductId | 字串 | Gets or sets the product unique identifier. |
| SkuId | 字串 | Gets or sets the SKU unique identifier. |
| AvailabilityId | 字串 | Gets or sets the availability unique identifier. |
| ProductName | 字串 | Gets or sets the product name. |
| SkuName | 字串 | Gets or sets the SKU name. |
| ChargeType | 字串 | Gets or sets the type of charge. |
| UnitPrice | 十進位 | Gets or sets the unit price. |
| EffectiveUnitPrice | 十進位 | Gets or sets the effective unit price. |
| UnitType | 字串 | Gets or sets the unit type. |
| 數量 | 整數 | Gets or sets the number of units associated with this line item. |
| 小計 | 十進位 | Gets or sets the amount after discount. |
| TaxTotal | 十進位 | Gets or sets the taxes charged. |
| TotalForCustomer | 十進位 | Gets or sets the total amount after discount and tax. |
| Currency | 字串 | Gets or sets the currency used for this line item. |
| PublisherName | 字串 | Gets or sets the publisher name associated with this purchase. |
| PublisherId | 字串 | Gets or sets the publisher ID associated with this purchase. |
| SubscriptionDescription | 字串 | Gets or sets the subscription description associated with this purchase. |
| SubscriptionId | 字串 | Gets or sets the subscription ID associated with this purchase. |
| ChargeStartDate | DateTime | Gets or sets the charge start date associated with this purchase. |
| ChargeEndDate | DateTime | Gets or sets the charge end date associated with this purchase. |
| TermAndBillingCycle | 字串 | Gets or sets the term and billing cycle associated with this purchase. |
| AlternateId | 字串 | Gets or sets the Alternate ID (quote ID). |
| PriceAdjustmentDescription | 字串 | Gets or sets the price adjustment description. |
| DiscountDetails | 字串 |  **過時**。 Gets or sets the discount details associated with this purchase. |
| PricingCurrency | 字串 | Gets or sets the pricing currency code. |
| PCToBCExchangeRate | 十進位 | Gets or sets the pricing currency to the billing currency exchange rate. |
| PCToBCExchangeRateDate | DateTime | Gets or sets the exchange rate date at which the pricing currency to the billing currency exchange rate was determined. |
| BillableQuantity | 十進位 | Gets or sets the units purchased. For each design column named as **BillableQuantity**. |
| MeterDescription | 字串 | Gets or sets the meter description for consumption line item. |
| BillingFrequency | 字串 | Gets or sets the billing frequency. |
| InvoiceLineItemType | InvoiceLineItemType | Returns the type of invoice line item. |
| BillingProvider | BillingProvider | Returns the billing provider. |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

Represents unbilled, billed reconciliation line items for daily rated usage.

| 屬性 | 在工作列搜尋方塊中輸入 | 說明 |
| --- | --- | --- |
| PartnerId | 字串 | Gets or sets the partner tenant ID. |
| PartnerName | 字串 | Gets or sets the partner name. |
| CustomerId | 字串 | Gets or sets the tenant ID of the customer that usage belongs to. |
| CustomerName | 字串 | Gets or sets the name of the customer company that usage belongs to. |
| CustomerDomainName | 字串 | Gets or sets the domain name of the customer that usage belongs to. |
| InvoiceNumber | 字串 | Gets or sets the ID of the invoice that usage belongs to. |
| ProductId | 字串 | Gets or sets the product unique identifier. |
| SkuId | 字串 | Gets or sets the SKU unique identifier. |
| AvailabilityId | 字串 | Gets or sets the availability unique identifier. |
| SkuName | 字串 | Gets or sets the SKU name for the service. |
| ProductName | 字串 | Gets or sets the name of the product. |
| PublisherName | 字串 | Gets or sets the name of publisher. |
| PublisherId | 字串 | Gets or sets the ID of the publisher. |
| SubscriptionId | 字串 | Gets or sets the subscription ID. |
| SubscriptionDescription | 字串 | Gets or sets the subscription description. |
| ChargeStartDate | DateTime | Gets or sets the charge start date. |
| ChargeEndDate | DateTime | Gets or sets the charge end date. |
| UsageDate | DateTime | Gets or sets the usage date. |
| MeterType | 字串 | Gets or sets the meter type. |
| MeterCategory | 字串 | Gets or sets the meter category. |
| MeterId | 字串 | Gets or sets the  meter ID (GUID). |
| MeterSubCategory | 字串 | Gets or sets the meter sub category. |
| MeterName | 字串 | Gets or sets the meter name. |
| MeterRegion | 字串 | Gets or sets the meter region. |
| UnitOfMeasure | 字串 | Gets or sets the unit of measure. |
| ResourceLocation | 字串 | Gets or sets the location of resource. |
| ConsumedService | 字串 | Gets or sets the consumed service name. |
| ResourceGroup | 字串 | Gets or sets the name of resource group. |
| ResourceUri | 字串 | Gets or sets the uri of the resource instance that the usage is about. |
| 標記 | 字串 | Gets or sets the customer added tags. |
| AdditionalInfo | 字串 | Gets or sets the service-specific metadata. For example, an image type for a virtual machine. |
| ServiceInfo1 | 字串 | Gets or sets internal Azure Service Metadata. |
| ServiceInfo2 | 字串 | Gets or sets service information for example, an image type for a virtual machine and ISP name for ExpressRoute. |
| CustomerCountry | 字串 | Gets or sets the country of the customer. |
| MpnId | 字串 | Gets or sets the MPN ID associated to this line item. |
| ResellerMpnId | 字串 | Gets or sets the Reseller MPN ID of the Tier 2 partner associated to this line item. |
| ChargeType | 字串 | Gets or sets the type of charge. |
| UnitPrice | 十進位 | Gets or sets the price of unit. |
| 數量 | 十進位 | Gets or sets the quantity of usage. |
| UnitType | 字串 | Gets or sets the unit type (such as 1 hour). |
| BillingPreTaxTotal | 十進位 | Gets or sets the extended cost or total cost before tax in local currency of the customer or billing currency. |
| BillingCurrency | 字串 | Gets or sets ISO currency in which the meter is charged in local currency of the customer or billing currency. |
| PricingPreTaxTotal | 十進位 | Gets or sets the extended cost or total cost before tax in USD or catalog currency used for rating. |
| PricingCurrency | 字串 | Gets or sets ISO currency in which the meter is charged in USD or catalog currency used for rating. |
| EntitlementId | 字串 | Gets or sets the entitlement (Azure subscription) ID. |
| EntitlementDescription | 字串 | Gets or sets the entitlement (Azure subscription) description. |
| PCToBCExchangeRate | 字串 | Gets or sets the pricing currency to the billing currency exchange rate. |
| PCToBCExchangeRateDate | DateTime | Gets or sets the pricing currency to the billing currency exchange rate date. |
| EffectiveUnitPrice | 十進位 | Gets or sets the effective unit price. |
| RateOfPartnerEarnedCredit | 十進位 | Gets or sets the rate of partner earned credit. |
| hasPartnerEarnedCredit | bool | Gets or sets is partner earned credit applied. |
| InvoiceLineItemType | InvoiceLineItemType | Returns the type of invoice line item. |
| BillingProvider | BillingProvider | Returns the billing provider. |
