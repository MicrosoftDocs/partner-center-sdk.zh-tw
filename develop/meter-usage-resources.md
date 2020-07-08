---
title: 計量使用量記錄資源
description: 您可以使用 MeterUsageRecord 資源來描述目前計費週期中，訂用帳戶計量層級使用量的預估貨幣成本。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c02c859d1d8ba3edd236d83d3056cb82533f7e8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094776"
---
# <a name="meter-usage-record-resource"></a>計量使用量記錄資源

**適用於：**

- 合作夥伴中心

您可以使用**MeterUsageRecord**資源來描述目前計費週期中，訂用帳戶計量層級使用量的預估貨幣成本。

## <a name="meterusagerecord"></a>MeterUsageRecord

| 屬性         | 類型               | 描述                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | 字串             | 對應至合作夥伴中心訂用帳戶[資源](subscription-resources.md#subscription)識別碼的 GUID，代表 MICROSOFT AZURE （Ms-azr-0017p-流程 ms-azr-0145p）訂用帳戶或 Azure 方案。 對於 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶，此值是 commerce 訂閱識別碼。 若為 Azure 方案訂用帳戶資源，此值為 Azure 方案識別碼。                  |
| MeterId  | 字串             | 取得或設定計量識別碼。                                                        |
| MeterName          | 字串             | 取得或設定計量名稱。                                       |
| 類別               | 字串             | 取得或設定 Azure 資源類別。                                                 |
| 子類別             | 字串             |  取得或設定 Azure 資源子類別。                                                     |
| QuantityUsed        | decimal             | 取得或設定所使用的 Azure 資源數量。   |
| 單位   | 字串             | 取得或設定 Azure 資源的測量單位。 |
| TotalCost   | decimal             | 取得或設定使用量的預估總成本。 |
| CurrencyLocale   | 字串             | 使用訂閱的地區設定。 這個屬性會決定發票上所使用的貨幣。 此屬性適用于 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂閱。 |
| CurrencyCode   | 字串             | 取得或設定貨幣代碼。 此屬性適用于 Azure 方案。                                         |
| USDTotalCost   | decimal             | 取得或設定估計的總成本（美元）。 此屬性適用于 Azure 方案。                                         |
| LastModifiedDate | 字串             | 此記錄上次修改的日期（日期時間格式）。                             |
| 屬性       | ResourceAttributes | 對應至資源的中繼資料屬性。                                        |                                           |
