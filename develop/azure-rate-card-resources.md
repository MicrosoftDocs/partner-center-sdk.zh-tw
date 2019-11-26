---
title: Azure rate card resources
description: The Azure Rate Card provides real-time prices for Azure offers.
ms.assetid: A42B4FFA-278E-41FF-B51E-E48C2CA70EEF
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e81debb15c30ba024d897a00075bffe28be3acaf
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489138"
---
# <a name="azure-rate-card-resources"></a>Azure rate card resources

適用於：

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

The Azure Rate Card provides real-time prices for Azure offers. Azure pricing is quite dynamic and changes frequently. Microsoft publishes updates on Partner Center, but the REST API provides the fastest way for Cloud Solution Provider partners to get current prices.

To track usage and help predict your monthly bill and the bills for individual customers, you can combine a Rate Card query to [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md) with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).

Prices differ by market and currency, and this API takes location into consideration. By default, it uses your partner profile settings in Partner Center and your browser language, but those are customizable. This is especially relevant if you manage sales in multiple markets from a single, centralized office.

## <a name="azureratecard"></a>AzureRateCard

Describes the properties of an Azure Rate Card resource.

| 屬性      | 在工作列搜尋方塊中輸入                                      | 說明                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | 字串                                    | The currency in which the rates are provided.                     |
| isTaxIncluded | boolean                                   | All rates are pretax, so this will always be returned as "false". |
| locale        | 字串                                    | The culture in which the resource information is localized.       |
| meters        | array of objects                          | Array of [AzureMeter](#azuremeter) objects.                       |
| offerTerms    | array of objects                          | Array of [AzureOfferTerm](#azureofferterm) objects.               |
| 屬性    | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Contains "objectType": "AzureRateCard"   |


### <a name="operations-on-the-azureratecard-resource"></a>Operations on the AzureRateCard resource

- [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| 屬性         | 在工作列搜尋方塊中輸入             | 說明                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | 字串           | Meter's unique identifier.                                                                    |
| name             | 字串           | Friendly name of the meter.                                                                   |
| rates            | 物件           | Meter rates. The key is the meter quantity (string) and the value is the meter rate (number). |
| tags             | array of strings | Optional meter tags. This array can be empty.                                                 |
| 類別         | 字串           | Category of the resource.                                                                     |
| subcategory      | 字串           | Sub-category of the resource.                                                                 |
| region           | 字串           | Region of the id.                                                                             |
| 單位             | 字串           | The type of quantity (hours, bytes, etc.)                                                     |
| includedQuantity | 數目           | Meter quantity that is included free of charge.                                               |
| effectiveDate    | 字串           | The date this meter is in effect.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| 屬性         | 在工作列搜尋方塊中輸入             | 說明                             |
|------------------|------------------|-----------------------------------------|
| name             | 字串           | Friendly name of the offer term.        |
| discount         | 數目           | The discount applied, if any.           |
| excludedMeterIds | array of strings | Meters excluded from the offer, if any. |
| effectiveDate    | 字串           | The date the offer is in effect.        |